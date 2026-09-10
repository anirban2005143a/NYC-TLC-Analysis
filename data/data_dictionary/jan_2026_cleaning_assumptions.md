# NYC Taxi Trip — January 2026 Data Cleaning Rules & Assumptions

 ## Vendor ID

1. For the January 2026 data, we consider the following mapping:
```
vendor_mapping = {
    1: "Creative Mobile Technologies, LLC",
    2: "Curb Mobility, LLC",
    6: "Myle Technologies Inc",
    7: "Helix"
}
```

2. For values not present in this mapping, use `"Unknown Provider"`.
3. Create a new column named `vendor_name`.

---

 ## Pickup Datetime & Dropoff Datetime

 1. Remove rows where `pickup_datetime >= dropoff_datetime`.
2. Allow the dates `2025-12-31` and `2026-02-01` in the January 2026 dataset, considering midnight cases.
3. Create a new column named `trip_duration`.
4. Remove trips where `trip_duration < 2 minutes`.
5. The scatter plot and quantiles show very long trips as extreme outliers. Therefore, trips exceeding **8 hours** were removed to avoid affecting the analysis.

---

 ## Passenger Count

 1. Keep records where `passenger_count >= 1`, as records with `0` passengers represent only **0.5554%** (`0.005554` ratio).
2. As `yellow_taxi` is a type of taxi, the maximum allowed passenger count is **6**.
    **Source:** [NYC Taxi & Limousine Commission — Passenger Frequently Asked Questions](<https://www.nyc.gov/site/tlc/passengers/passenger-frequently-asked-questions.page>)
    > Q: How many people can fit into a yellow taxicab?\
   >  A: The maximum amount of passengers allowed in a yellow taxicab by law is four (4) in a four (4) passenger taxicab or five (5) passengers in a five (5) passenger taxicab. All passengers must wear seat belts and children under the age of 4 must ride in child safety seats. Children under the age of 8 must ride in a child restraint system, such as a federally approved harness, vest, or booster-seat.
3. Drop rows with `NA` values because the following columns also have `NA` values in the same rows, showing a batch of missing trip records:

```
[
    "passenger_count",
    "fare_type_id",
    "store_and_fwd_flag",
    "congestion_surcharge_amount",
    "airport_fee_amount"
]
```

---

 ## Trip Distance & Taxi Speed

1. Keep records where `taxi_speed < 100`.
2. Create a new column for **great-circle distance** between the representative points of the pickup and drop-off zones.
3. Create two new columns: `distance_difference` and `distance_ratio`
4. Keep records where: `distance_ratio <= 5`
5. Keep records where: `distance_difference <= 10`
6. Keep records where: `trip_distance > 1`

---

 ## Fare Type ID

1. Some `fare_type_id` values do not match the pickup and drop-off locations.
2. Create a new column named: `fare_type_zone_mismatch`

---

 ## Fare Amount

 1. Create a new column named `fare_per_distance`, grouped by `fare_type_id`.
2. Based on `fare_per_distance`, remove `fare_amount` outliers.
3. Remove all rows with negative `fare_amount`. These rows have a very high standard deviation and represent only **1.3% of the total dataset**.

---

 ## MTA Tax Amount

 1. Remove rows where: ` mta_tax_amount > 1.0`

---

 ## Tip Amount

 1. Remove rows where: `tip_amount > 100`

 2. Create a new column for positive `tip_amount` values from non-credit-card payments.

---

 ## Total Amount

 1. Create a new column named `extra_total_amount`, representing the extra amount in `total_amount`.

