# NYC Taxi Trip — January 2026 Data Cleaning Observations

 > **Note:** These observations are from the ongoing data-cleaning process and may not show the same patterns or trends in the final cleaned dataset.

 ## Vendor ID / Vendor Name

1. There are many trip records with `vendor_id = 2`, `vendor_name = Curb Mobility, LLC`.
2. `vendor_id = 6` only has dirty data for `passenger_count`.
3. For `vendor_id = 7`, all values in `pickup_datetime` and `dropoff_datetime` column are dirty .

---

 ## Passenger Count

1. When `passenger_count = null`, both `fare_type_id` and `store_and_fwd_flag` are also `null`.
2. Null `passenger_count` values mainly show an increasing trend from evening to night.
3. The number of null values also increases at intervals of around 8 to 9 days during the month.

---

 ## Store and Forward Flag

1. Most values of `store_and_fwd_flag` are `'N'`, meaning direct sharing.

---

 ## Fare Amount

1. For `fare_amount < 0`, the main observations are:
   - Pickup boroughs are mostly `Manhattan` and `Queens`.
   - Drop-off boroughs are mostly `Manhattan`, `Queens`, `Brooklyn`, and `Unknown`.
   - `JFK Airport` has a very high rate.
   - Payment types are mainly `4`, `2`, and `3`.


2. All rows with negative `fare_amount` also have `total_amount < 0`.
3. After removing negative `fare_amount` , all other negative values of other columns (surcharge columns) got solved.

---

 ## Fare Type ID

1. Remove `fare_type_id = 6` when `passenger_count < 3`.
2. For `fare_type_id = 99`, many rows have very small `trip_distance` but very high `fare_amount`.
3. Most trips are `fare_type_id = 1`, which represents the **Standard rate**.


---

 ## Extra Amount

1. No clear relation was found between `extra_amount` and `trip_distance`, `trip_duration`, or `fare_amount`.
2. `extra_amount` does not have many outliers.
3. `payment_type = 1` (credit card) contributes the most to total `extra_amount`.
4. `payment_type = 3` (no charge) has an average `extra_amount` that is **\$1.70 higher** than others.
5. The median `extra_amount` for `payment_type = 3` is **\$2.25 higher** than others.
6. Most riders pay through credit card.
7. `fare_type_id = 3` has a slightly higher average `extra_amount`.
8. `fare_type_id = 1` contributes around **80% of the total extra charges**.

---

 # Tolls Amount

1. `tolls_amount` contains many zero values. Around **75% of trips have no toll charge**, while the mean toll amount is about **\$0.78**. Therefore, zero values should not be treated as missing or invalid.
2. Some trips have relatively high toll amounts. The maximum is approximately **\$122.22**, while **99% of observations are at or below \$7.46**.
3. Higher toll values are concentrated around certain pickup/drop-off areas, particularly **Newark Airport (EWR)** and **Staten Island**, and may reflect legitimate route-related toll charges.
4. **No rows were removed based only on `tolls_amount`.** Higher values were retained because they can be explained by trip location and routing.
5. Toll amounts vary considerably by pickup and drop-off location. The highest average tolls are concentrated around **Staten Island** and **EWR**, while Queens, the Bronx, and Manhattan generally have lower averages.
6. Newark Airport has an average toll of approximately **\$12.19 for pickups** and **\$18.59 for drop-offs**. Several Staten Island zones also have average tolls above **\$14–\$19**.
7. The geographical pattern suggests that high `tolls_amount` values are not necessarily errors. Extreme values were therefore retained rather than removed solely as statistical outliers.

---

# Improvement Surcharge Amount

1. `improvement_surcharge_amount` seems good.

---

# Airport Fee Amount

1. Around **4.68%** of records with `airport_fee_amount > 0` are in non-airport pickup, drop-off, borough, or service-type categories.
2. The issue is heavily concentrated in **Queens**. East Elmhurst appears prominently for pickups, while several northern/eastern Queens zones appear for drop-offs.
3. These areas are geographically close to the NYC airports, so the pattern may be related to airport trips, fee rules, or zone classification.
4. **LaGuardia Airport** appears in the pickup results despite `~is_airport`. This is the main point to investigate.
5. This suggests that the `is_airport` definition may not be identifying airport zones exactly as they appear in the dataset. It may therefore be a classification or code issue rather than a data-quality issue.
6. **Do not remove the 4.68% of records yet.** The airport-fee observations are concentrated around Queens and airport-adjacent areas, so they were retained until the TLC airport-fee rules and `is_airport` condition are understood.

---

# Total Amount

1. `total_amount` does not match the sum of all tax, surcharge, and amount components. There may be some hidden cost.
2. The differences between `total_amount` and the calculated component sum are not randomly distributed. They are strongly associated with certain `fare_type_id` values.
3. Negative differences are particularly common for **JFK (`fare_type_id = 2`)** and other special fare types. The average JFK residual is approximately **-\$4.0 to -\$4.3**, depending on payment type.
4. Positive differences are highly concentrated around **+\$2.50** across multiple fare and payment types. This may represent a specific fare or surcharge rule not included in the simple component-sum formula.
5. Negative differences are mainly around **-\$3.25 to -\$3.75** and vary somewhat by location. These patterns appear systematic rather than random.
6. Since the differences are likely related to fare or surcharge calculation rules, the observations were retained and documented rather than removed.
7. Payment type does not appear to be the primary explanation. Similar residual patterns occur across credit-card, cash, no-charge, and dispute records.

---

# Trip Duration

1. Trips longer than 8 hours are rare, with **646 trips exceeding 5 hours**. Most of these are from **Manhattan (392)** and **Queens (141)**.


