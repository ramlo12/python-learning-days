# Day 4 — Data Cleaning with Pandas

## Overview

Day 4 focused on **missing values, filling missing data, and duplicate records** using the supermarket practice dataset.

The notebook used:
- `pandas`
- Excel input: `Supermarket_Practice_Data.xlsx`
- Starting dataset size: **122 rows × 13 columns**

This README is based on the uploaded and executed `day 4.ipynb`. The PNGs are screenshot-style learning summaries made from the notebook's code and recorded outputs.

---

## 1. Detect Missing Values

### `isna()` and `isnull()`

```python
# Check all missing values in the entire dataset
data.isna()
```

- `True` = missing
- `False` = present

The notebook also checked a single column with:

```python
# Check missing values only in the City column
data["City"].isnull()
```

`isna()` and `isnull()` are used for the same missing-value check.

![Detect Missing Values](01_detect_missing.png)

---

## 2. Count Missing Values

```python
# Count the number of missing values in each column
Missing_Data = data.isnull().sum()

Missing_Data
```

Recorded results:

| Column | Missing |
|---|---:|
| Invoice_ID | 0 |
| Sale_Date | 0 |
| Product | 1 |
| Category | 0 |
| City | 1 |
| Quantity | 1 |
| Unit_Price | 1 |
| Discount | 0 |
| Revenue | 1 |
| Cost | 0 |
| Payment_Method | 0 |
| Customer_Type | 1 |
| Data_Quality_Issues | 82 |

Total missing cells:

```text
88
```

![Count Missing Values](02_count_missing.png)

---

## 3. Missing Value Percentage

The notebook calculated the missing-value percentage:

```python
# Calculate the percentage of missing values in each column
Missing_Percentage = data.isna().mean() * 100

Missing_Percentage
```

Results recorded in the notebook:

- Product → `0.819672%`
- City → `0.819672%`
- Quantity → `0.819672%`
- Unit_Price → `0.819672%`
- Revenue → `0.819672%`
- Customer_Type → `0.819672%`
- Data_Quality_Issues → `67.213115%`

The idea is:

```text
missing / total × 100
```

![Missing Value Percentage](03_missing_percentage.png)

---

## 4. Mode and Count

**Mode** is the value that occurs most frequently.

The notebook practiced this with `City`:

```python
# Get the mode and count for City
mode = data["City"].mode()[0]
count = data["City"].value_counts()[mode]

print("Column:", "City")
print("Mode:", mode)
print("Count:", count)
```

Recorded result:

```text
Column: City
Mode: Mogadishu
Count: 38
```

The notebook's City frequency result was:

- Mogadishu → 38
- Garowe → 31
- Kismayo → 28
- Hargeisa → 23
- Mogadisho → 1

![Mode and Count](04_mode.png)

---

## 5. Mode for Every Column

The notebook also practiced:

```python
# Get the mode of each column
modes = data.mode().iloc[0]
```

Then it used a loop and `value_counts()` to count the frequency of each mode.

This practiced:
- `mode()`
- `iloc[0]`
- `value_counts()`
- `data.columns`
- `for` loops

---

## 6. Find Rows With Missing Values

The notebook used:

```python
# Show rows with at least one missing value
data[data.isna().any(axis=1)]
```

This displays rows containing at least one missing value.

It does **not** delete them.

---

## 7. Delete vs Fill

Two approaches were studied:

### Delete
Remove rows that contain missing values.

### Fill
Keep the row and replace the missing value with a reasonable value.

The correct choice depends on the column and the amount/meaning of missing data.

---

## 8. Removing Missing Rows with `dropna()`

The notebook tested:

```python
# Create a new dataset without rows containing missing values
data_clean = data.dropna()
```

Then compared:

```python
# Compare the number of rows before and after cleaning
print("Before:", data.shape[0])
print("After:", data_clean.shape[0])
```

Recorded result:

```text
Before: 122
After: 34
```

This showed that `dropna()` can remove many rows when a dataset contains missing values.

The notebook stored the result in `data_clean`, so the original `data` variable was not directly overwritten.

![dropna](05_dropna.png)

---

## 9. Filling Numerical Data — Mean and Median

Numerical columns can be filled using statistics such as mean or median.

### Quantity

The notebook calculated:

```python
# Get the mean of Quantity
Quantity_mean = data["Quantity"].mean()

# Get the median of Quantity
Quantity_median = data["Quantity"].median()
```

