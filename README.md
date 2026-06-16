# BDA_Group_16
📁 Repository Structure

├── gun_violence_cleaned.csv   # Cleaned dataset (ready to use)
├── data_cleaning.rmp          # RapidMiner process file (data cleaning pipeline)
└── README.md                  # This file


📦 Original Dataset


Source: Gun Violence Archive
Downloaded from: Kaggle – jameslko/gun-violence-data
Coverage: January 2013 – March 2018
Raw size: 233,027 incidents, 29 columns



🧹 Data Cleaning Steps (Member 2)

Performed in RapidMiner using the following pipeline:

1. Import CSV


Loaded raw dataset using Read CSV operator
Comma separator, header row enabled


2. Select Attributes (Column Removal)

Removed 17 irrelevant columns, keeping only 12 useful features:

Kept ColumnsReasondateTemporal analysisstateGeographic featurecity_or_countyGeographic featuren_killedTarget-related, key metricn_injuredTarget-related, key metricn_guns_involvedWeapon featurecongressional_districtPolitical/geographic contextlatitude, longitudeGeospatial featuresincident_characteristicsIncident type classificationstate_house_districtRegional featurestate_senate_districtRegional feature

Dropped columns: address, incident_url, source_url, incident_url_fields_missing, notes, sources, location_description, gun_stolen, gun_type, incident_id, participant_name, participant_relationship, participant_age, participant_age_group, participant_gender, participant_status, participant_type

3. Replace Missing Values


Applied Replace Missing Values operator to all attributes
Numeric columns: replaced with average
Eliminated all ? values across the dataset


4. Generate Attributes (Severity Label)

Created a new target column severity using the following logic:

if(n_killed >= 4, "Mass Casualty",
   if(n_killed + n_injured >= 1, "Low Casualty",
      "No Casualty"))

5. Set Role


Set severity as the Label (target variable) for modelling



✅ Cleaned Dataset Summary


Rows: 233,027
Columns: 13 (12 features + 1 label)
Target variable: severity (Mass Casualty / Low Casualty / No Casualty)
Missing values: None



👥 Team Task Split

MemberRoleMember 1Abstract, Introduction (Background), Literature Review, Data Collection, Classification ModelMember 2Introduction (Problem Statement), Literature Review, Data Cleaning, Regression Model (victims killed)Member 3Introduction (Outline), Literature Review, EDA & Visualizations, Regression Model (victims injured), Conclusion, References, Appendix


⚠️ Notes for Teammates


Use gun_violence_cleaned.csv directly for your models — no need to redo cleaning
Open data_cleaning.rmp in RapidMiner to view the full cleaning pipeline
For EDA (Member 3): load the cleaned CSV and use Visualizations tab in RapidMiner
For models: use Set Role to set severity as label for classification, or n_killed/n_injured for regression
