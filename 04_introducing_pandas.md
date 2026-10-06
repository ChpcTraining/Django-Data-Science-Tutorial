# Lesson 4 — Introducing Pandas

## Goal

Add Pandas to the Django project.

Install:

```bash
pip install pandas
```

Create:

```text
data/students.csv
```

Add:

```csv
name,age,score
Alice,24,78
Bob,27,85
Carol,23,91
David,29,67
Emma,25,88
```

The project now includes:

```text
django-data-science/
├── manage.py
├── config/
├── explorer/
└── data/
    └── students.csv
```

Import Pandas in `explorer/views.py`:

```python
import pandas as pd
```

Pandas represents tabular datasets using a **DataFrame**.
