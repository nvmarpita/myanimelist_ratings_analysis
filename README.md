# myanimelist_ratings_analysis👩‍💻
## Overview: 
Sourced from MyAnimeList — the go-to hub for anime fans and one of the richest community-driven databases in the space — this dataset captures the full personality of each title: how it's identified, what it's about, who made it, how audiences rated and embraced it, and when it aired. It's less a spreadsheet and more a snapshot of anime as both art and cultural phenomenon.

## 📁 Dataset:
- 🔗 source: https://www.kaggle.com/datasets/dbdmobile/myanimelist-dataset
- size: the dataset contains 24 fields and 24905 entries

## 🔧Tools used:
- Python pandas: cleaning and preprocessing
- MySQL workbench: analysis & insights
- Tableau: interactive dashboard visualization

## 🧹Data Cleaning:
- Created a working copy of the raw dataset `(df_copy)` to preserve the original
-  Performed initial inspection/ overview about the data with-
 `.describe()`,
 `.info()`,
 `.shape()`,
 `.head()`,
 `.tail()`,
 `.duplicated()`,
  and `.isnull()`,
- A few numeric columns(eg.`Socre`,`Rank`) had their data type as str instead of float/int. This was fixed by using `pd.to_numeric`, many column had "UNKNOWN" str instead of nulls/NaN which was handled with help of `np.na` and `.fillna`
- `Duration` was cleaned and converted mixed units into mintues by using functions like- findall(), conditional function for better Analysis.
- Addressed the `English name` column, where ~58% of values were `"UNKNOWN"` rather than true nulls, by imputing with the corresponding Name value using `.replace()`


