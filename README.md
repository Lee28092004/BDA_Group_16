# BDA Group 16 – Gun Violence Severity Prediction

**Module:** CT099-3-3 Knowledge Discovery and Big Data Analytics  
**Topic:** Gun Violence Incidents in the USA (2013–2018)  
**Tool:** RapidMiner | **Methodology:** CRISP-DM

---

## 📁 Repository Structure

```
BDA_Group_16/
├── gun_violence_cleaned.csv    # Cleaned dataset (ready to use)
├── data_cleaning.rmp           # RapidMiner process file
└── README.md                   # This file
```

## 📦 Original Dataset

**| Field | Details |**
| Source | [Gun Violence Archive](http://www.gunviolencearchive.org/) |
| Download | [Kaggle – jameslko/gun-violence-data](https://www.kaggle.com/jameslko/gun-violence-data) |
| Coverage | January 2013 – March 2018 |
| Raw size | 233,027 incidents, 29 columns |


## 🧹 Data Cleaning Steps (Member 2)

Performed in RapidMiner using the following pipeline:

### Step 1 – Import CSV
- Loaded raw dataset using `Read CSV` operator
- Comma separator, header row enabled, replace errors with missing values

### Step 2 – Select Attributes (Column Removal)

Removed 17 irrelevant columns, keeping 12 useful features:

**| Kept Column | Reason |**
| `date` | Temporal analysis |
| `state` | Geographic feature |
| `city_or_county` | Geographic feature |
| `n_killed` | Key target metric |
| `n_injured` | Key target metric |
| `n_guns_involved` | Weapon feature |
| `congressional_district` | Political/geographic context |
| `latitude` | Geospatial feature |
| `longitude` | Geospatial feature |
| `incident_characteristics` | Incident type classification |
| `state_house_district` | Regional feature |
| `state_senate_district` | Regional feature |

**Dropped:** `address`, `incident_url`, `source_url`, `incident_url_fields_missing`, `notes`, `sources`, `location_description`, `gun_stolen`, `gun_type`, `incident_id`, `participant_name`, `participant_relationship`, `participant_age`, `participant_age_group`, `participant_gender`, `participant_status`, `participant_type`

### Step 3 – Replace Missing Values
- Applied `Replace Missing Values` operator to all attributes
- Numeric columns: replaced with **average**
- Eliminated all `?` values across the dataset

### Step 4 – Generate Attributes (Severity Label)

Created a new column `severity` using:

```
if(n_killed >= 4, "Mass Casualty",
   if(n_killed + n_injured >= 1, "Low Casualty",
      "No Casualty"))
```

### Step 5 – Set Role
- Set `severity` as the **Label** (target variable) for modelling

---

## ✅ Cleaned Dataset Summary

**| Field | Value |**
| Rows | 233,027 |
| Columns | 13 (12 features + 1 label) |
| Target variable | `severity` (Mass Casualty / Low Casualty / No Casualty) |
| Missing values | None |

---

## 👥 Team Task Split

| Member | Tasks |
| Member 1 | Abstract, Introduction (Background), Literature Review, Data Collection & Selection, Classification Model (severity prediction), Results & Discussion|
| Member 2 | Introduction (Problem Statement), Literature Review, Data Cleaning & Preprocessing, Regression Model (victims killed), Results & Discussion |
| Member 3 | Introduction (Outline), Literature Review, EDA & Visualizations, Regression Model (victims injured), Results & Discussion, Conclusion |


## ⚠️ Notes for Teammates

- Use `gun_violence_cleaned.csv` directly for your models — no need to redo cleaning
- Open `data_cleaning.rmp` in RapidMiner to view the full cleaning pipeline
- **Member 3 (EDA):** Load the cleaned CSV and use the Visualizations tab in RapidMiner
- **For models:** Use `Set Role` to set `severity` as label for classification, or `n_killed`/`n_injured` as label for regression
