# Day 2 — Selecting, Filtering & Sorting

## What I practiced
- Selecting a single column (`data['Customer_Age']`) → returns a Series
- Selecting multiple columns (`data[['Age_Group','Claim_Status']]`) → returns a DataFrame
- Row selection with `loc[]` (label-based, inclusive of end label)
- Row selection with `iloc[]` (position-based, exclusive of end position)
- Selecting rows *and* columns together with `loc[]` / `iloc[]`
- Filtering with numerical conditions (e.g. `data['Premium'] < 110`)
- Filtering with categorical conditions (e.g. `data['Policy_Type'] == "Travel"`)
- Filtering multiple categories with `.isin()`
- Combining conditions with `&` (AND)
- Sorting with `.sort_values()`, ascending/descending, and by multiple columns

## Key takeaway
`loc[]` uses labels and includes the end label; `iloc[]` uses integer
positions and excludes the end position.

## Dataset
See [`Dataset/`](./Dataset) — same insurance analytics data as Day 1.

## Screenshots
See [`Screenshots/`](./Screenshots) for output snapshots from this session.
