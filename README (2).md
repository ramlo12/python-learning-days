# Day 3 – Pandas Data Cleaning Practice

## 📌 Overview
This notebook contains my Day 3 Python and Pandas practice using an Excel dataset in Google Colab.

The main focus of this practice is **data cleaning and transformation**.

## 🛠️ Tools Used
- Python
- Pandas
- Google Colab
- Microsoft Excel dataset

## 📂 Dataset Loading
```python
import pandas as pd

data = pd.read_excel(
    "/content/drive/MyDrive/Colab Notebooks/Supermarket_Practice_Data.xlsx"
)
```

**Somali interpretation:** Pandas ayaa la import-gareeyay, kadib Excel dataset-ka ayaa laga akhriyey Google Drive waxaana lagu kaydiyey variable-ka `data`.

---

## 1. Renaming Columns

The `rename()` method was used to change a column name.

```python
data = data.rename(columns={
    "Invoice_ID": "InvoiceID"
})
```

**Somali interpretation:** Column-ka `Invoice_ID` waxaa loo beddelay `InvoiceID` si magaca column-ku u noqdo mid gaaban oo fudud in la isticmaalo.

---

## 2. Replacing Text Values

### Payment Method
```python
data["Payment_Method"] = data["Payment_Method"].replace(
    "evc plus", "EVC Plus"
)
```

**Somali interpretation:** Value-ka `evc plus` waxaa loo beddelay `EVC Plus` si capitalization-ka loo mideeyo.

### City Name
```python
data["City"] = data["City"].replace(
    "Mogadisho", "Mogadishu"
)
```

**Somali interpretation:** Magaca magaalada oo khaldan `Mogadisho` waxaa loo saxay `Mogadishu`.

### Category
```python
data["Category"] = data["Category"].replace(
    "grocery", "Grocery"
)
```

**Somali interpretation:** Value-ka `grocery` waxaa loo beddelay `Grocery`.

Before making replacements, `value_counts()` was used to inspect existing values.

```python
data["Category"].value_counts()
```

---

## 3. Numerical Replacement

The notebook also practiced replacing numerical values with text labels.

```python
data["Quantity"] = data["Quantity"].replace({
    1: "Low",
    2: "Medium",
    3: "more"
})
```

**Somali interpretation:** Values-ka 1, 2, iyo 3 waxaa loo beddelay labels qoraal ah.

---

## 4. Removing Unnecessary Columns

```python
data.drop(columns=["InvoiceID"])
```

**Somali interpretation:** Code-kan wuxuu sameeyaa DataFrame cusub oo aan lahayn `InvoiceID`. Si isbeddelka loogu kaydiyo `data`, waxaa fiican:

```python
data = data.drop(columns=["InvoiceID"])
```

---

## 5. Checking and Changing Data Types

First, data types were checked:

```python
data.dtypes
```

Then a numeric conversion was practiced:

```python
data["Quantity"] = pd.to_numeric(
    data["Quantity"],
    errors="coerce"
).astype("Int64")
```

**Somali interpretation:** `pd.to_numeric()` wuxuu isku dayayaa inuu values-ka u beddelo numbers. `errors="coerce"` wuxuu values-ka aan number-ka ahayn u beddelayaa missing value (`NaN`), kadibna `Int64` ayaa loo isticmaalayaa integer type oo taageera missing values.

> Note: In this notebook, `Quantity` was previously replaced with text labels (`Low`, `Medium`, `more`), so converting it back to numeric will turn those text values into missing values. In a real workflow, do not convert a column to text labels if you later need it as a numeric column.

---

## 6. Cleaning Text with `str.strip()`

```python
data["Category"] = data["Category"].str.strip()
```

**Somali interpretation:** `.str.strip()` waxay ka saartaa spaces-ka dheeraadka ah ee bilowga iyo dhammaadka text-ka.

---

## 7. Formatting Text with `str.title()`

```python
data["Category"] = data["Category"].str.title()
```

**Somali interpretation:** `.str.title()` waxay xarafka ugu horreeya ee eray kasta ka dhigtaa uppercase.

Example:

`grocery` → `Grocery`

---

## 📸 Screenshots
The repository includes screenshots created from the main Day 3 practice sections:

- `screenshots/01_load_data.png`
- `screenshots/02_rename_column.png`
- `screenshots/03_replace_values.png`
- `screenshots/04_clean_text.png`

## 📚 Key Concepts Practiced
- Loading Excel data with `pd.read_excel()`
- Inspecting data with `head()`, `columns`, `dtypes`, and `value_counts()`
- Renaming columns with `rename()`
- Replacing values with `replace()`
- Dropping unnecessary columns with `drop()`
- Converting data types with `pd.to_numeric()` and `astype()`
- Removing extra spaces with `str.strip()`
- Standardizing text formatting with `str.title()`

## ▶️ How to Run
1. Open `day_3.ipynb` in Google Colab.
2. Make sure the Excel file path is correct.
3. Run the cells from top to bottom.
4. Check the output after each cleaning step.

## 👩‍💻 Author
Day 3 Python & Pandas Practice
