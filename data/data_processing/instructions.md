# Notebook Execution Order

1. Run the **last cell** of `observe_data.ipynb`.
2. Run **all cells** of the following files in the given order:
   1. `clean_vendor_id.ipynb`
   2. `clean_passenger_count.ipynb`
   3. `clean_pickup_dropoff_datetime.ipynb`
   4. `clean_trip_distance.ipynb`
   5. `clean_locations.ipynb`
   6. `clean_fare_type_and_store_fwd_flag.ipynb`
   7. `clean_fare_amount.ipynb`
   8. `clean_payment_type.ipynb`
   9. `clean_extra_amount.ipynb`
   10. `clean_surcharge_amounts.ipynb`
   11. `store_to_pg.ipynb` ( If want to store in Postgres )