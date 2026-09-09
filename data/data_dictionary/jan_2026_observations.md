# this observations are from ongoing process of data cleaning , may noy present in the same pattern/trend in the final cleaned dataset

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
7. fare_type_id = 1 contributes 80% of the total extra charges 
8. found no relation between extra_amount and trip_distance, trip_duration, fare_amount
9. fare_type_id wise percentage of positive extra amount rows - 
     fare_type_id   fraction
     1              0.620404
     2              0.292638
     3              0.620422
     4              0.652105
     5              0.413089
     99             0.000030
9. payment_type wise percentage of positive extra amount rows - 
     payment_type
     1              0.572632
     2              0.550607
     3              0.788458
     4              0.595067
9. extra_amount does not having much outliers 
8. most of the rider pay though credit card
10. most of the trip is of type 1 = Standard rate
11. fare_type_id = 3, has a little bit higher avg extra_amount
12. payment_type = 1 (credit card) contributes most in total_extra_amount
13. payment_type = 3 (no charge) has avg and median extra_amount 1.7 and 2.25 dollar more that others respectively

tolls_amount:
1. tolls_amount contains a large number of zero values: Approximately 75% of trips have no toll charge, while the mean toll amount is about $0.78. Therefore, zero values should not be treated as missing or invalid data.

2. Some trips have relatively high toll amounts: The maximum observed toll is approximately $122.22, with 99% of observations at or below $7.46. These higher values are concentrated in certain pickup/drop-off areas, particularly Newark Airport (EWR) and Staten Island, and may reflect legitimate toll charges associated with specific routes.

3. No rows were removed based solely on tolls_amount: Since the higher toll values can be explained by trip location and routing, they were retained as potentially valid observations. The variable will instead be considered during analysis and outlier investigation.

4. Toll amounts vary considerably by pickup and drop-off location. The highest average tolls are concentrated around Staten Island and EWR (Newark Airport), while most locations in Queens, the Bronx, and Manhattan have substantially lower average toll amounts.

5. EWR and Staten Island stand out as high-toll areas. Newark Airport has an average toll of approximately $12.19 for pickups and $18.59 for drop-offs, while several Staten Island zones have average tolls above $14–$19. This suggests that toll charges are strongly associated with routes involving airports, bridges, and areas requiring toll crossings.

6. The geographical variation suggests that high tolls_amount values are not necessarily errors. Since the highest values occur systematically in particular pickup/drop-off zones rather than randomly across the dataset, these observations are likely influenced by the underlying travel routes and toll infrastructure. Therefore, extreme toll values were retained rather than removed solely as statistical outliers.

improvement_surcharge_amount:
1. seems good

airport_fee_amount:
1. around 4.68% airpost_fee_amount > 0 , in non airport pickup and dropoff zone/borough/service_type

2. The issue is heavily concentrated in Queens. East Elmhurst appears prominently for pickups, while many northern/eastern Queens zones such as Whitestone, Douglaston, Bay Terrace/Fort Totten, College Point, and Flushing appear for drop-offs. These areas are geographically close to the NYC airports, so this pattern is more suggestive of airport-related trips/fee rules or zone classification effects than random bad data.

3. LaGuardia Airport is showing up in your pickup results despite ~is_airport. This is the biggest thing I'd investigate. It suggests your is_airport definition may not be identifying the airport zones exactly as they appear in your dataset. In other words, this may be a classification/code issue rather than a data-quality issue.

4. I would not remove the 4.68% of records yet. The fact that the airport-fee observations are geographically concentrated around Queens and airport-adjacent areas gives us a reason to retain them until we understand the TLC's airport-fee rules and your is_airport condition.

total_amount :
1. not matching with sum of all tax/surcharges/amounts . May have some hidden cost
2. The comparison between total_amount and the sum of the available fare, tax, toll, tip, surcharge, and fee components shows that the remaining differences are not randomly distributed. The mismatches are strongly associated with particular fare_type_id values, indicating that certain fare types may follow additional or different fare-calculation rules.

3. Negative differences (where the calculated component total is higher than the recorded total_amount) are particularly common for JFK (fare_type_id = 2) and other special fare types. For example, the average residual for JFK trips is approximately -$4.0 to -$4.3, depending on payment type. This suggests that special airport/fare rules may affect how the final total_amount is calculated.

4. Positive differences are highly concentrated around +$2.50 across multiple fare and payment types. Because this difference is systematic and almost exactly $2.50 rather than a random floating-point error, it likely represents a specific fare/surcharge rule that is not captured by the simple component-sum formula.

5. The remaining discrepancies in total_amount are systematic rather than random: positive differences are consistently around +$2.50, while negative differences are concentrated around -$3.25 to -$3.75 and vary somewhat by location. Since these patterns occur across many pickup/drop-off zones and are likely related to fare or surcharge calculation rules rather than isolated data errors, the observations were retained and documented instead of being removed.

5. Payment type does not appear to be the primary explanation for these discrepancies: similar residual patterns occur across credit-card, cash, no-charge, and dispute records. Therefore, the observations were retained rather than removed, and the differences were treated as a characteristic of the fare-calculation structure requiring documentation rather than automatic data cleaning.