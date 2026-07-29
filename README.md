# IMDB Top Movies EDA (1980 – 2026)

Exploratory Data Analysis of **16,252 top-rated IMDB movies** spanning four and a half decades — from *Star Wars: The Empire Strikes Back* (1980) to films released in 2026.

---

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Key Findings](#key-findings)
- [Analysis Sections](#analysis-sections)
- [Getting Started](#getting-started)
- [Requirements](#requirements)
- [Sample Visuals](#sample-visuals)
- [License](#license)

---

## Overview

This project explores patterns in cinema over 46 years through the lens of IMDB's user ratings and vote counts. The goal is to answer questions like:

- Has average film quality changed over time?
- Which genres have grown or declined?
- Do longer films score better?
- What's the relationship between popularity and quality?
- Which decades produced the best-rated films?

---

## Dataset

**File:** `imdb_top_movies_1980_2026.csv`

| Column | Type | Description |
|---|---|---|
| `imdb_id` | string | Unique IMDB identifier (e.g. `tt0111161`) |
| `title` | string | English title |
| `original_title` | string | Original language title |
| `year` | int | Release year (1980 – 2026) |
| `runtime_minutes` | float | Film duration in minutes |
| `genres` | string | Comma-separated genre tags (e.g. `Action,Drama`) |
| `average_rating` | float | IMDB weighted average rating (1.0 – 10.0) |
| `num_votes` | int | Number of user votes on IMDB |
| `imdb_url` | string | Direct link to IMDB page |

**Quick stats:**

| Metric | Value |
|---|---|
| Total films | 16,252 |
| Year range | 1980 – 2026 |
| Average rating | 6.40 |
| Average runtime | 109 min |
| Average votes | 66,332 |
| Most voted | The Shawshank Redemption (3.18M votes) |
| Highest rated | The Shawshank Redemption (9.3 ⭐) |
| Missing data | < 0.1% (1 runtime, 6 genres) |

---

## Project Structure

```
.
├── imdb_top_movies_1980_2026.csv   # Raw dataset
├── imdb_eda.ipynb                  # Main analysis notebook
└── README.md
```

---

## Key Findings

1. **Drama dominates every decade** — it is the most common genre tag and appears in over 50% of all multi-genre films.

2. **More votes → higher ratings** — there is a consistent positive correlation (~0.30) between vote count and average rating. Films that attract mass audiences tend to be rated more generously.

3. **Longer films score better** — movies over 150 minutes average ~6.8, while films under 90 minutes average ~6.1. Epic runtimes correlate with prestige.

4. **Annual output has exploded** — the number of films in the dataset grew roughly 5× from the 1980s to the 2020s, reflecting both increased production and IMDB's expanding coverage.

5. **The 1990s had the highest average ratings** — classics like *The Shawshank Redemption*, *Pulp Fiction*, *Schindler's List*, and *The Silence of the Lambs* anchor a golden-era profile.

6. **Action and Sci-Fi surged post-2000** — driven by franchise filmmaking (Marvel, DC, Star Wars), their genre share doubled from the 1980s to the 2010s.

7. **Average ratings have declined slightly** over the decades, likely due to more niche and low-budget titles entering the dataset as IMDB coverage broadens.

8. **Niche films (< 10K votes) have a much wider rating spread** — they are either hidden gems or forgotten failures; the middle ground is rare.

9. **Multi-genre films do not outperform single-genre films** — genre blending does not reliably improve audience reception.

10. ***The Shawshank Redemption* remains untouched** — highest rating, highest vote count, still #1 after 30 years.

---

## Analysis Sections

The notebook (`imdb_eda.ipynb`) is organized into 10 sections:

### 1. Setup & Data Loading
Environment configuration, visual theme, and data ingestion.

### 2. Data Overview & Quality
Shape, data types, descriptive statistics, missing values, and duplicates check.

### 3. Feature Engineering
New columns derived from raw data:
- `decade` / `decade_label` — decade grouping
- `genres_list` / `primary_genre` / `num_genres` — genre parsing
- `log_votes` — log-transformed vote count for visualization
- `pop_tier` — popularity bucket (Niche / Known / Popular / Very Popular / Blockbuster)
- `runtime_cat` — runtime bucket (< 90 min / 90–120 / 120–150 / 150+)

### 4. Distribution Analysis
Histograms with KDE, mean/median annotations, and boxplots for all three core numeric variables. Identifies extreme runtimes (566-minute outlier).

### 5. Temporal Trends
Yearly and decade-level trends for film count, average rating, average runtime, and median votes — all with 5-year rolling averages to smooth noise.

### 6. Genre Analysis
- Top 15 genres by frequency and by average rating
- Genre popularity vs. quality scatter (bubble chart)
- Genre share evolution over decades (stacked area chart)
- Impact of genre count on ratings

### 7. Rating Deep-Dive
- Violin plots of rating distribution by decade
- Boxplots of rating by popularity tier
- Top 20 highest-rated films (min 50K votes)
- Top 20 most-voted films with rating color coding

### 8. Popularity vs. Quality
- Full dataset scatter (16K+ points, colored by year)
- Correlation heatmap across all numeric features
- Rating distribution by runtime category

### 9. Decade Spotlights
- Best-rated film of each decade
- Top 3 genres per decade (grouped bar chart)

### 10. Key Findings
Summary table and numbered findings with evidence references.

---

## Getting Started

```bash
# Clone the repo
git clone https://github.com/<your-username>/imdb-eda.git
cd imdb-eda

# Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# Launch the notebook
jupyter notebook imdb_eda.ipynb
```

> **Tip:** Run all cells in order. The feature engineering section (§3) creates columns that later sections depend on.

---

## Requirements

| Package | Version tested |
|---|---|
| Python | ≥ 3.9 |
| pandas | ≥ 2.0 |
| numpy | ≥ 1.24 |
| matplotlib | ≥ 3.7 |
| seaborn | ≥ 0.13 |
| jupyter | any |

Install all at once:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Or with conda:

```bash
conda install pandas numpy matplotlib seaborn jupyter
```

---

## Sample Visuals

The notebook produces the following charts:

| Chart | What it shows |
|---|---|
| Rating histogram + KDE | Overall distribution centered around 6.4 |
| Yearly trends (2×2 grid) | Output growth, rating decline, runtime stability, vote surge |
| Decade bar charts | Count, avg rating, and avg runtime per decade |
| Genre frequency (horizontal bars) | Drama, Comedy, and Thriller lead |
| Genre popularity vs. quality (bubble) | Action is most popular; Documentary scores highest |
| Genre share area chart | Action/Sci-Fi rise post-2000 |
| Rating violin by decade | 1990s peak, gradual decline after 2010 |
| Rating by popularity tier | Blockbusters rate consistently higher |
| Top 20 most-voted (horizontal bar) | Shawshank, Dark Knight, Inception top the list |
| Scatter: votes vs. rating | Positive trend with wide variance |
| Correlation heatmap | Votes and rating most correlated pair |
| Rating by runtime category | Longer = rated better |
| Best film per decade table | Decade-by-decade hall of fame |

---

## License

This project is released under the [MIT License](LICENSE).

Data sourced from IMDB. This repository is for educational and research purposes only.

---

*Analysis by João Meira · July 2026*
