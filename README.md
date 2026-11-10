# NYC Historical Vital Records — Postman Collection

Postman collection for the **NYC Historical Vital Records** indexes published by the NYC Department of Records and Information Services (DORIS) / Municipal Archives on [NYC Open Data](https://data.cityofnewyork.us/browse?Data-Collection_Data-Collection=NYC+Historical+Vital+Records), using the Socrata SODA API. No API key required.

| Dataset | ID | Years | Rows |
|---|---|---|---|
| [Births](https://data.cityofnewyork.us/d/5gq7-rgmv) | `5gq7-rgmv` | 1855–1909 | ~2.6M |
| [Deaths](https://data.cityofnewyork.us/d/797j-9xvg) | `797j-9xvg` | 1862–1948 | ~3.7M |
| [Marriages](https://data.cityofnewyork.us/d/j62e-7maa) | `j62e-7maa` | 1866–1937 | ~5.3M |
| [Marriage licenses](https://data.cityofnewyork.us/d/d8dr-nyhw) | `d8dr-nyhw` | 1908–1949 | ~1.3M |

## Import
Postman → **Import** → paste:
`https://raw.githubusercontent.com/mikeyeves/NYC-Historical-Vital-Records-Postman/main/NYC_Historical_Vital_Records.postman_collection.json`

## Variables
| Variable | Example | Notes |
|---|---|---|
| `last_name` | `Glassheim` | exact, case-insensitive |
| `first_name` | `Nath` | prefix; blank = any |
| `borough` | `MANHATTAN` | MANHATTAN, KINGS, BRONX, QUEENS, RICHMOND; blank = all |
| `year_from` / `year_to` | `1880` / `1910` | inclusive |
| `limit` | `200` | max rows |
| `app_token` | | optional Socrata app token (enable the `X-App-Token` header) |

## Requests (per dataset)
- **Search by name** — surname + first-name prefix + borough + year range
- **Sounds-like (Soundex)** — a pre-request script computes Soundex from `last_name` (verified against the dataset's own column) to catch spelling variants
- **Look up by certificate number** — numbers restart every year in every borough, so borough + year are required
- **Full-text search**, **count by year**, **CSV download**
- **Marriages → Find both spouses** — the index has one row per spouse; rows sharing borough + year + number are the couple
- **Open certificate** — link to the scanned certificate on the [Municipal Archives site](https://a860-historicalvitalrecords.nyc.gov)

Every search renders a table in Postman's **Visualize** tab with a *view* link to the certificate, and saves the first row's number/year/borough for the follow-up requests.

## Notes
- Deaths store `county`/`month` in lower case and births/marriages in upper case; all requests use `upper()` so this doesn't matter.
- These are **indexes**; the certificates themselves are viewed on the Municipal Archives site.

## Related collections
- [Unified Census ED Finder](https://github.com/mikeyeves/Unified-Census-ED-Finder-Postman)
- [Federal Register & National Archives Catalog APIs](https://github.com/mikeyeves/US-Federal-Register-National-Archives-Catalog-APIs)
- [Hebcal Jewish Calendar APIs](https://github.com/mikeyeves/Hebcal-Jewish-Calendar-APIs)
