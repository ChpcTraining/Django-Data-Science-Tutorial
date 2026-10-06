# Lesson 6 — Displaying Dataset Information

## Goal

Use Pandas inside a Django view.

Update `explorer/views.py`:

```python
import pandas as pd
from django.shortcuts import render

def home(request):

    df = pd.read_csv("data/students.csv")

    rows = df.shape[0]
    columns = df.shape[1]

    return render(
        request,
        "explorer/index.html",
        {
            "rows": rows,
            "columns": columns
        }
    )
```

In the template:

```html
<h2>Dataset Information</h2>

<p>Rows: {{ rows }}</p>
<p>Columns: {{ columns }}</p>
```

## Exercise

Also pass:

```python
df.columns.tolist()
```

to the template.

Display the column names as an HTML list.
