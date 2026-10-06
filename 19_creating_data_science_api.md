# Lesson 19 — Creating a Data Science API

## Goal

So far, Django has returned our analysis as HTML.

Now we will create a simple endpoint that:

1. Accepts a CSV
2. Loads it with Pandas
3. Calculates information about the dataset
4. Returns the result as JSON

The difference is:

```text
Website

Browser → Django → Pandas → HTML → User
```

versus:

```text
API

Application → Django → Pandas → JSON → Application
```

> This lesson uses Django's built-in `JsonResponse` to keep things simple. Larger Django APIs commonly use a dedicated API framework, but we do not need one for this introduction.

---

## 19.1 Create a Simple JSON Endpoint

In `explorer/views.py`:

```python
from django.http import JsonResponse

def api_status(request):

    return JsonResponse({
        "status": "running",
        "service": "Data Science API"
    })
```

Add the URL:

```python
path(
    "api/status/",
    views.api_status,
    name="api_status"
),
```

Visit:

```text
http://127.0.0.1:8000/api/status/
```

Django returns JSON:

```json
{
    "status": "running",
    "service": "Data Science API"
}
```

---

## 19.2 Create a CSV Analysis Endpoint

Create:

```text
POST /api/analyse/
```

In `views.py`:

```python
def api_analyse(request):

    if request.method == "POST":

        file = request.FILES["file"]

        df = pd.read_csv(file)

        return JsonResponse({
            "filename": file.name,
            "rows": df.shape[0],
            "columns": df.shape[1]
        })

    return JsonResponse(
        {"error": "POST request required"},
        status=405
    )
```

Add:

```python
path(
    "api/analyse/",
    views.api_analyse,
    name="api_analyse"
),
```

The flow is:

```text
CSV
 │
 ▼
Django
 │
 ▼
Pandas
 │
 ├── rows
 └── columns
 │
 ▼
JSON
```

---

## 19.3 Return Column Information

Add:

```python
"column_names": df.columns.tolist()
```

The endpoint becomes:

```python
def api_analyse(request):

    if request.method == "POST":

        file = request.FILES["file"]

        df = pd.read_csv(file)

        return JsonResponse({
            "filename": file.name,
            "rows": df.shape[0],
            "columns": df.shape[1],
            "column_names": df.columns.tolist()
        })

    return JsonResponse(
        {"error": "POST request required"},
        status=405
    )
```

A response might look like:

```json
{
    "filename": "students.csv",
    "rows": 5,
    "columns": 3,
    "column_names": [
        "name",
        "age",
        "score"
    ]
}
```

---

## 19.4 Return Summary Statistics

Pandas provides:

```python
df.describe()
```

Convert it to a dictionary:

```python
summary = df.describe().to_dict()
```

Then return:

```python
return JsonResponse({
    "filename": file.name,
    "rows": df.shape[0],
    "columns": df.shape[1],
    "column_names": df.columns.tolist(),
    "summary": summary
})
```

Now the endpoint provides a reusable data-analysis service.

---

## 19.5 Website vs API

Our Django application now provides two types of response.

### Website

```python
return render(
    request,
    "explorer/results.html",
    context
)
```

returns:

```text
HTML
```

### API

```python
return JsonResponse({
    "rows": df.shape[0]
})
```

returns:

```text
JSON
```

So Django can provide:

```text
                    Django
                       │
              ┌────────┴────────┐
              │                 │
           Website              API
              │                 │
            HTML               JSON
              │                 │
            Human          Application
```

---

## 19.6 Test the API from Python

Install Requests:

```bash
pip install requests
```

Create:

```text
test_api.py
```

Add:

```python
import requests

url = "http://127.0.0.1:8000/api/analyse/"

with open("students.csv", "rb") as file:

    response = requests.post(
        url,
        files={"file": file}
    )

print(response.json())
```

### A note about CSRF

Django protects POST requests with CSRF protection.

For a classroom demonstration of a programmatic API endpoint, you may need to exempt this specific view:

```python
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def api_analyse(request):
    ...
```

Use this only to understand the basic API concept. In a production API, authentication and security should be designed properly rather than simply disabling protection broadly.

---

## Exercise

Return the number of missing values in each column.

Pandas provides:

```python
df.isnull().sum().to_dict()
```

Add:

```python
"missing_values": df.isnull().sum().to_dict()
```

The response could contain:

```json
{
    "missing_values": {
        "name": 0,
        "age": 0,
        "score": 2
    }
}
```

---

## Final Challenge

Create:

```text
POST /api/preview/
```

It should return the first five rows.

Use:

```python
df.head().to_dict(orient="records")
```

Because the top-level result is a list, use:

```python
return JsonResponse(
    preview,
    safe=False
)
```

A response could look like:

```json
[
    {
        "name": "Alice",
        "age": 24,
        "score": 78
    },
    {
        "name": "Bob",
        "age": 27,
        "score": 85
    }
]
```

---

## What You Have Learned

You now have both a Django data-science website and a simple API:

```text
                  CSV DATA
                      │
                      ▼
                    Pandas
                      │
                      ▼
                    Django
                  /        \
                 /          \
              HTML          JSON
               │              │
               ▼              ▼
             User        Other Software
```

The same Pandas functionality can therefore be used by both a human-facing website and other software.
