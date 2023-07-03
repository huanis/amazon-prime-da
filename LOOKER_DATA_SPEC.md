## Data Sources
### CSV files:
- df_cast.csv
- df_genre.csv
- final.csv
- movie_rating.csv
- rating_category.csv

## Blended Data
### **cast-main** spesifications:
- Tables:
  - Cast: df_cast.csv (no filter)
  - Main: final.csv (no filter)
- Relation: Cast `INNER JOIN` Main
  - Cast (show_id) - Main (show_id)
- Dimensions:
  - show_id
  - cast
  - director
  - listed_in
  - rating
  - type
  - release_year
- Metrics:
  - Record Count

### **cast-show** spesifications:
- Tables:
  - Cast 1: df_cast.csv (no filter)
  - Movie: final.csv (type = Movie, release_year >= 2000)
  - Cast 2: df_cast.csv (no filter)
  - TV Show: final.csv (type = TV Show, release_year >= 2000)
- Relation: Cast 1 `INNER JOIN` Movie `INNER JOIN` Cast 2 `INNER JOIN` TV Show
  - Cast 1 (show_id) - Movie (show_id)
  - Cast 1 (cast) - Cast 2 (cast)
  - Cast 2 (show_id) - TV Show (show_id)
- Dimensions:
  - show_id (Cast 1)
  - show_id (Cast 2)
  - cast
  - type (Movie)
  - type (TV Show)
  - release_year (Movie)
  - release_year (TV Show)
- Metrics:
  - Record Count

### **genre-main** specifications:
- Tables:
  - Genre: df_genre.csv (no filter)
  - Main: final.csv (no filter)
- Relation: Genre `INNER JOIN` Main
  - Genre (show_id) - Main (show_id)
- Dimensions:
  - show_id
  - genre
  - rating
  - type
  - release_year
- Metrics:
  - Record Count

### **movie-rating-genre-2021** specifications:
- Tables:
  - Main: final.csv (type = Movie `AND` release_year = 2021 `AND` rating != NR)
  - Rating Relation: movie_rating.csv (no filter)
  - Rating Category: rating_category.csv (no filter)
  - Genre: df_genre.csv (no filter)
- Relation: Main `INNER JOIN` Rating Relation `INNER JOIN` Rating Category `INNER JOIN` Genre
  - Main (rating) - Rating Relation (rating)
  - Rating Relation (category_id) - Rating Category (id)
  - Main (show_id) - Genre (show_id)
- Dimensions:
  - show_id
  - rating
  - category
  - genre
  - release_year
  - type
  - category_id
- Metrics: None

## Filters
### **cast-main**:
- **director-cast filter** specification:
  - EXCLUDE `director` == (literal blank/missing value)
  - INCLUDE `type` = Movie
  - INCLUDE `release_year` >= 2000

### **genre-main**:
- **move (genre-main)** specification:
  - INCLUDE `type` = Movie
- **2017-2021 (genre-main)** specification:
  - INCLUDE `release_year` >= 2021
- **exclude-genre (genre-main)** specification:
  - EXCLUDE `genre` == Special Interest
 
### **movie-rating-genre-2021**:
- **kids (movie-rating)** specification:
  - INCLUDE `category` = kids
- **teens (movie-rating)** specification:
  - INCLUDE `category` = teens
- **adults (movie-rating)** specification:
  - INCLUDE `category` = adults
 

