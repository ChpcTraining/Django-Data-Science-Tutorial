# Lesson 14 — Adding Plots

## Goal

Add Matplotlib to the Django project.

Install:

```bash
pip install matplotlib
```

Create:

```text
explorer/
└── static/
    └── explorer/
        └── plots/
```

The project now includes:

```text
django-data-science/
├── manage.py
├── config/
├── explorer/
│   ├── static/
│   │   └── explorer/
│   │       └── plots/
│   └── templates/
└── data/
```

Import Matplotlib:

```python
import matplotlib.pyplot as plt
```

We can use Pandas to process the data, Matplotlib to create a plot, and Django to display the resulting image.
