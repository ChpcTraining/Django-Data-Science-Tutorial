# Lesson 20 — Making Your Django Site Look Nice with Bootstrap

## Goal

Our Django application works, but so far we have focused on functionality rather than appearance.

In this lesson we will use **Bootstrap** to make our application look more professional.

We will not add any new functionality.

The goal is simply:

```text
Plain HTML
    │
    ▼
Add Bootstrap
    │
    ▼
Modern-looking Website
```

By the end of this lesson, we will have:

- A navigation bar
- Better page spacing
- Cards
- Styled buttons
- Styled forms
- Better-looking tables
- A responsive layout

---

## 20.1 What is Bootstrap?

Bootstrap is a **CSS framework**.

Instead of writing all of our own CSS, Bootstrap provides ready-made styles that we can use by adding classes to our HTML.

For example, a normal HTML button:

```html
<button>
    Analyse Dataset
</button>
```

can become:

```html
<button class="btn btn-primary">
    Analyse Dataset
</button>
```

Bootstrap automatically gives the button:

- Colour
- Padding
- Rounded corners
- Hover effects
- Consistent styling

We do not need to write the CSS ourselves.

---

## 20.2 Add Bootstrap to the Page

Bootstrap can be added using a CDN.

A CDN allows our webpage to load Bootstrap directly from the internet.

Inside the `<head>` section of your HTML page, add:

```html
<link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
    rel="stylesheet"
>
```

For example:

```html
<!DOCTYPE html>

<html>

<head>

    <title>CSV Data Explorer</title>

    <link
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
        rel="stylesheet"
    >

</head>

<body>

    <h1>CSV Data Explorer</h1>

</body>

</html>
```

Bootstrap is now available on the page.

---

## 20.3 Add a Navigation Bar

Let's add a simple navigation bar to the top of our application.

```html
<nav class="navbar navbar-dark bg-dark">

    <div class="container">

        <span class="navbar-brand">

            Data Science Explorer

        </span>

    </div>

</nav>
```

Notice the classes:

```text
navbar
navbar-dark
bg-dark
container
navbar-brand
```

These are Bootstrap classes.

Bootstrap already knows how these elements should look.

---

## 20.4 Add a Page Container

Without styling, HTML normally stretches across the entire browser window.

Bootstrap provides:

```html
<div class="container">

</div>
```

This gives our content a sensible maximum width.

We can also add vertical spacing:

```html
<div class="container py-5">

</div>
```

The class:

```text
py-5
```

adds padding to the top and bottom of the container.

Our page can now look like:

```html
<body>

<nav class="navbar navbar-dark bg-dark">

    <div class="container">

        <span class="navbar-brand">
            Data Science Explorer
        </span>

    </div>

</nav>


<div class="container py-5">

    <h1>CSV Data Explorer</h1>

    <p>
        Upload a dataset to begin exploring your data.
    </p>

</div>

</body>
```

---

## 20.5 Use the Bootstrap Grid

Bootstrap includes a grid system for controlling page layout.

For example:

```html
<div class="row justify-content-center">

    <div class="col-md-8">

        Content goes here

    </div>

</div>
```

This means our content will use approximately eight columns of the Bootstrap grid on medium and larger screens.

It will also be centred.

The page structure becomes:

```text
Browser
│
└── Container
      │
      └── Row
            │
            └── Column
                  │
                  └── Content
```

---

## 20.6 Put Our Content Inside a Card

Bootstrap cards are useful for grouping content.

```html
<div class="card">

    <div class="card-body">

        <h2>Upload Dataset</h2>

        <p>
            Select a CSV file to analyse.
        </p>

    </div>

</div>
```

We can make the card stand out slightly:

```html
<div class="card shadow-sm">
```

The class:

```text
shadow-sm
```

adds a small shadow.

---

## 20.7 Style the Upload Form

Our original file input might look like:

```html
<input
    type="file"
    name="file"
>
```

Bootstrap can style it with:

```html
<input
    class="form-control"
    type="file"
    name="file"
>
```

We can also style the label:

```html
<label class="form-label">
    Select CSV file
</label>
```

And add spacing:

```html
<div class="mb-3">

    <label class="form-label">
        Select CSV file
    </label>

    <input
        class="form-control"
        type="file"
        name="file"
    >

</div>
```

The class:

```text
mb-3
```

adds margin below the element.

---

## 20.8 Style the Button

Our original button:

```html
<button type="submit">
    Analyse Dataset
</button>
```

can become:

```html
<button
    class="btn btn-primary"
    type="submit"
>

    Analyse Dataset

</button>
```

Other Bootstrap button styles include:

```html
<button class="btn btn-success">
    Success
</button>

<button class="btn btn-danger">
    Delete
</button>

<button class="btn btn-secondary">
    Cancel
</button>

<button class="btn btn-outline-primary">
    Learn More
</button>
```

Changing the appearance does not require changing any Python or Django code.

---

# 20.9 Complete Styled Upload Page

Let's combine everything.

