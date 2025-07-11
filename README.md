# California Wildfire Analysis and Prediction

## Project Overview

The goal of this project is to conduct a comprehensive data mining analysis on California wildfires to understand contributing factors and build predictive models for wildfire size classification. The project integrates diverse datasets, including wildfire records, historical temperatures, unemployment rates, and population statistics, to create a rich analytical base. A key focus is on addressing the significant class imbalance in the target variable (`FIRE_SIZE_CLASS`) using the SMOTE (Synthetic Minority Over-sampling Technique) to improve model performance.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset](#dataset)
3. [Tools & Technologies](#tools--technologies)
4. [Exploratory Data Analysis & Visualizations](#exploratory-data-analysis--visualizations)
5. [Key Findings & Insights](#key-findings--insights)
6. [Methodology](#methodology)
7. [Setup & Usage](#setup--usage)
8. [Project Structure](#project-structure)
9. [Contact](#contact)

## Dataset
The analysis consolidates data from four primary sources:
- **`CaliforniaWildfiresFIPS.csv`**: Contains records of wildfires in California from 1992-2015.
- [**`GlobalLandTemperaturesByState.csv`**](https://www.kaggle.com/datasets/berkeleyearth/climate-change-earth-surface-temperature-data): Historical average temperature data by state.
- **`Unemployment_US.csv`**: Unemployment rates by US county.
- **`population_by_county_1970_to_2018.csv`**: Yearly population data for California counties.

### Key Fields
*   **Wildfire Details**: `FIRE_SIZE`, `DISCOVERY_DATE`, `LATITUDE`, `LONGITUDE`, `STATE`, `FIPS_NAME` (County)
*   **Cause & Ownership**: `STAT_CAUSE_DESCR`, `OWNER_DESCR`
*   **External Factors**: `AverageTemperature`, `Rate` (Unemployment), `Population`
*   **Target Variable**: `FIRE_SIZE_CLASS` (Categorical representation of fire size, from A to G)

## Tools & Technologies
- **Data Analysis & Machine Learning**: Python 3 (with pandas, numpy, scikit-learn)
- **Data Visualization**: Matplotlib, Seaborn
- **Class Imbalance**: imbalanced-learn

![Python Logo](https://img.icons8.com/color/96/python--v1.png) ![Pandas Logo](https://img.icons8.com/color/96/pandas.png) 

## Key Findings & Insights
The analysis revealed several critical factors related to California wildfires:
- **Most Frequent Causes**: The most common cause of wildfires is categorized as "Miscellaneous," followed by lightning and equipment use. This suggests a wide variety of human and natural factors contribute to fire ignitions.
- **Seasonal Trends**: Wildfire frequency and total area burned peak during the summer months (June, July, August), which aligns with hotter and drier weather conditions.
- **Daily Patterns**: Fires are most frequently discovered in the afternoon, likely due to a combination of peak daily temperatures and increased human activity.
- **Class Imbalance**: The dataset is heavily skewed towards smaller fires (Classes A and B), making it challenging for models to predict larger, less frequent fire classes without resampling techniques.
- **Feature Importance**: The Random Forest model identified **Population**, **Latitude**, **Longitude**, and **Average Temperature** as the most significant predictors of wildfire size class. This highlights the strong interplay between geographic, climatic, and demographic factors.

## Methodology
The project follows a structured data mining workflow:
1.  **Data Loading & Initial Cleaning**: Loads the four datasets and performs initial cleaning, including handling missing values and removing duplicates.
2.  **Feature Engineering**:
    *   Converts wildfire discovery dates from Julian format to standard datetime objects.
    *   Extracts `MONTH`, `DAY_OF_WEEK`, and `PART_OF_DAY` as new features.
3.  **Data Integration**: Merges the wildfire, temperature, unemployment, and population datasets into a single comprehensive DataFrame. Missing values introduced during joins are imputed using yearly means.
4.  **Outlier Handling**: Normalizes numerical data using z-scores and removes outliers based on z-score thresholds and the Interquartile Range (IQR) method.
5.  **Model Preparation**:
    *   **Label Encoding**: Converts all categorical features into numerical format for modeling.
    *   **Class Imbalance Handling**: Reduces the number of target classes to simplify the problem and applies **SMOTE (Synthetic Minority Over-sampling Technique)** on the training data to create a balanced dataset.
    *   **Data Splitting**: Splits the data into stratified training (60%) and testing (40%) sets.
6.  **Predictive Modeling**:
    *   Builds and evaluates **Decision Tree** and **Random Forest** classifiers.
    *   Performance is measured using accuracy, a detailed classification report (precision, recall, F1-score), and a confusion matrix.

## Setup & Usage
To replicate this project locally:
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/shrististha/investigating-wildfire-severity-using-data-mining-and-machine
    cd investigating-wildfire-severity-using-data-mining-and-machine
    ```
2.  **Set up a Python environment:**
    ```bash
    python -m venv env
    source env/bin/activate  # On Windows: .\env\Scripts\activate
    ```
3.  **Execution**: Open and run the `Data_Mining_Project.ipynb` notebook. Cells should be run sequentially to ensure the data processing pipeline executes correctly. The notebook will generate analysis, visualizations, and model performance metrics.

## Project Structure
```
 investigating-wildfire-severity-using-data-mining-and-machine/
└── Data_Mining_Project.ipynb        # Main Jupyter notebook with all analysis
```

## Contact
*(Shristi Shrestha)* - [GitHub](https://github.com/shrististha) | [LinkedIn](https://linkedin.com/in/shristi-stha)
