# Steam Market Analysis

What makes a game succeed on Steam? This project analyzes 125,855 Steam games using three tools: **Excel** for data preparation, **Tableau** for a market overview dashboard, and **Power BI** for a genre analysis.

**Live Tableau dashboard:** [public.tableau.com/app/profile/jacob.turner3739](https://public.tableau.com/app/profile/jacob.turner3739)

## Key findings

- **Steam exploded after 2013.** Games with 10+ reviews grew from about 440 released in 2013 to 6,889 in 2024.
- **Success is extremely lopsided.** 60% of games have fewer than 20,000 owners. Only about 2% pass 1 million.
- **Mid-priced games are rated best.** Games listed at $10–$20 average 79.4% positive reviews; games at $40+ average the lowest, 72.2%.
- **The biggest genres are also well liked.** Indie is the largest genre (40,583 games), and Casual is the highest rated (78.0%). Massively Multiplayer is the clear outlier at 65.2%.

## Process

### 1. Excel: data preparation
- Started from a 125,855-row dataset of Steam games.
- Built 8 calculated fields with formulas:
  - **Total Reviews** and **Review Score** (share of positive reviews)
  - **List Price**: the dataset's price is the sale price on the day it was collected, so the formula reverses the discount: `Price / (1 - Discount / 100)`
  - **Owners Low / Owners High**: owner counts are stored as text ranges like "20000 - 50000", split into numbers
  - **Release Year** and **Price Band**
  - **Keep** flag: games with 10+ reviews, giving a 56,662-game analysis set
- Flagged rows instead of deleting them, so the original data stays intact and the cutoff can be changed.
- Built pivot tables to check the numbers before moving to other tools.

### 2. Tableau: market overview dashboard
- Games released per year
- Average review score by price band
- Number of games in each owner bracket

### 3. Power BI: genre analysis
- Used **Power Query** to split the multi-genre column into one row per genre (163,164 rows).
- Wrote **DAX** measures:
  - `Games = DISTINCTCOUNT(games[AppID])` counts each game once, even though it appears under several genres
  - `Avg Review Score = AVERAGEX(games, DIVIDE(games[Positive], games[Positive] + games[Negative]))`
- Charted the top 12 genres by number of games and by average review score.

## Limitations

- **Owner counts are estimates.** Steam doesn't publish sales, so owners come as ranges, not exact numbers.
- **Prices are a one-day snapshot.** Sale prices were converted back to list prices, but there's no record of what each buyer actually paid, so revenue can't be calculated.
- **2025 is incomplete.** Newer games haven't built up 10 reviews yet, so 2025 is left out of yearly trends.
- **Some "genres" are store labels.** Early Access and Free To Play appear in the genre list but aren't true genres.

## Files

| File | What it is |
|---|---|
| `Steam Genre Analysis.pdf` | Power BI report export |
| `Steam Genre Analysis.pbix` | Power BI source file |
| [Excel workbook (OneDrive)](https://1drv.ms/x/c/1a7e5bb9582a8d24/IQAiMkw1Fo-QT4_r_mrjMmToAWeT_wCAG2vZv_QB3Be6UP0?e=RhYArM&nav=MTVfezYzOTk4MzIzLTU1QTItNDM1OC1BN0UwLThFOTdGQjAxN0ZFRH0) | Cleaned workbook with formulas and pivot tables (too large for GitHub) |

## Data source

Steam games dataset (add source link here, e.g. the Kaggle page).

## Tools

Excel · Tableau Public · Power BI (Power Query, DAX)
