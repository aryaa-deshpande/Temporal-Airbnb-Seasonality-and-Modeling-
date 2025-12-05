# Temporal Airbnb Seasonality & Modeling 

This repository contains my implementation of the EAS 510 extra-credit assignment exploring seasonality patterns in Airbnb data and building predictive models for nightly price and booking probability. The work follows the full project specification: dataset construction, exploratory seasonality analysis, temporal modeling, XGBoost vs neural network comparison, and TensorBoard diagnostics.

---

## Repository Structure
```

├── Temporal-Airbnb-Seasonality-and-Modeling/
│   │
│   ├── data/
│   │   ├── raw/                         # InsideAirbnb CSVs (not included in repo)
│   │   └── processed/                   # Sampled panel files saved by the notebook
│   │
│   ├── images/
│   │   ├── importance/                  # XGBoost feature importance plots
│   │   │   ├── xgb_importance_bookings.png
│   │   │   └── xgb_importance_price.png
│   │   │
│   │   ├── seasonality/                 # Seasonality plots per city & snapshot
│   │   │   ├── austin_2024-12-14/
│   │   │   ├── austin_2025-03-06/
│   │   │   ├── chicago_2024-12-18/
│   │   │   ├── chicago_2025-03-11/
│   │   │   ├── dc_2025-03-13/
│   │   │   ├── dc_2025-12-18/
│   │   │   ├── santacruz_2025-03-28/
│   │   │   └── santacruz_2025-12-31/
│   │   │
│   │   └── tensorboard/                 # Screenshots of TensorBoard scalar curves
│   │       ├── epoch_accuracy.png
│   │       ├── epoch_auc.png
│   │       ├── epoch_loss.png
│   │       └── epoch_rmse.png
│   │
│   ├── Temporal-Airbnb-Seasonality-and-Modeling.ipynb
    │
    ├── requirements.txt
    └── README.md
```
---


## How to Run the Notebook

### 1. Create environment
```
pip install -r requirements.txt
```
### 2. Download the data

The notebook uses `InsideAirbnb` archived snapshots. You can download the same datasets from:

https://insideairbnb.com/get-the-data.html

For each of the following cities, create folders under data/raw/ in this format:
```
data/raw/<city>/<snapshot_date>/calendar.csv
data/raw/<city>/<snapshot_date>/listings.csv
```
Cities and dates used in the assignment:

	•	Austin: 2024-12-14, 2025-03-06
	•	Chicago: 2024-12-18, 2025-03-11
	•	Santa Cruz: 2025-03-28, 2025-12-31
	•	Washington DC: 2025-03-13, 2025-12-18

The notebook expects this folder structure, and reconstructs the panel dataset automatically.

---

## What the Notebook Does
	1.	Builds a cleaned night-level panel dataset
        •	Merges listings + calendar
        •	Cleans price, parses date, constructs is_booked
        •	Adds time-based features such as month, day-of-week,            week-of-year, etc.
	2.	Creates seasonality plots for each city/snapshot
        •	Average price by month
        •	Booking probability by month
        •	Weekend vs weekday comparisons
        •	Price by month × room type
        •	All plots are saved to images/seasonality/
	3.	Performs temporal modeling
        •	Train: early months
        •	Validation: middle months
        •	Test: unseen later months
        •	XGBoost (regression & classification)
        •	Neural networks with TensorBoard logging
	4.	Compares model behavior
        •	Feature importances
        •	Learning curves (from TensorBoard)
        •	Evaluation on unseen months
        •	Business insights and interpretation

All final discussion and analysis appear at the end of the notebook.

---

## Notes

	•	Raw InsideAirbnb data is not included due to file size; follow the structure above to place your copies locally.
	•	The project is fully reproducible once the raw data is added.

