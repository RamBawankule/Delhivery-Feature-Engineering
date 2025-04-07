# Delhivery Logistics Data: Feature Engineering

![image](https://github.com/user-attachments/assets/06edd02e-7323-4d9e-9be9-a41aae32f5d6)

## Project Overview

This project focuses on processing and transforming raw logistics data from Delhivery, India's largest fully integrated logistics player. The objective is to clean the data, handle its multi-segment trip structure, engineer meaningful features, and prepare a dataset suitable for use by data science teams for tasks like delivery time forecasting or route optimization modeling.

## Business Problem

Delhivery's data team needs to process complex data flowing from operational pipelines. Key challenges include:
* Handling data where a single delivery trip is represented across multiple rows (segments).
* Cleaning and sanitizing raw fields.
* Extracting meaningful features from timestamps, location names, and time/distance metrics.
* Comparing actual operational metrics (time, distance) with estimated metrics (e.g., from OSRM).
* Creating a clean, aggregated dataset with engineered features ready for modeling.

## Dataset

The dataset (`delhivery_data.csv`) contains detailed trip-level information, including:

* **Identifiers:** `trip_uuid`, `route_schedule_uuid`, `source_center`, `destination_cente`
* **Timestamps:** `trip_creation_time`, `od_start_time`, `od_end_time`, `cutoff_timestamp`
* **Route Info:** `route_type`, `source_name`, `destination_name`
* **Time Metrics:** `start_scan_to_end_scan`, `actual_time`, `osrm_time`, `segment_actual_time`, `segment_osrm_time`
* **Distance Metrics:** `actual_distance_to_destination`, `osrm_distance`, `segment_osrm_distance`
* **Other:** `data` (train/test marker), `is_cutoff`, `cutoff_factor`, `factor`, `segment_factor`

## Repository Structure

```text
Delhivery-Feature-Engineering/
├── data/
│   └── delhivery_data.csv  
├── notebooks/
│   └── delhivery_feature_engineering.ipynb   
├── reports/                      
│   └── delhivery_analysis_report.pdf
├── .gitignore
├── LICENSE 
└── README.md                   
```

## Key Findings & Insights
 
* **Effective Aggregation:** Grouping data by `trip_uuid` successfully consolidates multi-segment journeys, enabling the creation of meaningful trip-level features (like total actual time, total OSRM distance).
* **Value of Engineered Features:** Features derived from timestamps (e.g., hour, day of week, month) and locations (e.g., state, city extracted from names) provide valuable dimensions for analysis and potential modeling.
* **Actual vs. OSRM Discrepancies:** Significant deviations are observed between actual travel times/distances and OSRM estimates, indicating potential real-world factors (traffic, delays, route choices) not fully captured by OSRM, offering areas for model or operational improvement.
* **Operational Patterns:** Analysis reveals dominant route types (e.g., FTL preference), high-traffic corridors (busiest state/city pairs), and identifies outliers in time/distance metrics that may correspond to operational exceptions or data issues.

## Recommendations

1.  **Utilize Engineered Features:** Prioritize the aggregated trip-level data and newly engineered time/location features as inputs for predictive models (e.g., delivery time forecasting).
2.  **Refine Estimation Models:** Investigate the systematic differences between actual and OSRM metrics; consider developing custom estimation models or augmenting OSRM with real-time data (traffic, weather) for better accuracy.
3.  **Implement Anomaly Detection:** Integrate outlier detection mechanisms based on the identified time/distance thresholds into operational data pipelines to flag potentially problematic trips for proactive review and intervention.
4.  **Optimize High-Traffic Routes:** Focus logistics optimization efforts (e.g., resource allocation, route planning, exploring alternative modes like Carting) on the identified high-volume corridors and states to improve efficiency and reduce delays.
   
## Tools Used

* **Programming Language:** Python
* **Libraries:** Pandas (Data Manipulation), NumPy, Matplotlib & Seaborn (Visualization), Scikit-learn (Encoding, Scaling), SciPy.stats (Hypothesis Testing)
* **Environment:** Jupyter Notebook

## License
[Apache License 2.0](LICENSE)  
