---
render_with_liquid: false
---

# Lesson 9 — Uploading a CSV

## Goal

Create a Django form that lets a user select a CSV file.

Create:

```text
explorer/templates/explorer/upload.html
```

Add:

```html
<!DOCTYPE html>
<html>
<head>
    <title>CSV Data Viewer</title>
</head>
<body>

<h1>CSV Data Viewer</h1>

<p>Upload a CSV file to analyse the dataset.</p>

<form action="{% url 'upload_csv' %}"
      method="post"
      enctype="multipart/form-data">

    {% csrf_token %}

    <input
        type="file"
        name="file"
        accept=".csv"
        required
    >

    <button type="submit">
        Analyse CSV
    </button>

</form>

</body>
</html>
```

## Important Django concept

Django POST forms normally include:

```html
{% csrf_token %}
```

This protects the form against Cross-Site Request Forgery.

The form also requires:

```html
enctype="multipart/form-data"
```

because we are uploading a file.
