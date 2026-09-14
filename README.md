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
- A few numeric columns(eg.`Score`,`Rank`) had their data type as str instead of float/int. This was fixed by using `pd.to_numeric`, many column had "UNKNOWN" str instead of nulls/NaN which was handled with help of `np.nan` and `.fillna`
- `Duration` was cleaned and converted mixed units into minute by using functions like- used a custom function (duration_to_minute()) with re.findall() to parse the mixed hr/min/sec text into a single minutes value for better Analysis. `Duration_minute` was created as a new column in the dataset.
- Addressed the `English name` column, where ~58% of values were `"UNKNOWN"` rather than true nulls, by imputing with the corresponding `Name` value using `.fillna(df['Name'])`
- `Aired` was stored as text instead of datetime, which was fixed with `pd.to_datetime` and few end-date had '?' as they were still being aired, handled by replacing with NaN. the column was split into as `Aired_start` and `Aired_end` for better analysis and view
-  Genres stored multiple values in one text field (e.g. `"Action, Adventure, Fantasy")`, which isn't useable for filtering, grouping, or analysis directly. Used `get_dummies()` to one-hot encode it into one boolean column per genre (~20 new columns total, e.g. `Action`, `Comedy`, `Drama`). Each column holds 1 if the anime belongs to that genre and 0 if it doesn't and since an anime can belong to multiple genres at once, a single row can have several 1s across different genre columns. Eg: Cowboy Bebop has Action = 1 and Sci-Fi = 1 simultaneously, reflecting that it belongs to both genres.
## Data Analysis:

