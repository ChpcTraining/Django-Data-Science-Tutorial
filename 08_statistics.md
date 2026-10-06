# Lesson 8 — Generating Statistics

## Goal

Generate descriptive statistics with Pandas and display them in Django.

Pandas provides:

```python
df.describe()
```

Convert it to HTML:

```python
summary = df.describe().to_html()
```

Pass it to the template:

```python
return render(
    request,
    "explorer/index.html",
    {
        "table": table,
        "summary": summary
    }
)
```

HTML:

```html
<h2>Statistical Summary</h2>

{{ summary | safe }}
```

Other useful Pandas operations include:

```python
df.mean(numeric_only=True)
df.min(numeric_only=True)
df.max(numeric_only=True)
df.isnull().sum()
```

## Exercise

Calculate the number of missing values in each column.
