# Amazon Prime Dataset Analysis
## Dataset
Link: https://www.kaggle.com/datasets/shivamb/amazon-prime-movies-and-tv-shows
## Tools
- Google Spreadsheet
- Google Colaboratory
- Google Data Studio (Looker Studio)
## Dashboard
## Steps
1. Question identification
2. Data exploration and processing
3. Data visualization
### Steps: Question identification
1. What are the top 5 most common genres for movies and TV shows released on year 2017-2020?
2. Who are the top 10 people most frequently casted for horror movies released on year 2017-2020?
3. Who are the main target audience for movies and TV shows released on year 2017-2020?
4. Are there any correlation between content rating and genre for movies?
### Steps: Data exploration
Using Google Spreadsheet:
1. There are no duplicate rows found
2. Missing data are found in columns:
  - `director`: 21.53%
  - `cast`: 12.75%
  - `country`: 93.05% (drop column)
  - `date added`: 98.40% (drop column)
  - `rating`: 3.49% (drop rows)
3. Found data inconsistency in column `rating`:
  - replace `AGES_16_` to `16+`
  - replace `AGES_18_` to `18+`
  - replace `ALL`, `ALL_AGES` to `G`
  - replace `UNRATED`, `NOT_RATE`, `TV-NR` to `NR`
4. Found rows with integer values in `director` column (drop rows)
5. Found rows with integer values in `cast` column (drop rows)
6. Found rows with integer values in `description` column (drop rows)
7. Extract the integer values of `duration` column into `duration_int` column
