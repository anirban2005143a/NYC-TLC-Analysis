# 🚕 NYC TLC Taxi Trip Analysis

An end-to-end **data analysis and visualization project** using New York City Taxi & Limousine Commission (NYC TLC) Yellow Taxi trip data.

The project focuses on understanding taxi trip patterns, identifying data-quality issues, cleaning and preparing the dataset, and building an interactive **Power BI dashboard** to explore trip, fare, payment, location, and operational patterns.

---

## 📌 Project Overview

The **New York City Taxi & Limousine Commission (NYC TLC)** publishes detailed trip records for licensed taxi services operating in New York City.

This project analyzes **January 2026 Yellow Taxi trip data** and follows a structured data analytics workflow:

**Raw Data → Data Exploration → Data Cleaning → Cleaned Dataset → Data Storage → Power BI Visualization**

The objective is to transform raw taxi trip records into meaningful insights that can help understand:

* 🚕 Taxi trip behavior
* 📍 Pickup and drop-off patterns
* 💰 Fare and payment patterns
* 👥 Passenger-related information
* ⏱️ Trip timing and duration
* 🗺️ Taxi-zone activity
* 📊 Overall operational patterns

---

## 🎯 Project Objectives

The main objectives of this project are:

1. Understand the structure and characteristics of NYC TLC trip data.
2. Identify missing, invalid, inconsistent, and abnormal records.
3. Clean individual data attributes systematically.
4. Prepare a reliable dataset for analysis and visualization.
5. Analyze taxi trips across time, location, fare, and payment dimensions.
6. Build an interactive Power BI dashboard for exploratory analysis.
7. Create a reproducible and well-documented data-processing workflow.

---

## 📊 Dataset

The project uses the **NYC TLC Yellow Taxi Trip Record dataset for January 2026**.

### Dataset Files

The repository contains:

* `yellow_tripdata_2026-01.csv` — Raw Yellow Taxi trip data
* `clean_yellow_tripdata_2026-01.csv` — Cleaned trip dataset
* `taxi_zone_lookup.csv` — Taxi-zone lookup information
* NYC TLC trip-record documentation and data dictionary

The raw and cleaned datasets are maintained separately to preserve the original source data and make the cleaning process reproducible.

---

## 🧹 Data Cleaning

Data cleaning is performed through multiple dedicated Jupyter notebooks rather than one large cleaning script.

The repository contains notebooks for cleaning different groups of variables:

| Notebook                                   | Purpose                                  |
| ------------------------------------------ | ---------------------------------------- |
| `observe_data.ipynb`                       | Initial data exploration and observation |
| `clean_vendor_id.ipynb`                    | Vendor ID validation                     |
| `clean_pickup_dropoff_datetime.ipynb`      | Pickup/drop-off datetime validation      |
| `clean_passenger_count.ipynb`              | Passenger count cleaning                 |
| `clean_trip_distance.ipynb`                | Trip-distance validation                 |
| `clean_fare_amount.ipynb`                  | Fare amount cleaning                     |
| `clean_extra_amount.ipynb`                 | Extra-charge validation                  |
| `clean_surcharge_amounts.ipynb`            | Surcharge cleaning                       |
| `clean_payment_type.ipynb`                 | Payment-type validation                  |
| `clean_fare_type_and_store_fwd_flag.ipynb` | Fare and store-forward flag cleaning     |
| `clean_locations.ipynb`                    | Pickup/drop-off location validation      |
| `store_to_pg.ipynb`                        | Storing processed data in PostgreSQL     |

The cleaning workflow focuses on detecting and handling invalid values, inconsistent records, missing information, and values that do not make logical sense for taxi trips.

---

## 🔍 Data Exploration

Before cleaning, the dataset is inspected to understand:

* Data types
* Missing values
* Duplicate or suspicious records
* Numerical distributions
* Categorical values
* Invalid ranges
* Location identifiers
* Temporal information
* Fare and payment variables

This exploratory stage helps determine appropriate cleaning rules before modifying the data.

---

## 📈 Analysis Areas

The cleaned dataset can be explored across several dimensions.

### 🚕 Trip Analysis

* Number of trips
* Trip distance
* Trip duration
* Passenger count
* Average trip characteristics

### 💰 Fare Analysis

* Fare amount
* Total trip amount
* Tips
* Tolls
* Surcharges
* Additional charges

### 💳 Payment Analysis

Analysis of different payment methods and their relationship with trip and fare characteristics.

### ⏰ Time Analysis

Trips can be analyzed according to:

* Date
* Hour
* Day of the week
* Pickup time
* Drop-off time

This helps identify changes in taxi activity throughout the day.

### 📍 Location Analysis

Taxi-zone information is used to understand:

* Popular pickup areas
* Popular drop-off areas
* Trip flows between zones
* Geographic distribution of taxi activity

---

## 🗺️ Taxi Zone Data

The repository also contains NYC taxi-zone shapefile components:

```text
taxi_zones/
├── taxi_zones.cpg
├── taxi_zones.dbf
├── taxi_zones.prj
├── taxi_zones.shp
└── taxi_zones.shx
```

These files provide the geographic information required for spatial analysis and visualization of NYC taxi zones.

---

## 📊 Power BI Dashboard

The project includes an interactive Power BI report:

```text
NYC_Taxi_Trip.pbix
```

The dashboard is designed to convert the processed taxi data into interactive visualizations and make it easier to explore relationships between:

* Trips
* Time
* Locations
* Distance
* Fare
* Payment
* Passengers

### Dashboard Goals

The Power BI report allows users to interactively explore the dataset instead of relying only on static charts.

Typical analysis questions include:

* When is taxi demand highest?
* Which locations generate the most trips?
* How does trip distance vary?
* How do fares change with trip characteristics?
* Which payment methods are most commonly used?
* How are trips distributed across NYC taxi zones?

---

## 🗂️ Project Structure

```text
NYC-TLC-Analysis/
│
├── data/
│   │
│   ├── cleaned_data/
│   │   └── clean_yellow_tripdata_2026-01.csv
│   │
│   ├── data_dictionary/
│   │   ├── data_dictionary_trip_records_yellow.pdf
│   │   ├── trip_record_user_guide.pdf
│   │   ├── jan_2026_cleaning_assumptions.md
│   │   ├── jan_2026_observations.md
│   │   └── jan_2026_problems.md
│   │
│   ├── data_processing/
│   │   ├── observe_data.ipynb
│   │   ├── clean_vendor_id.ipynb
│   │   ├── clean_pickup_dropoff_datetime.ipynb
│   │   ├── clean_passenger_count.ipynb
│   │   ├── clean_trip_distance.ipynb
│   │   ├── clean_fare_amount.ipynb
│   │   ├── clean_extra_amount.ipynb
│   │   ├── clean_surcharge_amounts.ipynb
│   │   ├── clean_payment_type.ipynb
│   │   ├── clean_fare_type_and_store_fwd_flag.ipynb
│   │   ├── clean_locations.ipynb
│   │   ├── store_to_pg.ipynb
│   │   └── instructions.md
│   │
│   ├── raw_data/
│   │   ├── yellow_tripdata_2026-01.csv
│   │   └── taxi_zone_lookup.csv
│   │
│   └── taxi_zones/
│       ├── taxi_zones.cpg
│       ├── taxi_zones.dbf
│       ├── taxi_zones.prj
│       ├── taxi_zones.shp
│       └── taxi_zones.shx
│
├── NYC_Taxi_Trip.pbix
└── README.md
```

---

## 🛠️ Tech Stack

### Programming & Data Analysis

* **Python**
* **Pandas**
* **Jupyter Notebook**

### Data Visualization & BI

* **Microsoft Power BI**

### Data Storage

* **PostgreSQL**

### Geospatial Data

* **NYC Taxi Zone Shapefiles**

### Data Formats

* CSV
* PDF
* Markdown
* Jupyter Notebook
* Power BI

---

## 🔄 Project Workflow

```text
              NYC TLC Dataset
                    │
                    ▼
             Raw Data Loading
                    │
                    ▼
            Data Observation
                    │
                    ▼
          Data Quality Analysis
                    │
                    ▼
          ┌─────────────────────┐
          │   Data Cleaning     │
          │                     │
          │ Vendor              │
          │ Datetime            │
          │ Passenger Count     │
          │ Trip Distance       │
          │ Fare                │
          │ Payment             │
          │ Location            │
          │ Surcharges          │
          └─────────────────────┘
                    │
                    ▼
             Cleaned Dataset
                    │
             ┌──────┴──────┐
             ▼             ▼
        PostgreSQL      Power BI
             │             │
             └──────┬──────┘
                    ▼
             Data Analysis
                    │
                    ▼
               Insights
```

---

## 💡 Key Outcomes

This project demonstrates an end-to-end approach to working with a real-world transportation dataset.

The project covers:

* Raw data exploration
* Data-quality assessment
* Attribute-level data cleaning
* Handling invalid and inconsistent values
* Geographic data integration
* Structured data storage
* Business-oriented exploratory analysis
* Interactive dashboard development

The resulting workflow provides a foundation for further analysis such as **demand forecasting, trip-duration prediction, anomaly detection, geographic demand analysis, and taxi fleet optimization**.

---

## 🚀 Future Improvements

Potential extensions of this project include:

* [ ] Analyze multiple months or years of TLC data
* [ ] Build demand forecasting models
* [ ] Predict trip duration and fare
* [ ] Perform advanced geospatial analysis
* [ ] Identify high-demand taxi zones
* [ ] Analyze peak-hour demand
* [ ] Detect anomalous or fraudulent trips
* [ ] Build automated ETL pipelines
* [ ] Automate Power BI data refresh
* [ ] Add machine-learning based predictive analytics

---

## 📚 Data Source

The project is based on publicly available data provided by the:

**New York City Taxi & Limousine Commission (NYC TLC)**

The repository also includes the relevant TLC trip-record documentation and data dictionary for understanding the dataset structure and variables.

---

## 👨‍💻 Author

**Anirban Das**

Computer Science & Engineering Student

GitHub: [@anirban2005143a](https://github.com/anirban2005143a)

---

## 📄 License

This project is intended for **educational and analytical purposes**.

The underlying NYC TLC data is provided by the New York City Taxi & Limousine Commission and remains subject to its respective data terms and conditions.
