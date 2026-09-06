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

trip_diatnce & taxi_speed:
1. taxi_speed < 100
2. create a new col for `great circle distance' between two representative point of pickup and dropoff zone respectively 
3. create 2 new col - distance_difference , distance_ratio
4. distance_ratio <= 5
4. distance_difference <= 10
5. trip_distance > 1