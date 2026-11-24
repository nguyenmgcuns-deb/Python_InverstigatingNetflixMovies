# Investigating Netflix Movies

An exploratory data analysis (EDA) project from DataCamp, using **pandas** and **matplotlib** to look at Netflix movies released in the **1990s**.

## Questions

1. What was the most frequent movie duration in the 1990s?
2. How many short (under 90 minutes) action movies were released in the 1990s?

## Data

`netflix_data.csv` contains one row per Netflix show, with these columns:

| Column | Description |
|---|---|
| `show_id` | ID of the show |
| `type` | Movie or TV Show |
| `title` | Title |
| `director` | Director |
| `cast` | Cast |
| `country` | Country of origin |
| `date_added` | Date added to Netflix |
| `release_year` | Release year |
| `duration` | Duration in minutes |
| `description` | Description |
| `genre` | Genre |

## Approach

1. **Explore the data** with `.head()` and `.info()`. `release_year` and `duration` are integers, and no values are missing.
2. **Filter** to movies released from 1990 to 1999, combining boolean conditions with `&`:
   ```python
   netflix_subset = netflix_df[(netflix_df["type"] == "Movie") &
                               (netflix_df["release_year"] >= 1990) &
                               (netflix_df["release_year"] < 2000)]
   ```
3. **Most frequent duration (the mode)**, using `value_counts()`, which sorts from most to least common. The answer is the first index label. A histogram was used to check the result visually.
4. **Short action movies**: loop over the rows with `iterrows()` and count the movies where `duration < 90` and `genre == "Action"`.

## Results

| Question | Answer |
|---|---|
| 1990s movies in the dataset | 183 |
| Most frequent duration (`duration`) | **94 minutes** |
| Short action movies (`short_movie_count`) | **7** |

## What I learned

- Use `&` (not `and`) to combine conditions on pandas Series, and put each condition in brackets.
- A decade needs a start **and** an end condition (`>= 1990` and `< 2000`).
- `.sum()`, `.count()`, `.mean()` and `.mode()` answer different questions. "Most frequent" means mode.
- `value_counts().index[0]` gives the most common value, and `.values[0]` gives how often it appears.

## Files

- `notebook.ipynb`: the analysis notebook
- `netflix_data.csv`: the dataset
- `redpopcorn.jpg`: the project cover image

## How to run

```bash
pip install pandas matplotlib jupyter
jupyter notebook notebook.ipynb
```
