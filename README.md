# Music-ETL-Pipeline
ETL pipeline combining Last.fm API data to A/B test music popularity across decades using Python, Pandas, SQLite and SciPy

Built this to answer a question: Are 2020s artists holding up better on 
streaming than 2010s artists, or is it just algorithm bias?

I pulled data from the Last.fm API, cleaned it, loaded it into SQLite, then ran 
a full A/B test suite to find out.

## what this project does

- hits the Last.fm API for artist stats and top tracks across 10 artists
- normalizes playcount into a 0-100 popularity score
- loads cleaned data into a SQLite database via SQLAlchemy
- runs 4 layers of statistical testing to validate results
- generates charts and styled tables to visualize findings

## a/b test design

**Group A (2010s):** Drake, Rihanna, Kanye West, Beyoncé, Eminem

**Group B (2020s):** Taylor Swift, Bad Bunny, The Weeknd, Olivia Rodrigo, Doja Cat

**Hypothesis:** 2020s artists are more popular on Last.fm today than 2010s artists

## tests run

**1. T-test**
checks if the difference in popularity scores between eras is 
statistically significant or not
result: p=0.001, significant across all 3 metrics (popularity, listeners, playcount)

**2. Effect size (Cohen's D)**
T-test shows if the difference is real and Cohen's D shows HOW BIG it is
- popularity score: d=-0.71 meaning medium effect
- listeners: d=1.021 meaning large effect
- playcount: d=-0.71 meaning medium effect

**3. Artist-level breakdown**
drilled into which specific artists are driving each era's score
found that 2020s is carried by Taylor Swift and The Weeknd
2010s is held back by Beyoncé (22.22) and Bad Bunny underperforms at 21.42

**4. Confidence intervals (95%)**
2010s: 29.94 to 38.87
2020s: 41.59 to 53.47
intervals don't overlap 

## results

| metric | 2010s | 2020s |
|---|---|---|
| avg popularity score | 34.41 | 47.53 |
| avg listeners | 6.2M | 4.0M |
| avg playcount | 16.7M | 23.1M |

finding: 2010s artists have more total listeners but 2020s artists 
get played more per listener. wider reach vs deeper engagement.

## stack

python · pandas · sqlalchemy · sqlite · scipy · matplotlib · last.fm api


DATABRICK IN PROGRESS

