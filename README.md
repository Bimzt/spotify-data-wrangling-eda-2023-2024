# Spotify Data Wrangling & Exploratory Data Analysis (2023-2024)

> End-to-end data wrangling and EDA pipeline merging two years of Spotify chart data to uncover music streaming trends, artist performance patterns, and distribution characteristics across 2023 and 2024.

---

## Overview

This project demonstrates a complete **data engineering and analysis workflow** applied to real-world music streaming data. Starting from two raw, structurally inconsistent CSV files, the pipeline standardizes, merges, cleans, and analyzes Spotify chart data to surface actionable insights about what drives a track's popularity on the world's largest music streaming platform.

Key focus areas:
- Multi-source data integration with schema harmonization
- Robust cleaning pipeline handling encoding issues, type mismatches, and missing values
- Outlier detection using statistical methods (IQR)
- Visual storytelling through distribution and ranking analysis

---

## Problem Statement

Spotify chart data across different years is inconsistently structured different column names, date formats, numeric encodings, and feature sets. How do we transform two messy, incompatible datasets into a unified, analysis-ready source of truth?

---

## Repository Structure

```
├── spotify-2023.csv                    # Raw Spotify Most Streamed Songs 2023
├── spotify-2024.csv                    # Raw Spotify Most Streamed Songs 2024
├── spotify_cleaned.csv                 # Output: cleaned & merged master dataset
├── cleaning_EDA_data.ipynb             # Version 1: initial wrangling & EDA
├── cleaning_EDA_data_version 2.ipynb   # Version 2: refined pipeline & extended analysis
└── README.md
```

---

## Dataset

| Property | 2023 Dataset | 2024 Dataset |
|----------|-------------|-------------|
| **Source** | [Kaggle — Most Streamed Spotify Songs 2023](https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023) | [Kaggle — Most Streamed Spotify Songs 2024](https://www.kaggle.com/datasets/nelgiriyewithana/most-streamed-spotify-songs-2024) |
| **Key Fields** | track, artist, streams, playlists, charts | track, artist, streams, playlists, charts |
| **Challenges** | Comma-separated numerics, mixed date columns | Extra platform columns (TikTok, SoundCloud), different date format |

---

## Pipeline Workflow

```
spotify-2023.csv ──┐
                   ├──► Schema Harmonization ──► pd.concat() ──► Deduplication
spotify-2024.csv ──┘         │                                        │
                              │                                        ▼
                    Column rename/drop                         Outlier Detection
                    Type casting                                  (IQR Method)
                    Null imputation (median)                         │
                    Date standardization                             ▼
                                                           spotify_cleaned.csv
                                                                     │
                                                                     ▼
                                                    Exploratory Data Analysis
                                                    ├── Stream distribution (histogram)
                                                    ├── Outlier visualization (boxplot)
                                                    └── Top artists by streams (barplot)
```

---

## Tech Stack

| Category | Tools |
|----------|-------|
| Language | Python 3.8+ |
| Data Manipulation | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Environment | Jupyter Notebook / Google Colab |

---

## Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/Bimzt/spotify-data-wrangling-eda-2023-2024
cd https://github.com/Bimzt/spotify-data-wrangling-eda-2023-2024
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the notebook
```bash
jupyter notebook "cleaning_EDA_data_version 2.ipynb"
```

> Ensure `spotify-2023.csv` and `spotify-2024.csv` are in the **same directory** as the notebook before running.

---

## Key Wrangling Steps

**2023 Data**
- Dropped audio feature columns (bpm, danceability, etc.) to focus on chart performance metrics
- Removed commas from numeric strings and cast to float
- Imputed missing `streams` values using column median
- Merged separate year/month/day columns into a unified datetime

**2024 Data**
- Dropped cross-platform columns (TikTok Posts, SoundCloud Streams, etc.)
- Extracted date components from `Release Date` string
- Renamed columns to match 2023 schema

**Integration**
- Concatenated both years with `pd.concat()`
- Removed duplicates on `(track, artist)` key pairs
- Detected outliers in `spotify_playlist` and `shazam_charts` using IQR method
- Exported final dataset to `spotify_cleaned.csv`

---

## EDA Highlights

| Analysis | Method | Insight |
|----------|--------|---------|
| Stream distribution | Histogram | Highly right-skewed — most tracks have modest streams; a small elite drives massive totals |
| Outlier detection | Boxplot (IQR) | Viral/evergreen tracks appear as extreme outliers in playlist and chart counts |
| Artist ranking | Barplot | Top artists dominate not just by hit count but by sustained playlist inclusion |

---

## Real-World Impact

This type of EDA pipeline has direct applications in the music and entertainment industry:

- **Record Label A&R** - Identifies emerging artists early by analyzing chart velocity and playlist penetration trends year-over-year
- **Marketing & Promotion** - Uncovers which release months and artist profiles correlate with peak streaming performance, informing campaign timing
- **Playlist Curators & DSPs** - Quantifies how playlist inclusion drives stream counts, supporting data-driven curation decisions
- **Streaming Economics Research** - The extreme skew in stream distributions reveals the "superstar effect" in digital music, relevant for policy discussions on royalty distribution
- **Data Engineering Education** - Demonstrates real-world schema harmonization challenges that practitioners face when integrating data from inconsistent sources