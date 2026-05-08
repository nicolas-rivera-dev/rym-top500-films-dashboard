# rym-top500-films-dashboard

# Movies Dashboard — Dataset Documentation

**Top 500 Best Reviewed Films of All Time**  
Source: [RateYourMusic.com](https://rateyourmusic.com) · Collected as of April 21, 2026

---

## Dataset Overview

| Property | Value |
|---|---|
| File | `Dataset_Movies_Complete.xlsx` |
| Rows | 500 |
| Columns | 9 |
| Year Range | 1919 – 2025 |
| Null Values | None |
| Avg. Rating | 3.97 ★ |

---

## Column Reference

| Column | Type | Description | Example |
|---|---|---|---|
| `Position Ranking` | Integer | Position in the Top 500 list (1 = highest rated) | `1` |
| `Title` | Text | Full official film title | `Harakiri` |
| `Director` | Text | Film's director(s) | `Masaki Kobayashi` |
| `Release Year` | Integer | Year the film was released | `1962` |
| `Decade` | Text | Decade of release (pre-aggregated) | `1960s` |
| `Country of origin` | Text | Country or countries of production | `Japan` |
| `Language` | Text | Primary language(s) of the film | `Japanese` |
| `Genres` | Text | Genre classification (may be compound) | `Drama` |
| `Average rating` | Float | Average community rating (scale 1.00–5.00) | `4.41` |

---

## Key Statistics

### Rating Distribution
| Metric | Value |
|---|---|
| Minimum | 3.80 |
| 25th Percentile | 3.89 |
| Median | 3.94 |
| 75th Percentile | 4.03 |
| Maximum | 4.41 |
| Std. Deviation | 0.12 |

### Top 5 Highest Rated Films
| Rank | Title | Director | Year | Country | Rating |
|---|---|---|---|---|---|
| 1 | Harakiri | Masaki Kobayashi | 1962 | Japan | 4.41 |
| 2 | Come and See | Elem Klimov | 1985 | USSR / Belarus | 4.38 |
| 3 | 2001: A Space Odyssey | Stanley Kubrick | 1968 | USA / UK | 4.36 |
| 4 | The End of Evangelion | Hideaki Anno | 1997 | Japan | 4.35 |
| 5 | The Good, the Bad and the Ugly | Sergio Leone | 1966 | Italy | 4.35 |

### Genre Distribution (Top 10)
| Genre | Count |
|---|---|
| Drama | 60 |
| Documentary | 18 |
| War, Drama | 11 |
| Documentary, Music, Concert Film | 9 |
| Drama, Historical | 9 |
| Drama, Romance | 9 |
| Crime, Thriller, Drama | 6 |
| Drama, Neorealism | 6 |
| Animation, Science Fiction, Drama | 5 |
| Western | 5 |

### Decade Distribution
| Decade | Films |
|---|---|
| 1910s | 1 |
| 1920s | 15 |
| 1930s | 8 |
| 1940s | 26 |
| 1950s | 59 |
| 1960s | 74 |
| 1970s | 83 |
| 1980s | 70 |
| 1990s | 71 |
| 2000s | 50 |
| 2010s | 29 |
| 2020s | 14 |

### Directors with Most Films in the Top 500
| Director | Films |
|---|---|
| Akira Kurosawa | 10 |
| Ingmar Bergman | 9 |
| David Lynch | 8 |
| Stanley Kubrick | 8 |
| Martin Scorsese | 7 |

### Geographic Scope
- **Total unique countries:** 37
- **Total unique languages:** 38
- Most represented: USA (120), Japan (70), France (43), UK (30), Italy (27)

---

## Dashboard Visualizations Built From This Dataset

| Visual | Fields Used |
|---|---|
| KPI — Total Films | `Title` (COUNT) |
| KPI — Total Directors | `Director` (DISTINCTCOUNT) |
| KPI — Total Countries | `Country (Modern)` (DISTINCTCOUNT) |
| KPI — Average Rating | `Average rating` (AVERAGE) |
| Bar chart — Films by country | `Country (Modern)`, COUNT |
| Bar chart — Films by decade | `Decade`, COUNT |
| Bar chart — Films by director | `Director`, COUNT |
| Bar chart — Films by genre | `Genres`, COUNT |
| Ranking table | `Ranking`, `Title`, `Director`, `Country`, `Genres`, `Rating` |

**Slicers/Filters:**
- Director
- Country
- Decade
- Genres
- Language

---

## DAX Measures Used

```dax
Total Films = COUNTROWS(Movies)

Total Directors = DISTINCTCOUNT(Movies[Director])

Total Countries = DISTINCTCOUNT(Movies[Country of origin])

Average Rating = AVERAGE(Movies[Average rating])

Films by Decade = 
CALCULATE(
    COUNTROWS(Movies),
    ALLEXCEPT(Movies, Movies[Decade])
)

Top Director by Count = 
FIRSTNONBLANK(
    TOPN(1, ALL(Movies[Director]), CALCULATE(COUNTROWS(Movies))),
    1
)
```

---

## Data Quality Notes

- No null values across any column
- `Country of origin` may contain multiple countries separated by `/` for co-productions (e.g., `USA / Germany / Japan`)
- `Genres` field may contain compound genre strings (e.g., `War, Drama`) — these are stored as-is and split during Power Query transformation for the genre chart
- `Decade` was pre-calculated during data preparation, following the format `1910s`, `1920s`, etc.
- The 1919 entry represents the oldest film in the dataset
- Language field reflects the primary spoken language — multilingual films show the dominant language
- Rankings reflect community-weighted averages as of **April 21, 2026** and may have shifted since collection
