# Lesson 13 — Understanding Django Application Flow

## Goal

Understand how the different Django components work together.

Our application now follows:

```text
USER
  │
  │ GET /
  ▼
config/urls.py
  │
  ▼
explorer/urls.py
  │
  ▼
home view
  │
  ▼
upload.html
  │
  │ POST CSV
  ▼
upload_csv view
  │
  ▼
Pandas
  │
  ├── read_csv()
  ├── shape
  ├── head()
  └── describe()
  │
  ▼
results.html
  │
  ▼
USER
```

## Compared with Streamlit

Streamlit might use:

```python
file = st.file_uploader("Upload CSV")
df = pd.read_csv(file)
st.dataframe(df)
```

Django makes the web application structure explicit:

```text
URL
 ↓
View
 ↓
Python processing
 ↓
Template
 ↓
Response
```

This structure becomes useful as applications become larger.
