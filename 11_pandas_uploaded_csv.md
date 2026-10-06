# Lesson 11 — Reading Uploaded CSVs with Pandas

## Goal

Read the uploaded file directly with Pandas.

Update the view:

```python
def upload_csv(request):

    if request.method == "POST":

        file = request.FILES["file"]

        df = pd.read_csv(file)

        return JsonResponse({
            "filename": file.name,
            "rows": df.shape[0],
            "columns": df.shape[1]
        })
```

The important line is:

```python
df = pd.read_csv(file)
```

Now users can analyse their own CSV rather than a fixed server-side dataset.

## Exercise

Also return:

```python
df.columns.tolist()
```

as:

```text
column_names
```
