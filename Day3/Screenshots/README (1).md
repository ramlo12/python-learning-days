# Day 3 – Pandas Data Cleaning Practice

## 📌 Overview

This repository contains my **Day 3 Python and Pandas practice** using an Excel dataset in Google Colab.

The main focus of this practice is **data cleaning and transformation**.

## 🛠️ Tools Used

- Python
- Pandas
- Google Colab
- Microsoft Excel

---

## 📂 Loading the Excel Dataset

```python
# Import the Pandas library and give it the short name pd
import pandas as pd

# Read and load the Excel file into a variable called data
data = pd.read_excel(
    "/content/drive/MyDrive/Colab Notebooks/Supermarket_Practice_Data.xlsx"
)
```

**Somali Interpretation:** Pandas ayaa la import-gareeyay, kadib Excel dataset-ka ayaa laga akhriyey Google Drive waxaana lagu kaydiyey variable-ka `data`.

---

## 📸 Screenshots

### 1️⃣ Loading Excel Data

This screenshot shows how the Excel dataset is loaded into Pandas.

![Loading Excel Data](screenshots/01_load_data.png)

**Somali:** Screenshot-kan wuxuu muujinayaa sida Excel file-ka loogu load-gareeyo Pandas.

---

### 2️⃣ Renaming a Column

The `rename()` method was used to change `Invoice_ID` to `InvoiceID`.

```python
# Rename the Invoice_ID column
data = data.rename(columns={
    "Invoice_ID": "InvoiceID"
})
```

![Renaming Column](screenshots/02_rename_column.png)

**Somali:** Column-ka `Invoice_ID` waxaa loo beddelay `InvoiceID` si magaca column-ku u noqdo mid gaaban oo fudud in la isticmaalo.

---

### 3️⃣ Replacing Values

The `replace()` method was used to standardize values and correct spelling.

```python
# Standardize Payment Method
data["Payment_Method"] = data["Payment_Method"].replace(
    "evc plus", "EVC Plus"
)

# Correct the city spelling
data["City"] = data["City"].replace(
    "Mogadisho", "Mogadishu"
)
```

![Replacing Values](screenshots/03_replace_values.png)

**Somali:** Value-ka `evc plus` waxaa loo beddelay `EVC Plus`, halka `Mogadisho` loo saxay `Mogadishu`.

---

### 4️⃣ Cleaning and Formatting Text

The `.str.strip()` method removes extra spaces, and `.str.title()` formats text consistently.

```python
# Remove extra spaces
data["Category"] = data["Category"].str.strip()

# Convert each word to title case
data["Category"] = data["Category"].str.title()
```

![Cleaning Text](screenshots/04_clean_text.png)

**Somali:** `.str.strip()` waxay ka saartaa spaces-ka dheeraadka ah, halka `.str.title()` ay text-ka ka dhigto qaab isku mid ah sida `Grocery`.

---

## 5️⃣ Replacing Category Values

Before replacing values, `value_counts()` can be used to inspect existing categories.

```python
# Display the count of each unique value
data["Category"].value_counts()
```

Then a value can be replaced:

```python
# Replace grocery with Grocery
data["Category"] = data["Category"].replace(
    "grocery",
    "Grocery"
)
```

**Somali Interpretation:** Marka hore waxaan hubinaynaa values-ka ku jira `Category`, kadib `grocery` ayaan u beddelaynaa `Grocery`.

---

## 6️⃣ Numerical Replacement

Numerical values can also be replaced with descriptive labels.

```python
# Replace numerical values with text labels
data["Quantity"] = data["Quantity"].replace({
    1: "Low",
    2: "Medium",
    3: "more"
})
```

**Somali Interpretation:** Values-ka `1`, `2`, iyo `3` waxaa loo beddelay labels qoraal ah.

---

## 7️⃣ Removing Unnecessary Columns

```python
# Remove the InvoiceID column and save the result
data = data.drop(columns=["InvoiceID"])
```

**Somali Interpretation:** Column-ka `InvoiceID` ayaa laga saaray dataset-ka, kadib result-ka waxaa dib loogu kaydiyey `data`.

---

## 8️⃣ Checking and Changing Data Types

First, check the data types:

```python
# Display the data type of every column
data.dtypes
```

Convert values to numeric:

```python
# Convert values to numeric and change invalid values to missing values
data["Quantity"] = pd.to_numeric(
    data["Quantity"],
    errors="coerce"
).astype("Int64")
```

**Somali Interpretation:** `pd.to_numeric()` wuxuu isku dayayaa inuu values-ka u beddelo numbers. `errors="coerce"` wuxuu values-ka aan number-ka ahayn u beddelayaa missing values.

> **Important Note:** Haddii `Quantity` hore loogu beddelay text sida `Low`, `Medium`, iyo `more`, kadib `pd.to_numeric()` wuxuu values-kaas u beddeli karaa missing values. Sidaas darteed, column numeric ah waa in aan text loo beddelin haddii analysis dambe uu u baahan yahay numbers.

---

## 📚 Key Concepts Practiced

- Loading Excel data with `pd.read_excel()`
- Inspecting data with `head()`, `columns`, `dtypes`, and `value_counts()`
- Renaming columns with `rename()`
- Replacing values with `replace()`
- Dropping unnecessary columns with `drop()`
- Converting data types with `pd.to_numeric()` and `astype()`
- Removing extra spaces with `str.strip()`
- Formatting text with `str.title()`

---

## ▶️ How to Run This Project

1. Open `day_3.ipynb` in Google Colab.
2. Make sure the Excel file path is correct.
3. Run the cells from top to bottom.
4. Check the output after every data-cleaning step.

---

## 👩‍💻 Author

**Day 3 – Python & Pandas Data Cleaning Practice**
