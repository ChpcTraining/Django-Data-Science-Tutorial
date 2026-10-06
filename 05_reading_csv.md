# Lesson 5 — Reading CSV Data

## Goal

Read and inspect a CSV using Pandas.

In Python:

```python
import pandas as pd

df = pd.read_csv("data/students.csv")

print(df)
```

Useful operations:

```python
df.head()
df.columns
df.shape
df.describe()
```

For example:

```python
print(df.shape)
```

may return:

```text
(5, 3)
```

This means:

```text
5 rows
3 columns
```

## Exercise

Print:

- The first three rows
- The column names
- Number of rows
- Number of columns
