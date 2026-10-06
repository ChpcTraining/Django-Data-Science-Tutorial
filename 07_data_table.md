# Lesson 7 — Displaying a Data Table

## Goal

Convert a Pandas DataFrame into an HTML table.

Pandas provides:

```python
table = df.to_html(index=False)
```

Pass it from the view:

```python
return render(
    request,
    "explorer/index.html",
    {
        "table": table
    }
)
```

In the template:

```html
<h2>Dataset</h2>

{{ table | safe }}
```

The `safe` filter tells Django that the generated table should be rendered as HTML.

For large datasets, show only a preview:

```python
table = df.head(20).to_html(index=False)
```

## Exercise

Display only the first 10 rows.
