1. have so many trip record by vendor_id = 2, vendor_name = Curb Mobility, LLC
2. vendor 6 only has dirty data for passenger count
4. for vendor_id = 7, all values of this column are dirty or messy data 
5. passenger_count = null , have all fare_type_id = null & store_and_fwd_flag = null
4. passenger_count = null , mainly followe a trend of increasing null count from evening to night . Also increases at a interval of 8 to 9 days in that month 
3. store_and_fwd_flag most of the values 'N' - means direct sharing 
4. fare_amount < 0 - mostly is pickup_borough - 'Manhatan' and 'Queens'
                     mostly is dropoff_borough - 'Manhatan' , 'Queens', 'Brooklyn', 'Unknown'
                     JFK Airport has very high rate 
                     payment type - 4,2,3
                     fare_type_id - fare_type_id
                                    1     0.012825
                                    2     0.019909
                                    3     0.073855
                                    4     0.051093
                                    5     0.034933
                     all total_amount < 0
                *** will remove all negative fare_amount rows (its has a very high std in negative fare_amount) ,only 1.3% of total dataset

5. remove fare_type_id = 6 , having passenger count < 3
6. for fare_type_id = 99, there are so many rows where trip_distance very samll but fare_amount is very much 