Recorded values:

```text
Mean   = 4.115702479338843
Median = 4.0
```

The missing Quantity value was filled with the mean:

```python
# Fill missing Quantity using the mean
data["Quantity"] = data["Quantity"].fillna(Quantity_mean)
```

The final check returned:

```text
0
```

### Unit_Price

The notebook recorded:

```text
Mean   = 2.5289256198347108
Median = 2.11
```

It then filled the missing `Unit_Price` using the mean and confirmed that the missing-value count was `0`.

![Numerical Data](06_fill_numerical.png)

---

## 10. Filling Categorical Data — Mode

Categorical columns were filled using their mode.

### Product

```python
# Find the mode of Product
Product_mode = data["Product"].mode()[0]

# Fill missing Product using the mode
data["Product"] = data["Product"].fillna(Product_mode)
```

Recorded mode:

```text
Orange Juice 1L
```

Missing-value check:

```text
0
```

### City

Recorded mode:

```text
Mogadishu
```

Missing-value check:

```text
0
```

### Customer_Type

Recorded mode:

```text
Regular
```

Missing-value check:

```text
0
```

![Categorical Data](07_fill_categorical.png)

---

## 11. Why Not `fillna(0)` Everywhere?

The lesson demonstrated that `0` should not automatically replace every missing value.

For example:

- A missing City should not become `0`.
- A missing Product should not become `0`.
- A numerical value may also need a more meaningful replacement than `0`.

The approach practiced in Day 4 was:

```text
Numerical data → Mean / Median
Categorical data → Mode
```

---

## 12. Duplicate Records

Duplicates are repeated records.

The notebook first detected duplicates:

```python
# Check duplicate rows
data.duplicated()
```

Then counted them:

```python
# Count duplicate rows
data.duplicated().sum()
```

Recorded result:

```text
2
```

The notebook then displayed all members of duplicate groups:

```python
# Show all rows belonging to duplicate groups
data[data.duplicated(keep=False)]
```

The duplicate pairs were:

- Row `12` ↔ Row `120` → `INV-1013`
- Row `45` ↔ Row `121` → `INV-1046`

![Duplicate Records](08_duplicates.png)

---

## 13. Remove Duplicate Records

The notebook created a new dataset:

```python
# Remove duplicate rows and create a new dataset
data_no_duplicates = data.drop_duplicates()
```

The resulting shape was:

```text
(120, 13)
```

Meaning:

```text
122 original rows
- 2 duplicate rows
= 120 rows
```

There were still **13 columns**.

---

# Day 4 Final Summary

| Skill | Pandas |
|---|---|
| Detect missing values | `isna()`, `isnull()` |
| Count missing values | `sum()` |
| Missing percentage | `mean() * 100` |
| Find most common value | `mode()` |
| Count frequencies | `value_counts()` |
| Show rows with missing values | `isna().any(axis=1)` |
| Remove rows with missing values | `dropna()` |
| Fill missing values | `fillna()` |
| Detect duplicates | `duplicated()` |
| Count duplicates | `duplicated().sum()` |
| Remove duplicates | `drop_duplicates()` |
| Select first positional mode | `iloc[0]` |

## Day 4 Workflow

```text
Load data
   ↓
Detect missing values
   ↓
Count missing values
   ↓
Calculate missing percentages
   ↓
Inspect missing rows
   ↓
Choose Delete or Fill
   ↓
Fill numerical data with Mean/Median
   ↓
Fill categorical data with Mode
   ↓
Detect duplicate records
   ↓
Remove duplicate records
```

## Important Data Note

The executed notebook recorded **82 missing values in `Data_Quality_Issues`**. Those values were not filled in the later steps. Therefore, Day 4 did **not** completely remove every missing value from every column.

The notebook also contained the test:

```python
data_clean = data.dropna()
```

which reduced the row count from `122` to `34`. This was a demonstration of `dropna()`, not proof that the final working dataset should necessarily be reduced to 34 rows.

---

## Included Screenshots

1. `01_detect_missing.png`
2. `02_count_missing.png`
3. `03_missing_percentage.png`
4. `04_mode.png`
5. `05_dropna.png`
6. `06_fill_numerical.png`
7. `07_fill_categorical.png`
8. `08_duplicates.png`

The original notebook is also included as `day_4.ipynb`.
