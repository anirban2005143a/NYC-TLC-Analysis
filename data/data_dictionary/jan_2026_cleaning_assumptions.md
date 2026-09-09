vendor_id : 
1. for january 2026 data, we consider this mapping - {
    1 : 'Creative Mobile Technologies, LLC',
    2 : 'Curb Mobility, LLC',
    6 : 'Myle Technologies Inc',
    7 : 'Helix'
} 
for value not in this mapping have 'Unknown Provider'
2. create a new col - 'vendor_name'


pickup_datetime & dropoff_datetime:
1. remove rows where pickup_datetime >= dropoff_datetime
2. Also allow dates - '2025-12-31' and '2026-02-01' in jan 2026 dataset(considering midnight cases).
3. create a new col named 'trip_duration'
3. remove those trips which have trip_duration < 2 min

passenger_count:
1. passenger count >= 1 , as 0 passengers is only `0.5554%` (0.005554 ratio)
1. as yellow_taxi is a kind of taxi , so allowed passenger is atmax 6. source : https://www.nyc.gov/site/tlc/passengers/passenger-frequently-asked-questions.page (Q: How many people can fit into a yellow taxicab?
A: The maximum amount of passengers allowed in a yellow taxicab by law is four (4) in a four (4) passenger taxicab or five (5) passengers in a five (5) passenger taxicab. All passengers must wear seat belts and children under the age of 4 must ride in child safety seats. Children under the age of 8 must ride in a child restraint system, such as a federally approved harness, vest, or booster-seat.)
3. drop na rows , because  "passenger_count",
    "fare_type_id",
    "store_and_fwd_flag",
    "congestion_surcharge_amount",
    "airport_fee_amount" - these cols also have na values in the same rows - showing a batch of trip recod missing 

trip_diatnce & taxi_speed:
1. taxi_speed < 100
2. create a new col for `great circle distance' between two representative point of pickup and dropoff zone respectively 
3. create 2 new col - distance_difference , distance_ratio
4. distance_ratio <= 5
4. distance_difference <= 10
5. trip_distance > 1


fare_type_id:
1. some fare_type_id is not matching with pickup and dropoff location - will create a col `fare_type_zone_mismatch`

fare_amount:
2. create a new col `fare_per_distance` group by `fare_type_id` . based on that remove outliers(fare_amount) 

mta_tax_amount:
1. remove mta_tax_amount > 1.0

tip_amount:
1. remove those tip_amount > 100
2. create a new for non credit card positive tip_amount

total_amount:
1. create a new col extra_total_amount = extra amount in total_amount