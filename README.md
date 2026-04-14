# Music Era Analytics — ETL Pipeline

ETL pipeline combining Last.fm API data to A/B test music 
popularity across decades using Python, Pandas, Databricks 
Delta Lake, and SciPy.

Built this to answer a question: Are 2020s artists holding up 
better on streaming than 2010s artists, or is it just algorithm 
bias?

I pulled data from the Last.fm API, cleaned it, loaded it into 
Databricks Delta Lake, then ran a full A/B test suite to find out.

## Architecture

Last.fm API → Python ETL → Databricks Unity Catalog → 
Delta Lake → Databricks SQL Analytics → Visualizations

## What This Project Does

- Hits the Last.fm API for artist stats and top tracks 
  across 10 artists (100 tracks total)
- Normalizes playcount into a 0–100 popularity score
- Loads cleaned data into Databricks Delta Lake via Unity 
  Catalog with ACID compliance and schema enforcement
- Runs 4 layers of statistical testing to validate results
- Queries data using Databricks SQL Editor with 6 analytical 
  queries across popularity, listeners, and playcount dimensions
- Generates charts and visualizations to communicate findings

## Stack

| Layer | Technology |
|---|---|
| Extraction | Last.fm API, Python, Requests |
| Transformation | Pandas, SciPy |
| Storage | Databricks Delta Lake (Unity Catalog) |
| Analytics | Databricks SQL Editor |
| Statistical Testing | t-test, Cohen's D, 95% CI |
| Visualization | Databricks SQL, Matplotlib |

## A/B Test Design

- **Group A (2010s):** Drake, Rihanna, Kanye West, Beyoncé, Eminem  
- **Group B (2020s):** Taylor Swift, Bad Bunny, The Weeknd, 
  Olivia Rodrigo, Doja Cat

**Hypothesis:** 2020s artists are more popular on Last.fm today 
than 2010s artists.

## Tests Run

**1. T-test**
Checks if the difference in popularity scores between eras is 
statistically significant.
- Result: p=0.001 — significant across all 3 metrics 
  (popularity, listeners, playcount)

**2. Effect Size (Cohen's D)**
T-test shows if the difference is real. Cohen's D shows how big.
- Popularity score: d=-0.71 — medium effect
- Listeners: d=1.021 — large effect  
- Playcount: d=-0.71 — medium effect

**3. Artist-Level Breakdown**
Drilled into which artists drive each era's score.
- 2020s carried by Taylor Swift and The Weeknd
- 2010s held back by Beyoncé (22.22 avg popularity)
- Bad Bunny underperforms at 21.42 despite 2020s placement

**4. Confidence Intervals (95%)**
- 2010s: 29.94 to 38.87
- 2020s: 41.59 to 53.47
- Intervals don't overlap — strong evidence the difference is real

## Results

| Metric | 2010s | 2020s |
|---|---|---|
| Avg Popularity Score | 34.41 | 47.53 |
| Avg Listeners | 6.2M | 4.0M |
| Avg Playcount | 16.7M | 23.1M |

**Finding:** 2010s artists have more total listeners but 2020s 
artists get played more per listener. Wider reach vs deeper 
engagement.

## Databricks Delta Lake

** need to come back to this to upload the visuals from databricks

![Delta Table](screenshots/databricks_delta_table.png)

Data is stored as a managed Delta table in Unity Catalog 
(`workspace.default.music_tracks`) with ACID compliance, 
schema enforcement, and full SQL queryability via 
Databricks SQL Editor.

## SQL Analytics Layer

### Era Comparison
![Era Comparison](screenshots/era_comparison_chart.png)

### Artist Ranking  
![Artist Ranking](screenshots/artist_ranking_chart.png)

### A/B Test Summary
![A/B Test](screenshots/ab_test_summary.png)

### Listeners vs Playcount
![Scatter](screenshots/listeners_vs_playcount.png)

### Popularity Distribution
![Distribution](screenshots/popularity_distribution.png)

### Top Tracks by Artist
![Top Tracks](screenshots/top_tracks_by_artist.png)



## What I'd Add Next

- Automate the pipeline with Databricks Workflows (scheduled runs)
- Add dbt models for Silver/Gold layer transforms
- Expand to 50 artists across more genres
- Add Tableau dashboard for executive-level reporting
