# Top 500 Video Games Dashboard — Power BI

An interactive Power BI dashboard built around the **Top 500 best user-rated video games of all time** sourced from [Glitchwave](https://glitchwave.com/charts/top/game/all-time/). The project covers data collection, cleaning, modeling, and visualization — all in a single-page interactive report.

---

## Project Overview

| Detail | Info |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **Data Source** | [Glitchwave — All-Time Top Games](https://glitchwave.com/charts/top/game/all-time/) |
| **Dataset** | 500 games · 9 columns |
| **Rating Range** | 3.78 – 4.56 |
| **Year Span** | 1986 – 2026 |
| **Dashboard Pages** | 1 (single-page layout) |

---

## Dashboard Preview

> Open the `.pbix` file in Power BI Desktop to interact with all slicers and filters.

### Visuals Included

| Visual | Description |
|---|---|
| **KPI Cards (×5)** | Total Games, Total Platforms, Total Developers, Average Rating and Top-Ranking Game — all reactive to active filters |
| **Clustered Bar Chart** | Number of games per main platform |
| **Area Chart** | Game releases distributed across years (1986–2026) |
| **Treemap** | Franchises with the most titles featured in the Top 500 |
| **Bar Chart** | Game count grouped by decade (1980s through 2020s) |
| **Detail Table** | Full game list with Ranking, Game, Platform, Genre, Developer, and Rating |
| **Slicers (×5)** | Filter by Genre, Platform, Franchise, Release Year range and Rating range |

---

## Dataset Structure

**File:** `Dataset_Video_Games_Complete.xlsx`  
**Sheet:** `Video Games`

| Column | Type | Description |
|---|---|---|
| `Ranking` | Integer | Position in the Top 500 (1 = best) |
| `Game` | Text | Game title |
| `Release Year` | Integer | Original release year |
| `Franchise` | Text | Franchise or `Standalone` if independent |
| `Developer` | Text | Development studio |
| `Publisher` | Text | Publishing company |
| `Platform` | Text | Platform(s) the game was released on |
| `Genre` | Text | Primary genre classification |
| `Rating` | Decimal | Average user rating on Glitchwave (scale ~3.78–4.56) |

> **Note:** A computed column `Platform (Main)` was created in Power BI to extract the primary platform from multi-platform entries (e.g., `"PS2 / Multi"` → `"PS2"`), enabling cleaner platform-level aggregations.

---

## Key Insights from the Data

### Top Games
| Rank | Game | Rating | Genre |
|---|---|---|---|
| 1 | Disco Elysium | 4.54 | RPG |
| 2 | Silent Hill 2 | 4.56 | Survival Horror |
| 3 | Bloodborne | 4.52 | Action RPG |
| 4 | Mother 3 | 4.50 | RPG |
| 5 | Metal Gear Solid 3: Snake Eater | 4.48 | Stealth |

> Silent Hill 2 holds the **highest raw rating (4.56)** in the dataset despite being ranked #2 overall by Glitchwave's weighted scoring system.
> Why is Silent Hill 2 ranked #2 despite having a higher raw rating (4.56 vs 4.54)?
Glitchwave uses a weighted scoring system — similar to Bayesian averaging — that factors in the number of ratings, not just the average. Disco Elysium has 5,385 ratings vs Silent Hill 2's 4,493, giving it more statistical confidence and a higher weighted position on the chart.

### Genre Distribution (Top 10)
| Genre | Games |
|---|---|
| RPG | 72 |
| Platformer | 44 |
| Adventure | 38 |
| Action-Adventure | 38 |
| First-Person Shooter | 33 |
| Action RPG | 23 |
| Fighting | 23 |
| Visual Novel | 22 |
| Strategy | 20 |
| Action | 19 |

### Platform Breakdown
Multi-platform releases dominate the list (122 games), followed by PC exclusives (89). Among dedicated platforms, **PS2** (17), **Nintendo DS** (15), and **PS1** (15) are the most represented.

### Top Developers
| Developer | Games in Top 500 |
|---|---|
| Nintendo | 37 |
| Capcom | 24 |
| Atlus | 11 |
| HAL Laboratory | 8 |
| Konami | 8 |
| Game Freak | 8 |
| Square | 9 |

### Games by Decade
| Decade | Count |
|---|---|
| 1980s | 3 |
| 1990s | 93 |
| 2000s | 192 |
| 2010s | 130 |
| 2020s | 82 |

The **2000s** is by far the most represented decade, accounting for 38% of the entire Top 500.

### Top Franchises (by entries in Top 500)
Pokémon, Zelda, and Mario each have **9–8 entries**, while standalone titles (107 games) make up the largest group — showing that many of the most beloved games are unique, one-of-a-kind experiences.

---

## DAX Measures

The following custom DAX measure was created to power the dynamic KPI cards:

```DAX
-- Returns the name of the top-ranked game under the current filter context
Top Game =
VAR TopRank = MIN('Video Games'[Ranking])
RETURN
    CALCULATE(
        FIRSTNONBLANK('Video Games'[Game]; 1);
        'Video Games'[Ranking] = TopRank
    )
```

## How to Use

1. **Clone or download** this repository.
2. Open `Dashboard_Video_Games_Official.pbix` in **Power BI Desktop** (free download from [Microsoft](https://powerbi.microsoft.com/desktop/)).
3. The dataset is already embedded — no external connection needed.
4. Use the **slicers** on the left panel to filter by genre, year, platform, franchise, or rating range.
5. Hover over any chart for tooltips. Click a visual element to cross-filter the rest of the dashboard.

---

## Tools & Technologies

- **Microsoft Power BI Desktop** — data modeling, DAX, and report design
- **Microsoft Excel** — data structuring and storage
- **Glitchwave** — data source (user-rated game rankings)
- **DAX (Data Analysis Expressions)** — custom measures and computed columns

---

## Data Source

All game rankings and ratings were manually collected from:

> **Glitchwave — All-Time Top Games**  
> https://glitchwave.com/charts/top/game/all-time/

Glitchwave is a game cataloguing platform similar to RateYourMusic, where users rate and track the games they've played. The rankings reflect **weighted average user scores**, meaning a game's position is influenced by both its average rating and the number of votes it has received.

---

## Notes

- Games released in 2025–2026 are included when they had already appeared on the Glitchwave chart at the time of data collection. This includes early-access titles and highly anticipated releases.
- The `Platform` field reflects the original or most notable platform(s). The computed `Platform (Main)` column used in visualizations extracts only the first listed platform for cleaner grouping.
- Franchise values marked as `Standalone` indicate games with no sequel, prequel, or shared universe.

---

*Data collected and dashboard built by Nicolas Rivera. Part of a personal data analytics portfolio.*
