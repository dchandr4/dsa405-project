# Hybrid vs. Gasoline Fuel Economy, Model Year 2024

DSA 405 · Fall 2026 · Course project · Dhikshitha Chandrasekar (dchandr4)

## What this project is

Among model-year 2024 vehicles sold in the United States, do hybrids have higher combined fuel economy than gasoline-only vehicles of the same vehicle type and size class, and by how much?

The project compares hybrid and gasoline versions *within* each kind of vehicle, so hybrid small SUVs are compared with gasoline small SUVs and not with pickup trucks. The answer is meant to help a car buyer judge whether a hybrid's higher price is worth the fuel it saves.

## Where the data came from

| Source | Publisher | How it is collected | Used in |
|---|---|---|---|
| Model Year 2024 Fuel Economy and Technology Data (CSV, 1,978 rows × 164 columns) | U.S. Environmental Protection Agency, 2025 Automotive Trends Report. https://www.epa.gov/automotive-trends/explore-automotive-trends-data | Downloaded once and stored unmodified in `data/raw/` | P2 onward |
| Product Information Catalog and Vehicle Listing (vPIC) API | National Highway Traffic Safety Administration. https://vpic.nhtsa.dot.gov/api/ | Documented public API, one request per second, responses cached | P3 onward |

Download addresses and dates for every raw file are in [`data/raw/SOURCES.md`](data/raw/SOURCES.md).

**Citation:** US Environmental Protection Agency. 2025 EPA Automotive Trends Report. Data available at www.epa.gov/automotive-trends/explore-automotive-trends-data.

Both sources are free, public, need no login, and describe vehicles, not people.

## How to run it

1. Open `DSA405_002_FA26_P2_dchandr4.ipynb` on GitHub and click **Open in Colab** at the top.
2. In Colab choose **Runtime → Restart session and run all**.

Nothing needs to be downloaded first: the notebook reads the raw CSV straight from `data/raw/` in this repository over the web, so the code cannot change the raw file. The cleaned file and cleaning log are written to `data/clean/` inside the Colab session.

Requirements: Python 3 with pandas, numpy, matplotlib and seaborn (all preinstalled in Colab).

## What each milestone does

| Milestone | Notebook | Contents |
|---|---|---|
| P1 | `DSA405_002_FA26_P1_*.ipynb` | The question, the two sources, evidence both can be reached, terms of use |
| P2 | `DSA405_002_FA26_P2_dchandr4.ipynb` | Audit of the EPA file, data dictionary, cleaning log, row and column accounting, provenance brief. Cleans the EPA file from 1,978 rows × 164 columns to 1,427 rows × 37 columns |

## Repository layout

```
data/
  raw/
    model-year-2024-fuel-economy-and-technology-data.csv   raw EPA file, never edited
    SOURCES.md                                             where and when each raw file was downloaded
assignments/                                               course assignments
DSA405_002_FA26_P1_*.ipynb                                 P1
DSA405_002_FA26_P2_dchandr4.ipynb                          P2
README.md
```

Rule: files in `data/raw/` are never edited after upload, and no code writes to that folder.
