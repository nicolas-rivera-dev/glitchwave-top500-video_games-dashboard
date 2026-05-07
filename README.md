# glitchwave-top500-video_games-dashboard

# Video Games Dashboard — Dataset Documentation

**Top 500 Best Reviewed Video Games of All Time**  
Source: [Glitchwave.com](https://glitchwave.com) · Collected as of April 21, 2026

---

## Dataset Overview

| Property | Value |
|---|---|
| File | `Dataset_Video_Games_Complete.xlsx` |
| Rows | 500 |
| Columns | 9 |
| Year Range | 1986 – 2026 |
| Null Values | None |
| Avg. Rating | 4.02 ★ |

---

## Column Reference

| Column | Type | Description | Example |
|---|---|---|---|
| `Ranking` | Integer | Position in the Top 500 list (1 = highest rated) | `1` |
| `Game` | Text | Full official title of the game | `Disco Elysium` |
| `Release Year` | Integer | Year the game was first released | `2019` |
| `Franchise` | Text | Series or franchise the game belongs to (if any) | `Silent Hill` |
| `Developer` | Text | Studio that developed the game | `ZA/UM` |
| `Publisher` | Text | Company that published the game | `ZA/UM` |
| `Platform` | Text | Platform(s) where the game is available | `Multi` |
| `Genre` | Text | Primary genre classification | `RPG` |
| `Rating` | Float | Average community rating (scale 1.00–5.00) | `4.54` |

---

## Key Statistics

### Rating Distribution
| Metric | Value |
|---|---|
| Minimum | 3.78 |
| 25th Percentile | 3.91 |
| Median | 3.99 |
| 75th Percentile | 4.10 |
| Maximum | 4.56 |
| Std. Deviation | 0.14 |

### Top 5 Highest Rated Games
| Ranking | Game | Developer | Platform | Rating |
|---|---|---|---|---|
| 1 | Silent Hill 2 | Team Silent | PS2 / PC | 4.56 |
| 2 | Disco Elysium | ZA/UM | Multi | 4.54 |
| 3 | Bloodborne | FromSoftware | PS4 | 4.52 |
| 4 | Mother 3 | HAL Laboratory | Game Boy Advance | 4.50 |
| 5 | Metal Gear Solid 3: Snake Eater | Konami | PS2 / Multi | 4.48 |

### Genre Distribution (Top 10)
| Genre | Count |
|---|---|
| RPG | 72 |
| Platformer | 44 |
| Adventure | 38 |
| Action-Adventure | 38 |
| First-Person Shooter | 33 |
| Visual Novel | 22 |
| Action RPG | 23 |
| Fighting | 23 |
| Strategy | 20 |
| Action | 19 |

### Platform Distribution (Top 10)
| Platform | Count |
|---|---|
| Multi | 122 |
| PC | 89 |
| PC / Multi | 35 |
| PS2 | 17 |
| Nintendo DS | 15 |
| PS1 | 15 |
| Arcade / Multi | 13 |
| PS2 / Multi | 13 |
| Game Boy Advance | 11 |
| SNES / Multi | 11 |

### Most Represented Developers
| Developer | Games in Top 500 |
|---|---|
| FromSoftware | Multiple |
| Nintendo | Multiple |
| Konami | Multiple |
| Capcom | Multiple |
| HAL Laboratory | Multiple |

> Total unique developers: **251**

---

## Dashboard Visualizations Built From This Dataset

| Visual | Fields Used |
|---|---|
| KPI — Total Games | `Ranking` (COUNT) |
| KPI — Total Platforms | `Platform` (DISTINCTCOUNT) |
| KPI — Total Developers | `Developer` (DISTINCTCOUNT) |
| KPI — Average Rating | `Rating` (AVERAGE) |
| Bar chart — Games by platform | `Platform`, COUNT |
| Line chart — Games by year | `Release Year`, COUNT |
| Treemap — Franchises | `Franchise`, COUNT |
| Bar chart — Games by decade | `Decade` (calculated), COUNT |
| Ranking table | All columns |

**Slicers/Filters:**
- Genre
- Platform
- Release Year (range slider)
- Rating (range slider)
- Franchise

---

## DAX Measures Used

```dax
Total Games = COUNTROWS(VideoGames)

Total Platforms = DISTINCTCOUNT(VideoGames[Platform])

Total Developers = DISTINCTCOUNT(VideoGames[Developer])

Average Rating = AVERAGE(VideoGames[Rating])

Decade = LEFT(VideoGames[Release Year], 3) & "0s"
```

---

## Data Quality Notes

- No null values across any column
- Platform field uses a consolidated taxonomy (e.g., `Multi` for multiplatform titles)
- Franchise field contains `None` or `N/A` for standalone games with no series affiliation
- Some games appear under multiple platforms formatted as `PS2 / Multi`
- Rating scale: 1.00 to 5.00, community-weighted average
- Data reflects rankings as of **April 21, 2026** — positions may have shifted since collection
