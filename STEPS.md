### 1. Question formulation
1. Genre trend for movies released from the year 2017 to 2021?
2. Are there any genre caracteristics based on content rating for movies released on 2021?
3. Who are the main target audience for movies and TV shows released on year 2021?
4. Which pair of director and cast are most frequently working in the same show?
5. Are there anyone who had been casted in both movies and TV shows from the year 2017 to 2021?

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
   - Drop all 521 rows with `duration_int` value less than 40 (cut off short films, test objects, and music videos)
   - Drop all 29 rows with `duration_int` value greater than 210 (most of them are something along the line of "X hours of [adjective] sounds")
10. Resulting dataset: **processed.csv** (8746 data rows, excluding header)

Using **Google Colaboratory**:
1. Resulting dataset: **processed.csv**
2. Split `listed_in` into multiple genre columns
3. Split `cast` into multiple cast columns
4. cast_count: how many casts are in shows
   - Q1: 2.0
   - Q3: 6.0
   - LUB: -6.0
   - RUB: 12.0
   - Max: 76
5. Drop cast columns after the 11th cast (RUB)
6. Create dataset **df_genre.csv** with the following attributes:
   - `show_id`
   - `genre` (only 1 column)
7. Create dataset **df_cast.csv** with the following attributes:
   - `show_id`
   - `cast` (only 1 column)
  
Using **Google Spreadsheet**:
1. Main dataset preparation for Google Data Studio (Looker)
   - Drop columns `description` and `cast` from **processing.csv**
   - Resulting dataset: **final.csv**
2. Drop index column in **df_genre.csv** and **df_cast** which is a residue from Google Colaboratory processes
3. Create a new csv file **rating_category.csv** that contains 2 columns:
   - `id`: Primary key of the row
   - `category`: Has 3 unique values (-, kids, teens, and adults)
4. Create a new csv file **movie_rating.csv** that contains 2 columns:
   - `rating`: Has 11 unique values, which are all the movie ratings in **processed.csv**
   - `category_id`: To connect this csv to **rating_category.csv** (mutually exclusive)

### 3. Data Visualization
