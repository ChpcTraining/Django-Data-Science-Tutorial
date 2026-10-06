# Lesson 3 — Passing Python Data to HTML

## Goal

Pass Python values from a Django view to an HTML template.

Update the view:

```python
def home(request):

    students = 120

    return render(
        request,
        "explorer/index.html",
        {
            "students": students
        }
    )
```

In the template:

```html
<h2>Students</h2>

<p>Students registered: {{ students }}</p>
```

Django replaces:

```text
{{ students }}
```

with the value from Python.

## Exercise

Create:

```python
course = "Data Science"
students = 120
weeks = 2
```

Pass all three values to the template and display them.

## Key concept

```text
Python variables
       ↓
context dictionary
       ↓
Django template
       ↓
HTML
```
