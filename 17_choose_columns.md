---
render_with_liquid: false
---

# Lesson 17 — Letting the User Choose Columns

## Goal

Use DataFrame columns to dynamically build HTML controls.

Get the columns:

```python
columns = df.columns.tolist()
```

Pass them to the template:

```python
return render(
    request,
    "explorer/results.html",
    {
        "columns": columns
    }
)
```

Create an X-column selector:

```html
<label>X Column</label>

<select name="x_column">

    {% for column in columns %}

        <option value="{{ column }}">
            {{ column }}
        </option>

    {% endfor %}

</select>
```

Create a Y-column selector:

```html
<label>Y Column</label>

<select name="y_column">

    {% for column in columns %}

        <option value="{{ column }}">
            {{ column }}
        </option>

    {% endfor %}

</select>
```

And a plot selector:

```html
<select name="plot_type">

    <option value="scatter">
        Scatter
    </option>

    <option value="line">
        Line
    </option>

    <option value="bar">
        Bar
    </option>

</select>
```

## Key concept

```text
DataFrame columns
       ↓
Python list
       ↓
Django template loop
       ↓
HTML dropdown
```