Because this is a Django template, the example is wrapped so that GitHub Pages does not try to process the Django template tags.

{% raw %}

```html
<!DOCTYPE html>

<html>

<head>

    <title>CSV Data Explorer</title>

    <link
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
        rel="stylesheet"
    >

</head>


<body class="bg-light">


<nav class="navbar navbar-dark bg-dark">

    <div class="container">

        <span class="navbar-brand">

            Data Science Explorer

        </span>

    </div>

</nav>


<div class="container py-5">


    <div class="row justify-content-center">


        <div class="col-md-8">


            <div class="card shadow-sm">


                <div class="card-body p-4">


                    <h1 class="mb-3">

                        CSV Data Explorer

                    </h1>


                    <p class="text-muted">

                        Upload a CSV dataset to explore
                        its structure and statistics.

                    </p>


                    <form
                        method="post"
                        enctype="multipart/form-data"
                    >

                        {% csrf_token %}


                        <div class="mb-3">

                            <label class="form-label">

                                Select CSV file

                            </label>


                            <input
                                class="form-control"
                                type="file"
                                name="file"
                                accept=".csv"
                                required
                            >

                        </div>


                        <button
                            class="btn btn-primary"
                            type="submit"
                        >

                            Analyse Dataset

                        </button>


                    </form>


                </div>

            </div>

        </div>

    </div>

</div>


</body>

</html>
```

{% endraw %}

Run your Django server:

```bash
python manage.py runserver
```

Then visit:

```text
http://127.0.0.1:8000/
```

Compare the page with the original version.

The application functionality has not changed.

Only its appearance has changed.

---

# 20.10 Styling the Results Page

We can apply the same Bootstrap ideas to our results page.

For example, dataset information can be displayed inside a card.

{% raw %}

```html
<div class="card shadow-sm mb-4">

    <div class="card-body">

        <h2 class="card-title">
            Dataset Information
        </h2>

        <p>
            <strong>Filename:</strong>
            {{ filename }}
        </p>

        <p>
            <strong>Rows:</strong>
            {{ rows }}
        </p>

        <p>
            <strong>Columns:</strong>
            {{ columns }}
        </p>

    </div>

</div>
```

{% endraw %}

The classes:

```text
card
shadow-sm
mb-4
card-body
card-title
```

give us a clean information panel without writing custom CSS.

---

# 20.11 Styling Tables

Bootstrap can also make normal HTML tables look much better.

A plain table:

```html
<table>
```

can become:

```html
<table class="table table-striped table-hover">
```

The classes mean:

```text
table
    Basic Bootstrap table styling

table-striped
    Alternating row colours

table-hover
    Highlights a row when the mouse moves over it
```

You can also place large tables inside:

```html
<div class="table-responsive">

    <!-- table here -->

</div>
```

This helps tables work better on smaller screens.

---

# 20.12 Useful Bootstrap Classes

You do not need to memorise Bootstrap.

Here are some useful classes:

| Class | Purpose |
|---|---|
| `container` | Centres page content |
| `py-5` | Adds vertical padding |
| `mb-3` | Adds bottom margin |
| `mb-4` | Adds more bottom margin |
| `p-4` | Adds padding |
| `bg-light` | Light background |
| `text-muted` | Softer text colour |
| `card` | Creates a card |
| `shadow-sm` | Adds a small shadow |
| `btn` | Creates a button |
| `btn-primary` | Primary button style |
| `form-control` | Styles form inputs |
| `form-label` | Styles form labels |
| `table` | Styles a table |
| `table-striped` | Alternating table rows |
| `table-hover` | Table row hover effect |

---

# Exercise

Take one of your existing Django pages and improve its appearance using Bootstrap.

Try adding:

- A navbar
- A container
- A card
- A styled button
- Better spacing

Do not change any Python code.

---

# Challenge

Try changing:

```html
<div class="col-md-8">
```

to:

```html
<div class="col-md-6">
```

What happens?

Then try:

```html
<div class="col-md-10">
```

Also experiment with:

```html
btn-primary
```

versus:

```html
btn-success
```

or:

```html
btn-dark
```

The goal is to experiment with Bootstrap classes and see how they affect the appearance of the page.

---

# What You Have Learned

Before Bootstrap, our application might look like:

```text
Plain HTML
    │
    ├── Heading
    ├── File Input
    └── Button
```

After Bootstrap:

```text
Django Template
       │
       ▼
      HTML
       │
       ▼
 Bootstrap Classes
       │
       ▼
 Navbar + Layout + Cards
       │
       ▼
 Styled Forms + Buttons
       │
       ▼
Modern-looking Website
```

Most importantly:

> **We did not change our Django or Pandas functionality.**

Bootstrap only changed the **presentation** of our application.

Our overall application now consists of:

```text
Django
   │
   ├── Views       → Application logic
   │
   ├── Pandas      → Data processing
   │
   ├── Templates   → Page structure
   │
   └── Bootstrap   → Appearance
```

You can therefore improve the appearance of a Django application without having to redesign the Python code that powers it.