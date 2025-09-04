# gtc-ml-project1-hotel-bookings

##  Project Overview
This project was completed as part of the **GTC Machine Learning Internship – Project 1**.  

Last-minute booking cancellations significantly impact hotel profitability.  
The goal of this project is **not to build the final prediction model**, but to **prepare raw hotel booking data** into a clean, structured, and machine-learning-ready format.  

This project is structured around **three phases**:  
1. Exploratory Data Analysis (EDA) & Data Quality Report  
2. Data Cleaning  
3. Feature Engineering & Preprocessing  

By the end, we produce a **clean dataset** split into train/test sets, ready for machine learning.  

---

## Dataset
- **Source**: `hotel_bookings.csv` (Property Management System dataset)  
- **Rows**: 119,390  
- **Columns**: 32  

The dataset contains booking details such as:  
- Hotel type, arrival dates, length of stay  
- Number of adults, children, babies  
- Special requests, deposit types, booking channels  
- Target variable: **`is_canceled`** (1 = booking canceled, 0 = not canceled)  

---

##  Phase 1: Exploratory Data Analysis
- Generated summary statistics (`.describe()`, `.info()`)  
- Detected missing values (notable in `children`, `country`, `agent`, `company`)  
- Visualized missingness with heatmaps  
- Outlier detection in numeric columns using:  
  - **Boxplots**  
  - **IQR method** (flagged outliers in `adr`, `lead_time`, `adults`, etc.)  

---

##  Phase 2: Data Cleaning
- **Missing Values**  
  - `children` → filled with `0` (then converted to int)  
  - `country` → imputed with mode (most frequent value)  
  - `agent` and `company` → filled with `0` (representing "None")  
- **Duplicates** → removed exact duplicates  
- **Outliers** → capped `adr` at `1000` to avoid extreme skew  
- **Data Types Fixed**  
  - Count-based variables → integers  
  - Continuous variables (`adr`) → float  
  - Categorical features (like `meal`, `deposit_type`) → category dtype  
  - Dates (`reservation_status_date`) → datetime  

---

##  Phase 3: Feature Engineering & Preprocessing
- **Removed Data Leakage**  
  - Dropped `reservation_status` and `reservation_status_date` 
- **Created New Features**  
  - `total_guests = adults + children + babies`  
  - `total_nights = stays_in_weekend_nights + stays_in_week_nights`  
  - `is_family = 1 if children or babies > 0 else 0`   
- **Encoding**  
  - One-Hot Encoding for low-cardinality categorical features  
  - Frequency Encoding for high-cardinality `country`  
- **Final Prep**  
  - Train-test split (`test_size=0.2`, `random_state=42`, stratified by target)  

---

## Project Structure
```

├── hotel_bookings.csv             # Raw dataset
├── GTC ML Project 1 - Data Cleaning & Preprocessing Challenge.ipynb   # Main notebook with all phases
├── README.md                     

```

