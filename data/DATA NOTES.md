## Data Sources & Collection Notes

### Source

- **Website:** [Glitchwave.com](https://glitchwave.com/charts/top/game/all-time/)
- **Snapshot date:** May 21, 2026
- **Collection method:** Manual — data was hand-collected directly from the website (no scraping tools were used)

### Dataset File

`Dataset_Video_Games_Complete.xlsx` — 500 rows, 9 columns

### Enrichment Process

The following columns were collected **manually** from Glitchwave.com:

| Column | Method |
|---|---|
| `Ranking` | Manually collected from Glitchwave.com |
| `Game` | Manually collected from Glitchwave.com |
| `Release Year` | Manually collected from Glitchwave.com |
| `Franchise` | Manually collected from Glitchwave.com |
| `Developer` | Manually collected from Glitchwave.com |
| `Publisher` | Manually collected from Glitchwave.com |
| `Platform` | Manually collected from Glitchwave.com |
| `Genre` | Manually collected from Glitchwave.com |
| `Rating` | Manually collected from Glitchwave.com |

The following columns were **added during enrichment**:

| Column | Method |
|---|---|
| `Platform (Main)` | DAX computed column — extracts the primary platform from multi-platform entries (e.g. `"PS2 / Multi"` → `"PS2"`) for cleaner visual grouping |
| `Decade` | DAX computed column derived from `Release Year`, used for decade-level aggregations in the dashboard |

### Important Notes

- Rankings reflect community-weighted averages as of **May 21, 2026** and may have changed since collection
- Glitchwave uses a **weighted scoring system** (similar to Bayesian averaging) rather than a simple arithmetic mean — a game with more ratings will rank higher than one with a higher raw average but fewer votes. This explains, for example, why **Disco Elysium** (4.54 avg · 5,385 ratings) ranks #1 over **Silent Hill 2** (4.56 avg · 4,493 ratings)
- Games released in 2025–2026 are included when they had already appeared on the Glitchwave chart at the time of data collection
- Franchise values marked as `Standalone` indicate games with no sequel, prequel, or shared universe entry in the Top 500
- This dataset is intended for educational and portfolio purposes only
