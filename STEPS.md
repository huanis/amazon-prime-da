### 1. Question formulation
1. What are the top 5 most common genre for movies and TV shows released on year 2017-2021?
2. Are there any correlation between content rating and common movie genre for movies released 2021?
3. Who are the main target audience for movies and TV shows released on year 2017-2021?

Dropped questions:
1. Which pair of director and cast are most frequently working in the same show?
2. Top 5 most casted people in horror movies of the year 2017-2021?

### 2. Data Exploration and Processing
Using **Google Spreadsheet**:
1. There are no duplicate rows found
2. Extract the integer values of `duration` into `duration_int`
3. Found data inconsistencies in column `rating`:
   - replace `AGES_16_` to `16+`
   - replace `AGES_18_` to `18+`
   - replace `ALL`, `ALL_AGES` to `G`
   - replace `UNRATED`, `NOT_RATE`, `TV-NR` to `NR`
4. Resulting dataset: **intermediate.csv** (9297 data rows)
5. Missing data are found in columns:
   - `director`: 2082 rows (21.53%)
   - `cast`: 1233 rows (12.75%)
   - `country`: 8996 rows (93.05%) -> **drop column**
   - `date added`: 9513 rows (98.40%) -> **drop column**
   - `rating`: 337 (3.49%) -> **immediate drop rows**
6. Found 16 rows with integer values in `director` column -> **immediate drop rows**
7. Found 14 rows with integer values in `cast` column -> **immediate drop rows**
8. Found 5 rows with integer values in `description` column -> **immediate drop rows**
9. For `type` Movie, we focus on feature films.
   - Drop rows with `duration_int` value less than 40 (cut off short films, test objects, and music videos)
   - Drop rows with `duration_int` value greater than 210 (most of them are something along the line of "X hours of [adjective] sounds")
10. Resulting dataset: **processed.csv** (9297 data rows)

Using **Google Colaboratory**
1. Check `duration_int` for outliers using Q1, Q3, LUB, RUB, MIN, MAX
   - Note: must first separate by `type`
2. Handle `duration_int` outliers:
   - For `Movie`: drop rows where `duration_int` is less than 40 or greater than 210
3. Resulting dataset: **processed.csv**
4. Split `listed_in` into multiple genre columns
5. Split `cast` into multiple cast columns
6. cast_count: how many casts are in shows
   - Q1: 1.0
   - Q3: 5.0
   - LUB: -5.0
   - RUB: 11.0
   - Max: 76
7. Drop cast columns after the 11th cast (RUB)
8. Create dataset **df_genre.csv** with the following attributes:
   - `show_id`
   - `type`
   - `release_date`
   - `genre` (only 1 column)
   - `duration` (from `duration_int`)
   - `rating`
9. Create dataset **df_cast.csv** with the following attributes:
   - `show_id`
   - `type`
   - `cast` (only 1 column)
   - `director`
   - `listed_in`
