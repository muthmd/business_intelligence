# Midwest Airbnb Listings: Data Dictionary

**Dataset:** `listings` table in `midwest_airbnb.db` (SQLite), 14,887 rows and 29 columns
**Source:** Inside Airbnb (https://insideairbnb.com/get-the-data/), the detailed `listings.csv.gz` file for each of three regions: Chicago (snapshot 2026-07-20), Columbus (snapshot 2026-07-23), and Twin Cities MSA (snapshot 2026-07-21). Column meanings follow Inside Airbnb's data dictionary and assumptions (https://insideairbnb.com/data-assumptions/).
**Course:** ISA 401, Miami University

> One row is one listing that showed a nightly price on the snapshot date; listings with no price were dropped. Empty cells are stored as SQL `NULL`.

---

## Field Definitions

| Field | Type | Description |
|---|---|---|
| `city` | text | Which Inside Airbnb region the listing came from: `Chicago` (7,439 rows), `Columbus` (2,587), or `Twin Cities` (4,861). The Twin Cities file covers the Minneapolis-St. Paul metro area, not just the two cities. |
| `snapshot_date` | text | Date Inside Airbnb compiled the file, stored as an ISO text string, not a date: `2026-07-20` for Chicago, `2026-07-23` for Columbus, `2026-07-21` for Twin Cities. Every row of a city shares the same value. |
| `id` | text | Airbnb's listing id. Unique across the table (14,887 distinct values). Stored as text even though it looks numeric, so compare it to a quoted string. |
| `name` | text | Listing title as shown on Airbnb (for example "Tiny Studio Apartment 94 Walk Score"). Never empty. |
| `price` | real | Nightly price in U.S. dollars on the snapshot date, with the dollar sign and commas removed. Ranges from 2.56 to 11,412; never `NULL` (rows without a price were dropped). |
| `room_type` | text | Airbnb's four listing categories: `Entire home/apt` (11,652 rows), `Private room` (2,951), `Hotel room` (246), or `Shared room` (38). |
| `host_id` | text | Airbnb's id for the host. One host can have many listings (6,970 distinct hosts). Stored as text. |
| `host_name` | text | Host's display name, e.g. "David" or a company like "Evolve". Not unique, so use `host_id` to count hosts. `NULL` for 25 rows. |
| `host_since` | text | Date the host joined Airbnb. Empty (`NULL`) for every row in this table. |
| `host_is_superhost` | text | Whether the host is an Airbnb Superhost: `t` (yes, 7,982 rows) or `f` (no, 6,880). `NULL` for 25 rows. |
| `neighbourhood` | text | Inside Airbnb's `neighbourhood_cleansed`. Chicago uses community areas (e.g. "Loop"), Columbus uses city areas (e.g. "Downtown"), and the Twin Cities use counties (e.g. "Hennepin", "Ramsey"). |
| `latitude` | real | Latitude of the listing, about 39.9 to 46.2. Airbnb shifts locations slightly for privacy. |
| `longitude` | real | Longitude of the listing, about -94.5 to -82.8. |
| `property_type` | text | Detailed property type chosen by the host, e.g. "Entire rental unit", "Entire home", "Private room in home" (62 types). |
| `accommodates` | integer | Maximum number of guests, 1 to 16. |
| `bedrooms` | real | Number of bedrooms, 1 to 16. `NULL` for 2,976 rows. |
| `beds` | real | Number of beds, 1 to 32. `NULL` for 668 rows. |
| `bathrooms_text` | text | Bathrooms as written on Airbnb, e.g. "1 bath", "2.5 baths", "1 shared bath". Text, not a number. |
| `minimum_nights` | integer | Shortest stay allowed in nights, 1 to 365. Most are 1 or 2; 30 or more means a monthly rental. |
| `availability_365` | integer | Nights available to book in the next 365 days, 0 to 365. |
| `number_of_reviews` | integer | Total reviews the listing has ever received, 0 to 2,246. |
| `number_of_reviews_ltm` | integer | Reviews in the last 12 months ("ltm" = last twelve months), 0 to 1,220. |
| `first_review` | text | Date of the first review, as `YYYY-MM-DD`. `NULL` if the listing has no reviews (1,761 rows). |
| `last_review` | text | Date of the most recent review, as `YYYY-MM-DD`. `NULL` if the listing has no reviews. |
| `review_scores_rating` | real | Average guest rating from 1 to 5; most are above 4.7. `NULL` if no reviews. |
| `reviews_per_month` | real | Average number of reviews per month, 0.01 to 77.72. `NULL` if no reviews. |
| `instant_bookable` | text | Whether guests can book without host approval. Empty (`NULL`) for every row in this table. |
| `estimated_revenue_l365d` | real | Inside Airbnb's estimate of revenue over the last 365 days in U.S. dollars (price times estimated nights booked, based on reviews). 0 to 1,114,800; an estimate, not actual earnings. |
| `amenities_count` | integer | Number of amenities the listing lists (wifi, kitchen, etc.), computed for this course. 0 to 100. |

