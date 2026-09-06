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