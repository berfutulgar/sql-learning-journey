# 01 - Data Wrangling & Cleaning

## Goal
Practice SQLZoo-style exercises using a real-world dataset: Google Play Store.

## What Happened
The initial plan was to run basic selection and filtering queries. 
During the first inspection of the data, a structural anomaly was discovered 
that required fixing before any meaningful SQL work could begin.

## 🔍 Data Anomaly
A column shift was identified at row 10472. A missing `Category` value caused 
all fields in that row to shift left by one position, corrupting critical 
columns such as `Installs` and `Rating`.

## 🛠️ The Fix
Rather than dropping the record, the row was surgically repaired using 
Python and Pandas to preserve data integrity across the full dataset.
```python
# Shift all fields one position to the right, then fill the missing Category
df.iloc[10472, 1:] = df.iloc[10472, 1:].astype(object).shift(1)
df.at[10472, 'Category'] = 'PHOTOGRAPHY'
df.to_sql("games", conn, if_exists="replace", index=False)
```

## Status
✅ Data is sanitized and ready for SQL exercises.