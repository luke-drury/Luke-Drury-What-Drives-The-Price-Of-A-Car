# What Drives the Price of a Used Car?
_A quick, student-friendly ML project_

**Author:** _Your Name_  
**Course:** Practical Application II — Initial Report & EDA  
**Notebook:** `notebooks/01_used_car_price_eda_modeling.ipynb`

---

## 1) Goal (Business Understanding)
Help a used-car dealership understand **which factors drive price** (age, mileage, brand, transmission, fuel, etc.) and produce a simple, defensible model to **estimate fair value**.

---

## 2) Data (Data Understanding)
- **Source:** Kaggle “Used Cars / Craigslist vehicles”–style dataset (typical columns: `price`, `year`, `odometer`, `manufacturer`, `model`, `transmission`, `fuel`, etc.).  
- **Local file:** `data/used_cars.csv`  
- I work entirely from the CSV (no external services needed).

> If your CSV has different column names, the notebook includes a small
> “column normalization” helper to auto-detect common variants.

---

## 3) Methods (Data Prep, EDA, Modeling)
**Cleaning & Prep**
- Remove duplicates and unrealistic entries (price, year, mileage bounds).
- Feature engineering: `age = current_year - year`, `miles_per_year = mileage / age`.
- Light imputation for categoricals; standardize text (lowercase/strip).
- One-hot encoding for selected categorical features.

**EDA Visuals**
- Distributions: price, mileage, age (histograms).  
- Relationships: price vs mileage, price vs age (scatter).  
- Grouped views: price by brand, transmission (boxplots).  
- Clear titles, axis labels, and readable scales.

**Models (fast, no grid search)**
- **Ridge Regression** (very fast, interpretable)  
- **HistGradientBoosting (compact settings)** (fast, non-linear)  
- Quick 3-fold CV check on the winning model for sanity.

**Evaluation**
- Primary: **RMSE** (penalizes large pricing errors).  
- Also: **MAE**, **R²**.  
- Predicted vs. Actual plot for the best model.

---

## 4) Results (Initial)
> Replace with your actual numbers after running.

- **Best model:** `___`  
  - RMSE: `___`  
  - MAE:  `___`  
  - R²:   `___`  
- Takeaways (typical):  
  - **Age** and **mileage** strongly reduce price.  
  - **Brand**, **transmission**, and sometimes **fuel type** shift price levels.  
- Predicted vs. Actual plot shows reasonable alignment with expected noise in used-car data.

---

## 5) Repository Structure
.
├─ data/
│ └─ used_cars.csv
├─ notebooks/
│ └─ 01_used_car_price_eda_modeling.ipynb
├─ README.md
└─ requirements.txt


---

## 6) How to Run
1. **Set up environment**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
Add data
Place your CSV at vehicles.csv.

Open the notebook
Run cells top-to-bottom.
If it’s slow on your machine, the notebook already includes fast settings:

smaller training sample cap (MAX_TRAIN),

only fast models (Ridge + compact HistGB),

ability to drop very high-cardinality columns during dev (e.g., model).

7) Assumptions & Limitations

Prices may include outliers, negotiated deals, and missing trims/options not captured by the dataset.

Feature engineering is intentionally lightweight (course-friendly) and focuses on core signals.

No claim of causality; this is predictive/associational modeling.

Results will vary by market, season, and data freshness.

8) Ethics & Responsible Use

Don’t use the model to justify unfair pricing. Treat outputs as decision support, not a final authority.

Be transparent: predictions reflect patterns in historical listings and may embed market biases.

9) References

Kaggle: Used Car / Craigslist vehicles datasets (acknowledge the specific Kaggle source used in class).

scikit-learn, pandas, seaborn, matplotlib documentation (standard Python data stack).

10) Quick Summary (1 paragraph)

This project cleans a large used-car dataset, visualizes key relationships, and trains fast baseline models to predict price. Age and mileage are the biggest drivers, while brand and transmission type shift price levels. A compact gradient-boosting model or a simple Ridge regressor provides solid baseline performance in seconds, meeting the course rubric without long grid searches. The notebook ends with a clear summary and ideas for improving accuracy (e.g., parsing trims/options, light NLP on descriptions, and targeted hyperparameter tuning).
