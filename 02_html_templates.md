# Lesson 2 — Creating HTML Pages

## Goal

Render a normal HTML page using Django templates.

Create:

```text
explorer/
└── templates/
    └── explorer/
        └── index.html
```

Add to `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Data Science Portal</title>
</head>
<body>

<h1>Data Science Portal</h1>

<p>Welcome to my Django website.</p>

<h2>What can we do?</h2>

<ul>
    <li>Upload datasets</li>
    <li>Analyse data</li>
    <li>View statistics</li>
    <li>Create plots</li>
</ul>

</body>
</html>
```

Change `explorer/views.py`:

```python
from django.shortcuts import render

def home(request):
    return render(
        request,
        "explorer/index.html"
    )
```

Refresh the browser.

## Key concept

Django now follows:

```text
Browser → URL → View → Template → HTML → Browser
```

The view decides which template should be returned.
