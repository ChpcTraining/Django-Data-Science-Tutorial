# Lesson 16 — Creating Your First Plot

## Goal

Generate a plot from Pandas data and display it in Django.

Suppose the dataset contains:

```csv
name,age,score
Alice,24,78
Bob,27,85
Carol,23,91
David,29,67
Emma,25,88
```

Create a scatter plot:

```python
import matplotlib.pyplot as plt

plt.figure()

plt.scatter(
    df["age"],
    df["score"]
)

plt.xlabel("Age")
plt.ylabel("Score")
plt.title("Age vs Score")

plt.savefig(
    "explorer/static/explorer/plots/plot.png"
)

plt.close()
```

Then in the template, load Django's static files:

{% raw %}

```django
{% load static %}
```

{% endraw %}

Display the generated plot:

{% raw %}

```html
<img
    src="{% static 'explorer/plots/plot.png' %}"
    alt="Age vs Score"
>
```

{% endraw %}

## Important

Always close the figure after saving:

```python
plt.close()
```

This prevents figures from accumulating in server memory.

## Application Flow

Our plotting process now looks like:

```text
CSV Dataset
     │
     ▼
   Pandas
     │
     ▼
 Matplotlib
     │
     ▼
  plot.png
     │
     ▼
Django Static File
     │
     ▼
   Browser
```

We use **Pandas** to work with the dataset and **Matplotlib** to generate the visualisation.
