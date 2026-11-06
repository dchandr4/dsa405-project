# Hybrid vs. Gasoline Fuel Economy, Model Year 2024

DSA 405 · Fall 2026 · Course project · Dhikshitha Chandrasekar (dchandr4)

## What this project is

Among model-year 2024 vehicles sold in the United States, do hybrids have higher combined fuel economy than gasoline-only vehicles of the same vehicle type and size class, and by how much?

The project compares hybrid and gasoline versions *within* each kind of vehicle, so hybrid small SUVs are compared with gasoline small SUVs and not with pickup trucks. The answer is meant to help a car buyer judge whether a hybrid's higher price is worth the fuel it saves.

## Where the data came from

| Source | Publisher | How it is collected | Used in |
|---|---|---|---|
| Model Year 2024 Fuel Economy and Technology Data (CSV, 1,978 rows × 164 columns) | U.S. Environmental Protection Agency, 2025 Automotive Trends Report. https://www.epa.gov/automotive-trends/explore-automotive-trends-data | Downloaded once and stored unmodified in `data/raw/` | P2 onward |
| Product Information Catalog and Vehicle Listing (vPIC) API | National Highway Traffic Safety Administration. https://vpic.nhtsa.dot.gov/api/ | Documented public API (`GetModelsForMakeYear`), one request per second or slower if the response headers ask, every response cached in `data/raw/nhtsa_vpic_2024.zip` | P3 onward |

Download addresses and dates for every raw file are in [`data/raw/SOURCES.md`](data/raw/SOURCES.md).

**Credit:** NHTSA vehicle types from the National Highway Traffic Safety Administration's vPIC API (https://vpic.nhtsa.dot.gov/api/).

**Citation:** US Environmental Protection Agency. 2025 EPA Automotive Trends Report. Data available at www.epa.gov/automotive-trends/explore-automotive-trends-data.

Both sources are free, public, need no login, and describe vehicles, not people.

## How to run it

1. Open a notebook (P2 or P3) on GitHub and click **Open in Colab** at the top.
2. In Colab choose **Runtime → Restart session and run all**.

Nothing needs to be downloaded first: the notebooks read the raw EPA CSV straight from `data/raw/` in this repository over the web, so the code cannot change the raw file.

**P3 and the NHTSA API.** P3 first unpacks the cached API responses from `data/raw/nhtsa_vpic_2024.zip`, so a re-run does not call NHTSA again. Only if that file is missing does it call the API (about 160 requests, one per second, about 3 minutes) and save each response to `data/raw/nhtsa_vpic/`. After such a run, the notebook writes a new `nhtsa_vpic_2024.zip`; upload it to `data/raw/` here.

Outputs are written to `data/clean/` inside the Colab session: the cleaned EPA file and cleaning log (P2), and the NHTSA model list and the joined EPA + NHTSA table (P3).

Requirements: Python 3 with pandas, numpy, requests, matplotlib and seaborn (all preinstalled in Colab).

## What each milestone does

| Milestone | Notebook | Contents |
|---|---|---|
| P1 | `DSA405_002_FA26_P1_*.ipynb` | The question, the two sources, evidence both can be reached, terms of use |
| P2 | `DSA405_002_FA26_P2_dchandr4.ipynb` | Audit of the EPA file, data dictionary, cleaning log, row and column accounting, provenance brief. Cleans the EPA file from 1,978 rows × 164 columns to 1,427 rows × 37 columns |
| P3 | `DSA405_002_FA26_P3_dchandr4.ipynb` | Collects NHTSA vehicle types from the vPIC API (rate-limited, cached, fails loudly), compares the collection with the A8 plan, joins EPA and NHTSA many-to-one on make + model (left join, `validate="many_to_one"`), and checks the join with an 8-check verification suite |

## Repository layout

```
data/
  raw/
    model-year-2024-fuel-economy-and-technology-data.csv   raw EPA file, never edited
    nhtsa_vpic_2024.zip                                    cached NHTSA API responses (one JSON per make and vehicle type)
    SOURCES.md                                             where and when each raw file was downloaded
assignments/                                               course assignments
DSA405_002_FA26_P1_*.ipynb                                 P1
DSA405_002_FA26_P2_dchandr4.ipynb                          P2
DSA405_002_FA26_P3_dchandr4.ipynb                          P3
README.md
```

Rule: files in `data/raw/` are never edited after upload. The only code that writes there is P3's acquisition step, which adds new API responses to the cache and never changes an existing file.
