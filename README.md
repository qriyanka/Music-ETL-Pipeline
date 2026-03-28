# Music-ETL-Pipeline
ETL pipeline combining Last.fm API data to A/B test music popularity across decades using Python, Pandas, SQLite and SciPy


# Music Era A/B Test — ETL Pipeline

An end-to-end ETL pipeline that extracts music data from the Last.fm API, 
transforms it with Python, loads it into a SQLite database, and runs 
statistical A/B testing to compare music popularity across decades.

## Research Question
Are 2020s artists more popular than 2010s artists on Last.fm today?

## A/B Test Design
| | Group A | Group B |
|---|---|---|
| **Era** | 2010s | 2020s |
| **Artists** | Drake, Rihanna, Kanye West, Beyoncé, Eminem | Taylor Swift, Bad Bunny, The Weeknd, Olivia Rodrigo, Doja Cat |
| **Metric** | Popularity Score (normalized playcount) | Popularity Score (normalized playcount) |

## Results
- **2010s Average Score:** 34.41
- **2020s Average Score:** 47.53
- **P-value:** 0.001
- **Conclusion:** Statistically significant — 2020s artists are genuinely more popular on Last.fm today

## Tech Stack
- Python
- Pandas
- SQLAlchemy
- SQLite
- SciPy
- Matplotlib
- Last.fm API
- Google Colab

  ## 💡 Key Findings
- 2020s artists score 38% higher than 2010s artists
- Taylor Swift and The Weeknd are the top performers overall
- 2010s artists show more consistent but lower popularity
- 2020s artists show higher variance — some very high, some very low
