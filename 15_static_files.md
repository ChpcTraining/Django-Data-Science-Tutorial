# Lesson 15 — Serving Static Files

## Goal

Understand Django static files.

Static files include:

- CSS
- JavaScript
- Images
- Generated plots

Our application stores files under:

```text
explorer/static/explorer/
```

At the top of a Django template, add:

```django
{% load static %}
```

A plot stored at:

```text
explorer/static/explorer/plots/plot.png
```

can be displayed with:

```html
<img
    src="{% static 'explorer/plots/plot.png' %}"
    alt="Dataset plot"
>
```

During development, Django's development server can serve static files when `DEBUG=True`.

## Why the extra `explorer/` directory?

Using:

```text
static/explorer/
```

namespaces the application's files and helps avoid filename conflicts with other Django apps.
