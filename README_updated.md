# Python Learning Days

A day-by-day log of my Python + pandas practice, working through an insurance
data analytics dataset.

## Structure

```
python-learning-days/
│
├── Day1/     → Loading data, first look (head/tail/shape/info/describe)
├── Day2/     → Selecting, filtering, and sorting data with pandas
├── Day3/     → Cleaning and standardizing data with pandas
└── DayN/     → Future daily pandas practice
```

Each `DayN/` folder contains:
- `DayN.ipynb` — the practice notebook for that day
- `README.md` — a short summary of what was covered that day
- `Screenshots/` — screenshots of the code/output, with their own `README.md` explaining each one

(Add your own `Dataset/` folder if you want to keep the data alongside the notebook.)

## Days

| Day | Topics |
|-----|--------|
| [Day 1](./Day1/README.md) | Reading an Excel file with pandas, `head()`, `tail()`, `shape`, `info()`, `describe()`, `columns`, `dtypes` |
| [Day 2](./Day2/README.md) | Column selection, `loc[]` vs `iloc[]`, filtering (numeric, categorical, multi-condition), `isin()`, `sort_values()` |
| [Day 3](./Day3/README.md) | Data cleaning and standardization, including fixing inconsistent values with `replace()` |
| Day N | Future Python + pandas practice topics |

## Setup

```bash
pip install pandas openpyxl jupyter
jupyter notebook
```
