# Lesson 12 — Creating a Results Page

## Goal

Display the uploaded dataset analysis as HTML.

Create:

```text
explorer/templates/explorer/results.html
```

Add:

{% raw %}

```html
<!DOCTYPE html>
<html>
<head>
    <title>Dataset Results</title>
</head>
<body>

<h1>Dataset Analysis</h1>

<h2>{{ filename }}</h2>

<p>Rows: {{ rows }}</p>
<p>Columns: {{ columns }}</p>

<h2>Data Preview</h2>

{{ table | safe }}

<h2>Statistical Summary</h2>

{{ summary | safe }}

<p>
    <a href="{% url 'home' %}">
        Upload another dataset
    </a>
</p>

</body>
</html>
```

{% endraw %}

Update the view:

```python
def upload_csv(request):

    if request.method == "POST":

        file = request.FILES["file"]

        df = pd.read_csv(file)

        rows = df.shape[0]
        columns = df.shape[1]

        table = df.head(20).to_html(index=False)
        summary = df.describe().to_html()

        return render(
            request,
            "explorer/results.html",
            {
                "filename": file.name,
                "rows": rows,
                "columns": columns,
                "table": table,
                "summary": summary
            }
        )
```

We use:

```python
df.head(20)
```

so that very large datasets do not create enormous HTML pages.
