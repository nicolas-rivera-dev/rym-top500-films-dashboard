## 📋 Data Sources & Collection Notes

### Source
- **Website:** [RateYourMusic.com](https://rateyourmusic.com/charts/top/film/all-time/separate:live,archival,soundtrack/)
- **Snapshot date:** April 21, 2026
- **Collection method:** Manual — data was hand-collected
  directly from the website (no scraping tools were used)

### Dataset File
`Dataset_Films_Complete.xlsx` — 500 rows, 9 columns

### Enrichment Process

The following columns were collected **manually** from RateYourMusic.com:

| Column | Method |
|---|---|
| `Position Ranking` | Manually collected from RateYourMusic.com |
| `Title` | Manually collected from RateYourMusic.com |
| `Director` | Manually collected from RateYourMusic.com |
| `Release Year` | Manually collected from RateYourMusic.com |
| `Country of origin` | Manually collected from RateYourMusic.com |
| `Genres` | Manually collected from RateYourMusic.com |
| `Average rating` | Manually collected from RateYourMusic.com |

The following columns were **added during enrichment**:

| Column | Method |
|---|---|
| `Decade` | AI-assisted generation based on Release Year, manually reviewed |
| `Language` | AI-assisted generation based on Country of origin and Title, manually reviewed |
| `Country (Modern)` | DAX Measure made from Country of origin, to fill countries that no longer exist from RateYourMusic.com |

### Important Notes
- Rankings reflect community-weighted averages as of **April 21, 2026**
  and may have changed since collection
- RateYourMusic uses a **Bayesian weighted average** rather than a simple
  arithmetic mean — a film with more ratings will rank higher than one with
  a higher raw average but fewer votes. This is consistent with the ranking
  methodology used by platforms such as IMDb
- RateYourMusic.com does not allow scraping per their Terms of Service;
  all data was collected manually in compliance with their policies
- This dataset is intended for educational and portfolio purposes only
