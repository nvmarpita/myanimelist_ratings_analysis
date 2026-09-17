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
Unlike [Olist/Startup Funding], which focused on [SQL-based trend/aggregation analysis], this project uses CORRELATION AND REGRESSION to test specific hypotheses about what drives an anime's reception moving from describing the data to explaining
relationships within it


❔ Question: Does Episode count correlate with Score? 

Hypothesis: I expect little to no correlation between Episodes and Score, because it depends more on the plot and story quality of the
anime than on how many episodes it has.


Method: Pearson correlation via.corr()


Result: r = 0.08 


Interpretation: The correlation is very close to zero, indicating a negligible relationship between Episodes and Score -neither meaningfully
positive nor negative. This supports my hypothesis: episode count doesn't have a strong effect on how an anime is rated


❔ Question: Does Duration_minutes correlate with Score?


Hypothesis: i'm not expecting any correlation between duration and score as short duration movie title has also been hit mostly.


Method: Pearson correlation via.corr()


Result: r = 0.31


Interpretation: The correlation (r = 0.31) is weak but not negligible, suggesting a slight positive relationship between duration and score - longer anime tend to score marginally higher on average. This partially contradicts my hypothesis; but duration alone cant strongly predict quality

❔Question: Do certain genres have a higher average Score than others?

Hypothesis: i think yes few genre such as 'Slice of Life', 'Suspense',could have more score than other genres as it is one of the popular and loved genre

Method: Group comparison (mean per genre, via loop)

Result: 6.38 overall average

**(top_scorers)**:
`Award Winning`, (7.29),
 `Mystery`, (6.99),
 `Suspense`, (6.96),
 **(bottom_scorers)**:
 `Erotica`, (6.12),
 `Hentai`, (6.06),
 `Avant Garde`, (5.14)

Interpretation: here `Award Winning` at (7.29) tops from other genre  but this reflects prior recognition rather than genre content, so it's not treated as a meaningful genre-level finding. `Mystery` at (6.99),and `Suspense` at (6.96) are actual genre  hits over other genre, my hypothesis about `Slice of Life` 6.47 was wrong it ranks 16 out of 21, in overall average but `Suspense` ranks third top making my half hypothesis true.

❔Question: 


