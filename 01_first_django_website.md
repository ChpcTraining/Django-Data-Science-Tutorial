# Lesson 1 — Your First Django Website

## Goal

Create a Django project, create an application, and understand the relationship between URLs and views.

## 1.1 Create the project

```bash
mkdir django-data-science
cd django-data-science

python -m venv venv
```

Activate the environment.

Linux/macOS:

```bash
source venv/bin/activate
```

Windows:

```bash
venv\Scripts\activate
```

Install Django:

```bash
pip install django
```

Create a Django project:

```bash
django-admin startproject config .
```

Create an application:

```bash
python manage.py startapp explorer
```

Your project should now contain:

```text
django-data-science/
├── manage.py
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── ...
└── explorer/
    ├── views.py
    ├── models.py
    └── ...
```

## 1.2 Register the application

In `config/settings.py`, add:

```python
INSTALLED_APPS = [
    # Django apps...
    "explorer",
]
```

## 1.3 Create your first view

In `explorer/views.py`:

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Welcome to Data Science with Django")
```

Create `explorer/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.home, name="home"),
]
```

Update `config/urls.py`:

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("explorer.urls")),
]
```

Run the server:

```bash
python manage.py runserver
```

Visit:

```text
http://127.0.0.1:8000/
```

## Key concept

```text
Browser
   ↓
urls.py
   ↓
views.py
   ↓
Response
```

## Exercise

Create `/about/` that returns:

```text
Data Science with Django and Python
```
