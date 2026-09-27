# Data sources

All raw files are in `data/raw/` and are not included in this repo because of their size.
Everything was downloaded on 2026-09-27.

## 1. NTSB aviation accident database

Source: https://data.ntsb.gov/avdata

| File | Years | Size | Contents |
|---|---|---|---|
| `avall.zip` → `avall.mdb` | 2008–2026 | 96 MB zipped, 559 MB unzipped | accidents and incidents investigated by the NTSB (Microsoft Access database) |
| `Pre2008.zip` → `Pre2008.mdb` | up to 2007 | 155 MB zipped, 893 MB unzipped | same tables for older events |
| `docs/codman.pdf` | – | 124 KB | coding manual (meaning of the codes) |
| `docs/eadmspub_legacy.pdf` | – | 19 KB | data dictionary for the older records |

Both databases have the same tables (`events`, `aircraft`, `engines`, `injury`, `Findings`, ...).

## 2. FAA General Aviation and Part 135 Activity Survey

Source: https://www.faa.gov/data_research/aviation_data_statistics/general_aviation
(one page per survey year, e.g. `.../general_aviation/cy2024`)

| File | Survey edition | Years covered | Tables used |
|---|---|---|---|
| `2024GASurveyCh1.xlsx` | CY2024 | 2013–2024 | 1.3 hours flown by aircraft type, 1.4 hours flown by actual use |
| `2024GASurveyCh3.xlsx` | CY2024 | 2024 | 3.1–3.3 aircraft and hours by use and aircraft type |
| `2012GASurveyChapter1Tables.xls` | CY2012 | 2001–2012 | 1.3 by aircraft type, 1.4 by actual use |
| `FAA_2004_1.xls` | CY2004 | 1992–2004 | 1.5 by aircraft type, 1.6 by actual use |

Hours are estimates from a sample survey, in thousands of hours.
The FAA never published estimates for 2011, so 2011 is missing.
The two old `.xls` files were opened in Excel and saved as `.xlsx` in `data/interim/`, because pandas
could not read the old format.

## 3. BTS National Transportation Statistics

Source: https://www.bts.gov/topics/national-transportation-statistics

| File | Table | Covers |
|---|---|---|
| `table_02_09_072726.xlsx` | 2-9 U.S. Air Carrier Safety Data | airlines (Part 121), 1960–2024 |
| `table_02_10_072726.xlsx` | 2-10 U.S. Commuter Air Carrier Safety Data | scheduled Part 135, 1980–2024 |
| `table_02_13_072726.xlsx` | 2-13 U.S. On-Demand Air Taxi Safety Data | charter / air taxi (Part 135 non-scheduled), 1975–2024 |
| `table_02_14_072726.xlsx` | 2-14 U.S. General Aviation Safety Data | general aviation, 1960–2024 |

Each table has accidents, fatal accidents, fatalities and flight hours per year (tables 2-9 and 2-10 also
have departures). The numbers come from the NTSB's official aviation statistics.
*2011 flight hours are missing in tables 2-13 and 2-14.

## How these are used

- **NTSB** – detailed information about the accidents
- **BTS** – flight hours and departures for airlines, commuters and charter, plus official accident counts
- **FAA survey** – flight hours inside general aviation (personal, business, corporate, training) and by aircraft type
