# California Wildfire Analysis and Prediction

This repository contains a Jupyter Notebook that performs a comprehensive data mining project on California wildfires. The project aims to preprocess, merge, and analyze a diverse set of data to understand the factors contributing to wildfires and to build predictive models for wildfire size classification.

## Project Overview

The goal of this project is to conduct a comprehensive data mining analysis on California wildfires to understand contributing factors and build predictive models for wildfire size classification. The project integrates diverse datasets, including wildfire records, historical temperatures, unemployment rates, and population statistics, to create a rich analytical base. A key focus is on addressing the significant class imbalance in the target variable (`FIRE_SIZE_CLASS`) using the SMOTE (Synthetic Minority Over-sampling Technique) to improve model performance.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset](#dataset)
3. [Tools & Technologies](#tools--technologies)
4. [Key Findings & Insights](#key-findings--insights)
5. [Methodology](#methodology)
6. [Setup](#setup)
7. [Project Structure](#project-structure)
8. [Contact](#contact)

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

### 1. Data Loading & Preprocessing
- **Libraries**: Imports standard data science libraries including `pandas`, `numpy`, `matplotlib`, `seaborn`, and `sklearn`.
- **Initial Loading**: Loads the four datasets into pandas DataFrames.
- **Feature Engineering**:
    - Converts the wildfire `DISCOVERY_DATE` from Julian format to a standard datetime object.
    - Extracts new features like `MONTH`, `DAY_OF_WEEK`, and `PART_OF_DAY` from the discovery date and time.
    - Drops original time/date columns after feature extraction.
- **Initial Cleaning**:
    - Handles missing values from the initial datasets.
    - Removes duplicate records to ensure data quality.

### 2. Exploratory Data Analysis (EDA)
- **Summary Statistics**: Uses `describe()` to get a high-level statistical overview of the data.
- **Visualizations**:
    - Bar charts are used to visualize the frequency of fires by `PART_OF_DAY` and `MONTH`.
    - Pie charts illustrate the distribution of wildfire causes (`STAT_CAUSE_DESCR`) and their contribution to the total area burned.

### 3. Data Integration
- **Filtering**: The temperature, unemployment, and population datasets are filtered to match the temporal (1992-2015) and geographical (California) scope of the wildfire data.
- **Join Columns**: Composite keys (e.g., `Year-Month-County`) are created in each DataFrame to facilitate accurate merging.
- **Merging**: The wildfire DataFrame is progressively merged with the temperature, unemployment, and population data, creating a single, comprehensive dataset.
- **Post-Merge Cleaning**: Missing values introduced during the left joins (e.g., missing temperature or unemployment data for a specific month) are imputed using the yearly mean for that column. Population data is converted to a numeric type.

### 4. Outlier Handling
- A custom function is used to normalize numerical data using the z-score.
- Outliers are then identified and removed using a combination of z-score thresholds and the Interquartile Range (IQR) method to create a more robust dataset for modeling.

### 5. Model Preparation
- **Label Encoding**: All categorical features (e.g., `STAT_CAUSE_DESCR`, `OWNER_DESCR`, `FIPS_NAME`) are converted into numerical representations using `sklearn.preprocessing.LabelEncoder`.
- **Class Imbalance Handling**:
    - The target variable, `FIRE_SIZE_CLASS`, is highly imbalanced. The notebook experiments with reducing the number of classes (from 7 down to 5, 3, and finally 2) to simplify the classification task.
    - The **SMOTE (Synthetic Minority Over-sampling TEchnique)** is applied to the *training data* after splitting to create synthetic samples for the minority classes, resulting in a balanced dataset for model training.
- **Data Splitting**: The dataset is split into training (60%) and testing (40%) sets using `train_test_split`, with stratification to maintain the class distribution in both sets.

### 6. Predictive Modeling
- **Models**: Several classification algorithms are implemented and evaluated:
    - **Decision Tree Classifier**
    - **Random Forest Classifier**
- **Evaluation**: Each model's performance is assessed using:
    - **Accuracy Score**: The proportion of correctly classified instances.
    - **Classification Report**: Provides precision, recall, and F1-score for each class.
    - **Confusion Matrix**: Visualizes the model's performance, showing correct vs. incorrect predictions for each class.
- **Feature Importance**: The Random Forest model is used to extract and rank the importance of each feature in predicting the fire size class.

## Setup

1.  **Prerequisites**: Ensure you have Python and the following libraries installed:
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn mlxtend
    ```

2.  **Dataset Location**: Place the four required CSV files in the same directory as the notebook or update the file paths in the data loading cells.

3.  **Execution**: Run the Jupyter Notebook cells sequentially from top to bottom. The notebook is structured to be executed in order, as later cells depend on the transformations and DataFrames created in earlier ones.

4.  **Output**: The notebook will generate various plots for EDA, and at the end, it will output the performance metrics and confusion matrices for the trained machine learning models. It also saves the final preprocessed and balanced training data (`train.csv`, `train3.csv`) and the corresponding test data (`test.csv`, `test3.csv`).

## Project Structure
```
 investigating-wildfire-severity-using-data-mining-and-machine/
└── Data_Mining_Project.ipynb        # Main Jupyter notebook with all analysis
```

## Contact
*(Shristi Shrestha)* - [GitHub](https://github.com/shrististha) | [LinkedIn](https://linkedin.com/in/shristi-stha)
