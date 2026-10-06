# Final Project — CSV Data Viewer & Plotter

## Objective

Build a complete Django data-science web application.

The user should be able to:

1. Upload a CSV file
2. See the filename
3. See the number of rows
4. See the number of columns
5. See the column names
6. Preview the first 20 rows
7. View descriptive statistics
8. Choose columns for visualisation
9. Choose a plot type
10. Generate and display a plot

## Suggested interface

```text
--------------------------------------------

             CSV DATA EXPLORER

            [ Choose File ]
               [ Analyse ]

--------------------------------------------

Dataset: students.csv

Rows: 1000
Columns: 8

--------------------------------------------

DATA PREVIEW

| Name  | Age | Score |
|-------|-----|-------|
| Alice | 24  | 78    |
| Bob   | 27  | 85    |

--------------------------------------------

STATISTICAL SUMMARY

       count   mean   std   min   max
Age      ...
Score    ...

--------------------------------------------

CREATE VISUALISATION

X Column:  [ Age      ▼ ]
Y Column:  [ Score    ▼ ]
Plot Type: [ Scatter  ▼ ]

           [ Generate Plot ]

--------------------------------------------

                 PLOT

--------------------------------------------
```

## Suggested project structure

```text
django-data-science/
├── manage.py
├── requirements.txt
├── config/
│   ├── settings.py
│   └── urls.py
├── explorer/
│   ├── urls.py
│   ├── views.py
│   ├── templates/
│   │   └── explorer/
│   │       ├── upload.html
│   │       └── results.html
│   └── static/
│       └── explorer/
│           ├── css/
│           │   └── style.css
│           └── plots/
└── data/
    └── students.csv
```

## requirements.txt

```text
django
pandas
matplotlib
```

## Minimum requirements

Your application must:

- Accept `.csv` uploads
- Load the file with Pandas
- Show dataset dimensions
- Show column names
- Show a preview
- Show descriptive statistics
- Generate at least one plot

## Extension challenges

Add:

- CSV validation
- Friendly errors for invalid files
- Missing-value counts
- Column data types
- Histograms
- Scatter plots
- Line plots
- Bar charts
- X/Y column selection
- CSS styling
- Downloadable results
- A JSON API

## What you have learned

```text
HTML
  ↕
Django
  ↕
Python
  ↕
Pandas
  ↕
Matplotlib
```

You have also learned the core Django request flow:

```text
Browser
   ↓
URL
   ↓
View
   ↓
Pandas / Python
   ↓
Template
   ↓
Response
```

The next lesson will expose some of the same data-analysis functionality as an API.
