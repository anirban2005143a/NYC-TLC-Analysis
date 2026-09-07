### Dirty Data

1. `passenger_count`, `RatecodeID`, `store_and_fwd_flag`, `congestion_surcharge`, and `Airport_fee` contain null values.
2. `VendorID` should not contain any value other than `[2, 1, 7, 6]`. - done
3. `trip_distance` chross check with zone shape file approximate distance. - done
4. `trip_distance` contains `0` values. - done
5. `RatecodeID` should not contain any value other than `[1, 4, 2, 5, 99, 3, 6]`. - done
6. `total_amount` needs to be checked to determine whether it is mathematically correct by summing all applicable fees.
5. `PULocationID` IDs outside the official lookup. - done
5. `payment_type` should not contain any value other than `[0, 1, 2, 3, 4, 5, 6]`.

### Messy Data

1. Normalize the column names to `snake_case`.
2. `VendorID` should have the datatype `category`. - done
3. `tpep_pickup_datetime` contains February 1st, 2026 dates (January 31st midnight). - done
3. `tpep_pickup_datetime` should be < `tpep_dropoff_datetime` - done
4. `tpep_dropoff_datetime` contains February 1st, 2026 dates. - done
4. `tpep_dropoff_datetime` should be > `tpep_pickup_datetime` - done
5. `passenger_count` contains many `0` values. - done
6. `passenger_count` can be of type `int8` since it represents the number of passengers in a taxi. - done
3. `trip_distance` Very short/non-zero distance. Distance vs. geographical pickup/drop-off zones - done
3. `trip_distance` need to check correlation between trip disatance and total_amount or fare_amount
7. `RatecodeID` should have the datatype `category`. - done(int8)
8. `store_and_fwd_flag` should be of type `boolean`. - done
9. `PULocationID` should have the datatype `category`. - done
9. `PULocationID` 264 and 265 is unknown location. - done
9. `DOLocationID` should have the datatype `category`. - done
9. `DOLocationID` 264 and 265 is unknown location. - done
10. `payment_type` should have the datatype `category`. - done
10. `payment_type` check some patter like when and which payment type occure.
11. `fare_amount` contains negative values; these need to be checked against the payment type. - done
11. `fare_amount` change data type to float32 - done
12. `extra` contains negative values; these need to be checked against the payment type.
13. `mta_tax` contains negative values; these need to be checked against the payment type.
13. `mta_tax` Whether values follow the expected tax structure.
13. `mta_tax` Extremely large values(relative to other values)
14. `tip_amount` contains negative values; these need to be checked against the payment type.
15. `tip_amount` contains suspiciously large values.
16. `tolls_amount` contains negative values; these need to be checked against the payment type.
17. `tolls_amount` contains suspiciously large values.
18. `improvement_surcharge` contains negative values; these need to be checked against the payment type.
18. `improvement_surcharge` Whether the amount follows the expected surcharge structure.
19. `total_amount` contains negative values; these need to be checked against the payment type.
20. `total_amount` contains suspiciously large values; these need to be checked against `trip_distance` and trip duration.
21. `congestion_surcharge` contains negative values; these need to be checked against the payment type.
18. `congestion_surcharge` Whether the amount follows the expected surcharge structure.
22. `Airport_fee` contains negative values; these need to be checked.
13. `Airport_fee` Extremely large values(relative to other values)
23. `cbd_congestion_fee` contains negative values; these need to be checked.


External / Business-rule validation

For example:

Column	External validation
tip_amount	Compare with payment_type
airport_fee	Compare with airport pickup zones
congestion_surcharge	Compare with official congestion-zone rules
cbd_congestion_fee	Compare with Congestion Relief Zone rules
extra	Compare with official time/rate surcharge rules
fare_amount	Compare with TLC fare calculation rules
RatecodeID	Compare with rate-code definitions
PULocationID	Validate against TLC Taxi Zone lookup
DOLocationID	Validate against TLC Taxi Zone lookup
trip_distance	Compare against geographic plausibility
tolls_amount	Compare with possible toll routes
Airport_fee	Compare with JFK/LGA pickup requirement

### Additional Information

1. `trip_distance` is measured in miles.
2. A new column, `trip_duration`, needs to be created.
3. Currency is in US dollars.
4. `VendorID = 2` has many issues, including negative values in fare-related columns.
