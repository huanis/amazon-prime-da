### Data Sources
CSV files:
- df_cast.csv
- df_genre.csv
- final.csv
- movie_rating.csv
- rating_category.csv

### Blended Data
**cast-main** spesifications:
- tables:
  - Cast: df_cast.csv (no filter)
  - Main: final.csv (no filter)
- relation: Cast `INNER JOIN` Main
  - Cast (show_id) - Main (show_id)
- dimensions:
  - show_id
  - cast
  - director
  - listed_in
  - rating
  - type
  - release_year
- metrics:
  - Record Count

**cast-show** spesifications:
- tables:
  - Cast 1: df_cast.csv (no filter)
  - Movie: final.csv (type: Movie only)
  - Cast 2: df_cast.csv (no filter)
  - TV Show: final.csv (type: TV Show only)
- relation: Cast 1 `INNER JOIN` Movie `INNER JOIN` Cast 2 `INNER JOIN` TV Show
  - Cast 1 (show_id) - Movie (show_id)
  - Cast 1 (cast) - Cast 2 (cast)
  - Cast 2 (show_id) - TV Show (show_id)
- dimensions:
  - show_id (Cast 1)
  - show_id (Cast 2)
  - cast
  - type (Movie)
  - type (TV Show)
  - release_year (Movie)
  - release_year (TV Show)
- metrics:
  - Record Count

**genre-main** specifications:

**movie-rating-genre-2021** specifications:
