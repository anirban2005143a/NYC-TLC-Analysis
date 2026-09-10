# 🚕 NYC TLC Taxi Trip Analysis

An end-to-end **data quality, data cleaning, storage, and visualization project** using the **NYC TLC Yellow Taxi Trip Record Data — January 2026**.

The project takes raw taxi trip records through a structured data-quality and cleaning pipeline, stores the processed dataset in **PostgreSQL**, and uses **Power BI** to build interactive dashboards for understanding trip demand, efficiency, geography, fares, payments, and revenue.

---

## 📌 Project Overview

The **New York City Taxi & Limousine Commission (NYC TLC)** publishes trip-level records for New York City's taxi services.

This project focuses on turning the raw January 2026 Yellow Taxi dataset into a reliable analytical dataset through:

```text
Raw TLC Data
     ↓
Data Exploration
     ↓
Data Quality Analysis
     ↓
Column-wise Data Cleaning
     ↓
Cleaned Dataset
     ↓
PostgreSQL
     ↓
Power BI
     ↓
Interactive Analysis & Insights
```

The project is designed around an important principle:

> **Reliable analysis starts with reliable data.**

Instead of directly visualizing the raw dataset, each important attribute is inspected for missing, invalid, inconsistent, or logically impossible values before the data is used for analysis.

---

## 🎯 Objectives

The main objectives of this project are:

* Understand the structure of NYC TLC Yellow Taxi trip data.
* Perform systematic **data-quality analysis**.
* Identify missing, invalid, inconsistent, and anomalous values.
* Clean important attributes individually rather than applying generic rules.
* Preserve the raw dataset separately from the cleaned dataset.
* Store the cleaned data in PostgreSQL.
* Build an interactive Power BI dashboard.
* Analyze taxi demand, trip efficiency, geography, fares, payments, and revenue.
* Create a reproducible data-processing workflow.

---

## 📊 Dataset

### Source

**NYC Taxi & Limousine Commission — Trip Record Data**

The project currently uses:

* **Vehicle type:** Yellow Taxi
* **Period:** January 2026
* **Data type:** Trip-level records

The dataset contains information related to:

* Vendor
* Pickup and drop-off timestamps
* Passenger count
* Trip distance
* Pickup and drop-off taxi zones
* Rate code
* Payment type
* Fare
* Tips
* Tolls
* Surcharges
* Airport fees
* Total trip amount
* Other trip attributes

---

## 🧹 Data Quality & Cleaning

A major part of the project is **attribute-level data cleaning**.

Instead of putting every cleaning rule into a single large notebook, the project separates the work into dedicated notebooks for individual groups of columns.

### Cleaning workflow

| Notebook                                   | Purpose                                                            |
| ------------------------------------------ | ------------------------------------------------------------------ |
| `observe_data.ipynb`                       | Initial dataset exploration and identification of potential issues |
| `clean_vendor_id.ipynb`                    | Vendor ID validation                                               |
| `clean_pickup_dropoff_datetime.ipynb`      | Pickup/drop-off datetime validation                                |
| `clean_passenger_count.ipynb`              | Passenger count validation                                         |
| `clean_trip_distance.ipynb`                | Trip-distance validation                                           |
| `clean_fare_amount.ipynb`                  | Fare amount validation                                             |
| `clean_extra_amount.ipynb`                 | Extra-charge validation                                            |
| `clean_surcharge_amounts.ipynb`            | Surcharge and additional-charge validation                         |
| `clean_payment_type.ipynb`                 | Payment-type validation                                            |
| `clean_fare_type_and_store_fwd_flag.ipynb` | Rate/fare type and store-and-forward validation                    |
| `clean_locations.ipynb`                    | Pickup/drop-off location validation                                |
| `store_to_pg.ipynb`                        | Loading processed data into PostgreSQL                             |

### Data-quality checks include

* Missing values
* Invalid categorical values
* Invalid numerical ranges
* Zero and negative values where inappropriate
* Suspicious trip distances
* Invalid timestamps
* Passenger-count anomalies
* Fare and surcharge inconsistencies
* Payment-related inconsistencies
* Invalid pickup/drop-off locations
* Logical relationships between related fields
* Geographic consistency checks

The objective is not simply to remove unusual rows, but to determine **whether a value is actually invalid according to the meaning and constraints of the corresponding TLC field**.

---

## 🗃️ Data Organization

The project keeps different stages of the dataset separate:

```text
data/
├── raw_data/
│   ├── yellow_tripdata_2026-01.csv
│   └── taxi_zone_lookup.csv
│
├── cleaned_data/
│   └── clean_yellow_tripdata_2026-01.csv
│
├── data_processing/
│   ├── observe_data.ipynb
│   ├── clean_vendor_id.ipynb
│   ├── clean_pickup_dropoff_datetime.ipynb
│   ├── clean_passenger_count.ipynb
│   ├── clean_trip_distance.ipynb
│   ├── clean_fare_amount.ipynb
│   ├── clean_extra_amount.ipynb
│   ├── clean_surcharge_amounts.ipynb
│   ├── clean_payment_type.ipynb
│   ├── clean_fare_type_and_store_fwd_flag.ipynb
│   ├── clean_locations.ipynb
│   └── store_to_pg.ipynb
│
├── data_dictionary/
│   ├── data_dictionary_trip_records_yellow.pdf
│   ├── trip_record_user_guide.pdf
│   ├── jan_2026_observations.md
│   ├── jan_2026_problems.md
│   └── jan_2026_cleaning_assumptions.md
│
└── taxi_zones/
    ├── taxi_zones.cpg
    ├── taxi_zones.dbf
    ├── taxi_zones.prj
    ├── taxi_zones.shp
    └── taxi_zones.shx
```

The repository also contains the Power BI report:

```text
NYC_Taxi_Trip.pbix
```

---

# 🗺️ Taxi Zone Data

NYC TLC provides taxi-zone identifiers that can be mapped to geographic information.

This project includes the NYC taxi-zone shapefile components:

* `.shp`
* `.shx`
* `.dbf`
* `.prj`
* `.cpg`

These are used to support geographic analysis such as:

* Pickup-zone activity
* Drop-off-zone activity
* Zone-level demand
* Pickup vs. drop-off patterns
* Geographic distribution of trips
* Trip-distance analysis by location

---

# 📊 Power BI Dashboard

The cleaned dataset is used to build an interactive **Power BI dashboard**.

The dashboard is divided into three major analytical views.

---

## 1. 🚕 Trip Overview & Demand

This page focuses on the overall characteristics of taxi trips and demand patterns.

Key areas include:

* Total trip activity
* Trip demand
* Passenger information
* Trip distance
* Trip duration
* Time-based demand patterns
* Pickup/drop-off activity

### Dashboard

![Trip Overview & Demand](sceenshots/Trip%20Overview%20%26%20Demand.png)

---

## 2. 💰 Fare, Payment & Revenue Analysis

This page focuses on the financial side of taxi trips.

It explores:

* Fare amounts
* Total revenue
* Tips
* Payment methods
* Tolls
* Surcharges
* Additional charges
* Relationships between payment and trip characteristics

### Dashboard

![Fare, Payment & Revenue Analysis](sceenshots/Fare,%20Payment%20%26%20Revenue%20Analysis.png)

---

## 3. 📍 Trip Efficiency, Geography & Data Quality

This page combines operational and geographic analysis with data-quality information.

It focuses on areas such as:

* Trip efficiency
* Trip distance
* Trip duration
* Geographic distribution
* Pickup/drop-off zones
* Data-quality indicators
* Suspicious or problematic records

### Dashboard

![Trip Efficiency, Geography & Data Quality](sceenshots/Trip%20Efficiency,%20Geography%20%26%20Data%20Quality.png)

---

# 🔍 Analysis Areas

The cleaned dataset enables analysis across multiple dimensions.

### 🚕 Trip Analysis

* Number of trips
* Trip distance
* Trip duration
* Passenger count
* Average trip characteristics
* Trip efficiency

### ⏰ Time Analysis

Trips can be analyzed by:

* Date
* Hour
* Day of week
* Pickup time
* Drop-off time

This helps identify changes in taxi demand throughout the day.

### 📍 Geographic Analysis

Using taxi-zone information:

* Most active pickup zones
* Most active drop-off zones
* Pickup vs. drop-off patterns
* Geographic distribution of trips
* Zone-level demand
* Relationship between geographic distance and recorded trip distance

### 💳 Payment Analysis

Payment-related analysis includes:

* Payment-type distribution
* Fare by payment type
* Tips by payment type
* Revenue by payment type
* Payment and fare consistency

### 💵 Fare & Revenue Analysis

The project analyzes:

* Base fare
* Total amount
* Tips
* Tolls
* Surcharges
* Airport fees
* Additional charges
* Revenue patterns

---

# 🗄️ PostgreSQL

After cleaning, the processed dataset can be stored in **PostgreSQL**.

The `store_to_pg.ipynb` notebook handles the database-loading stage.

This creates a separation between:

```text
Raw Files
    ↓
Cleaning / Processing
    ↓
Cleaned Dataset
    ↓
PostgreSQL
    ↓
Power BI / Analysis
```

Using a database also makes the project more suitable for extending the workflow beyond a single CSV-based analysis.

---

# 🛠️ Technology Stack

### Data Analysis

* Python
* Pandas
* Jupyter Notebook

### Database

* PostgreSQL

### Visualization

* Microsoft Power BI

### Geographic Data

* NYC Taxi Zone Shapefiles

### Data Formats

* CSV
* PDF
* Markdown
* Jupyter Notebook
* Power BI

---

# 📁 Repository Structure

```text
NYC-TLC-Analysis/
│
├── data/
│   ├── cleaned_data/
│   ├── data_dictionary/
│   ├── data_processing/
│   ├── raw_data/
│   └── taxi_zones/
│
├── sceenshots/
│   ├── Fare, Payment & Revenue Analysis.png
│   ├── Trip Efficiency, Geography & Data Quality.png
│   └── Trip Overview & Demand.png
│
├── NYC_Taxi_Trip.pbix
├── .gitignore
├── .gitattributes
└── README.md
```

---

# 🔄 End-to-End Workflow

```text
                    NYC TLC
                 Yellow Taxi Data
                        │
                        ▼
                Raw Data Loading
                        │
                        ▼
                Data Exploration
                        │
                        ▼
             Data Quality Analysis
                        │
                        ▼
              Column-wise Cleaning
                        │
          ┌─────────────┼─────────────┐
          │             │             │
       Trip Data     Fare Data    Location Data
          │             │             │
          └─────────────┼─────────────┘
                        │
                        ▼
                 Cleaned Dataset
                        │
                 ┌──────┴──────┐
                 │             │
                 ▼             ▼
            PostgreSQL      Power BI
                 │             │
                 └──────┬──────┘
                        ▼
                Interactive Analysis
                        │
                        ▼
                    Insights
```

---

# 📈 Project Outcomes

This project demonstrates an end-to-end approach to working with a real-world transportation dataset.

### The project covers:

* Raw data exploration
* Data profiling
* Data-quality investigation
* Column-level validation
* Data cleaning
* Handling missing and invalid values
* Logical consistency checks
* Geographic data integration
* PostgreSQL data storage
* Power BI dashboard development
* Interactive transportation analysis

The emphasis of the project is on **building a trustworthy analytical dataset before drawing conclusions from it**.

---

# 🚀 Future Improvements

Possible extensions include:

* Analyze multiple months of TLC data
* Compare different years
* Build taxi-demand forecasting models
* Predict trip duration
* Predict fare/revenue
* Perform deeper geospatial analysis
* Analyze high-demand taxi zones
* Detect anomalous trips
* Build automated ETL pipelines
* Automate database updates
* Automate Power BI refresh
* Add predictive analytics and machine-learning models

---

# 📚 Data Source

The project uses publicly available data from the:

**New York City Taxi & Limousine Commission (NYC TLC)**

The repository also includes TLC documentation and data dictionaries used to understand the meaning and constraints of the dataset fields.

---

# 👨‍💻 Author

**Anirban Das**

Computer Science & Engineering Student

* GitHub: [@anirban2005143a](https://github.com/anirban2005143a)

---

## 📄 License & Data Usage

This project is intended for **educational and analytical purposes**.

The underlying taxi trip data is provided by the **NYC Taxi & Limousine Commission** and remains subject to the applicable NYC TLC data terms and conditions.
