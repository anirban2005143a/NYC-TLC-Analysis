### Dirty Data

1. `passenger_count`, `RatecodeID`, `store_and_fwd_flag`, `congestion_surcharge`, and `Airport_fee` contain null values.
2. `VendorID` should not contain any value other than `[2, 1, 7, 6]`.
3. `trip_distance` values do not match the pickup and drop-off time based on normal/extreme taxi speeds.
4. `trip_distance` contains `0` values.
5. `RatecodeID` should not contain any value other than `[1, 4, 2, 5, 99, 3, 6]`.
6. `total_amount` needs to be checked to determine whether it is mathematically correct by summing all applicable fees.

### Messy Data

1. Normalize the column names to `snake_case`.
2. `VendorID` should have the datatype `category`.
2. `VendorID` too many values from vendorId - 2.
3. `tpep_pickup_datetime` contains February 1st, 2026 dates (January 31st midnight).
3. `tpep_pickup_datetime` should be < `tpep_dropoff_datetime`
4. `tpep_dropoff_datetime` contains February 1st, 2026 dates.
4. `tpep_dropoff_datetime` should be > `tpep_pickup_datetime`
5. `passenger_count` contains many `0` values.
6. `passenger_count` can be of type `int8` since it represents the number of passengers in a taxi.
3. `trip_distance` Very short/non-zero distance. Distance vs. geographical pickup/drop-off zones
7. `RatecodeID` should be of categorical type.
8. `store_and_fwd_flag` should be of type `bool`.
9. `store_and_fwd_flag` contains many null values; this needs to be checked.
10. `payment_type` should be of categorical type.
11. `fare_amount` contains negative values; these need to be checked against the payment type.
12. `extra` contains negative values; these need to be checked against the payment type.
13. `mta_tax` contains negative values; these need to be checked against the payment type.
14. `tip_amount` contains negative values; these need to be checked against the payment type.
15. `tip_amount` contains suspiciously large values.
16. `tolls_amount` contains negative values; these need to be checked against the payment type.
17. `tolls_amount` contains suspiciously large values.
18. `improvement_surcharge` contains negative values; these need to be checked against the payment type.
19. `total_amount` contains negative values; these need to be checked against the payment type.
20. `total_amount` contains suspiciously large values; these need to be checked against `trip_distance` and trip duration.
21. `congestion_surcharge` contains negative values; these need to be checked against the payment type.
22. `Airport_fee` contains negative values; these need to be checked.
23. `cbd_congestion_fee` contains negative values; these need to be checked.

### Additional Information

1. `trip_distance` is measured in miles.
2. A new column, `trip_duration`, needs to be created.
3. Currency is in US dollars.
4. `VendorID = 2` has many issues, including negative values in fare-related columns.
