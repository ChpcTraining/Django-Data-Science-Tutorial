# Lesson 10 — Receiving the Uploaded File

## Goal

Receive the uploaded CSV in a Django view.

Create the upload page:

```python
def home(request):

    return render(
        request,
        "explorer/upload.html"
    )
```

Create the upload view:

```python
from django.http import JsonResponse

def upload_csv(request):

    if request.method == "POST":

        file = request.FILES["file"]

        return JsonResponse({
            "filename": file.name
        })
```

Update `explorer/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.home, name="home"),
    path(
        "upload/",
        views.upload_csv,
        name="upload_csv"
    ),
]
```

The uploaded file is available through:

```python
request.FILES
```

and:

```python
request.FILES["file"]
```

## Exercise

Also return:

```python
file.size
```

to see the uploaded file size.
