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

*(Summarize 3-5 major insights from your notebook, focusing on data characteristics, feature effectiveness, and comparisons.)*
* Example: Aggregating trip segments by `trip_uuid` effectively consolidates multi-leg journeys, allowing for trip-level feature creation (e.g., total actual time, total OSRM distance).
* Example: Engineered time features (e.g., `trip_duration = od_end_time - od_start_time`) correlate well with actual delivery times but show discrepancies compared to `start_scan_to_end_scan`, suggesting potential process gaps.
* Example: Significant differences exist between actual travel times/distances and OSRM estimates, particularly in certain geographical regions or during specific times, highlighting areas for route optimization or better estimation models.
* Example: Outlier analysis reveals specific trips with exceptionally long durations or distances, potentially indicating operational issues, data errors, or unique circumstances requiring investigation.

## Recommendations

*(List 3-5 actionable recommendations based on your feature engineering and analysis. Keep language clear.)*
* Example: Utilize the aggregated trip-level features (total time, total distance, engineered time components) as primary inputs for delivery time prediction models.
* Example: Investigate the discrepancies between actual time and OSRM time further; consider incorporating real-time traffic or event data to improve OSRM accuracy or build custom estimation models.
* Example: Implement robust outlier detection and handling mechanisms in data pipelines to flag potentially problematic trips for operational review.
* Example: Use the extracted geographical features (State, City) combined with performance metrics (time differences) to identify regions or corridors needing operational improvements or infrastructure focus.

## Tools Used

* **Programming Language:** Python
* **Libraries:** Pandas (Data Manipulation), NumPy, Matplotlib & Seaborn (Visualization), Scikit-learn (Encoding, Scaling), SciPy.stats (Hypothesis Testing - Optional)
* **Environment:** Jupyter Notebook

## License
[Apache License 2.0](LICENSE)  
