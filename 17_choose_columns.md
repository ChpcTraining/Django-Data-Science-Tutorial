# Lesson 17 — Letting the User Choose Columns

## Goal

Use DataFrame columns to dynamically build HTML controls.

Instead of always plotting fixed columns such as:

```python
df["age"]
df["score"]
```

we can allow the user to choose which columns they want to visualise.

## Get the Dataset Columns

Get the columns from the DataFrame:

```python
columns = df.columns.tolist()
```

For our example dataset:

```csv
name,age,score
Alice,24,78
Bob,27,85
Carol,23,91
```

the result would be:

```python
[
    "name",
    "age",
    "score"
]
```

Pass the columns to the template:

```python
return render(
    request,
    "explorer/results.html",
    {
        "columns": columns
    }
)
```

## Create an X-Column Selector

We can use a Django template loop to create the options automatically.

{% raw %}

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

{% endraw %}

Django will generate an option for every column in the dataset.

For example:

```text
X Column:

[ name  ▼ ]
[ age     ]
[ score   ]
```

## Create a Y-Column Selector

We can do the same thing for the Y axis.

{% raw %}

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

{% endraw %}

The user can now independently choose the X and Y columns.

## Add a Plot Type Selector

We can also allow the user to select the type of visualisation.

```html
<label>Plot Type</label>

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

## Add a Generate Button

The controls could be placed inside a form:

{% raw %}

```html
<form method="post">

    {% csrf_token %}

    <label>X Column</label>

    <select name="x_column">

        {% for column in columns %}

            <option value="{{ column }}">
                {{ column }}
            </option>

        {% endfor %}

    </select>


    <label>Y Column</label>

    <select name="y_column">

        {% for column in columns %}

            <option value="{{ column }}">
                {{ column }}
            </option>

        {% endfor %}

    </select>


    <label>Plot Type</label>

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

    <button type="submit">
        Generate Plot
    </button>

</form>
```

{% endraw %}

## Reading the Selected Values

When the form is submitted, Django can access the selected values using:

```python
x_column = request.POST.get("x_column")
y_column = request.POST.get("y_column")
plot_type = request.POST.get("plot_type")
```

For example, the user might select:

```text
X Column:  age
Y Column:  score
Plot Type: scatter
```

Python would receive:

```python
x_column = "age"
y_column = "score"
plot_type = "scatter"
```

We could then generate the plot using:

```python
if plot_type == "scatter":

    plt.scatter(
        df[x_column],
        df[y_column]
    )
```

## Key Concept

The important flow is:

```text
DataFrame
    │
    ▼
Column Names
    │
    ▼
Python List
    │
    ▼
Django Template
    │
    ▼
HTML Dropdowns
    │
    ▼
User Selection
    │
    ▼
POST Request
    │
    ▼
Django View
    │
    ▼
Matplotlib
```

This is an important step toward our final **CSV Data Viewer & Plotter**, because the application is no longer limited to columns chosen by the programmer.

The user can now decide what data they want to visualise.
