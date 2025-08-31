# Bosch Production Line Performance: Defect Prediction


## Description

This project aims to predict manufacturing defects using the Bosch Production Line Performance dataset. Leveraging machine learning techniques, the goal is to identify products likely to be defective based on sensor measurements and process data collected throughout the production line. This predictive model can help optimize manufacturing processes, reduce waste, and improve product quality.



## Data

The project utilizes the **Bosch Production Line Performance** dataset. This dataset is characterized by:

*   **High Dimensionality:** It contains a vast number of features collected from various sensor measurements and process parameters across different stations and levels of the production line.
*   **Sparsity:** A significant portion of the data is missing, which is often indicative of products not passing through certain stations or measurements not being applicable.
*   **Severe Class Imbalance:** The target variable ('Response'), indicating whether a product is defective (1) or not (0), is highly imbalanced, with defective products representing a very small percentage of the total.

Due to the large size and sparsity of the original dataset, the initial data loading process involved:

*   **Stratified Sampling:** A smaller, representative sample of the data was created using stratified sampling based on the 'Response' variable to maintain the class distribution.
*   **Loading in Chunks:** The large raw data files were read in chunks to manage memory usage efficiently.

This initial data handling and sampling process is detailed in the notebook: `Handling_data_in_stratified_chunks_sampled_merged_bosch.ipynb`.



## Exploratory Data Analysis (EDA) Summary

The exploratory data analysis on the sampled Bosch Production Line Performance dataset provided crucial insights for subsequent feature engineering and modeling. Key findings include:

*   **Column Meanings:** Based on the column naming conventions (`L#_S#_F#`, `L#_S#_D#`), features likely represent measurements or timestamps at different **Levels (L#)** and **Stations (S#)**. However, detailed descriptions of specific features (`F#` or `D#`) were not available.
*   **Missing Values:** Missing data is widespread, particularly in features from stations L0, L1, and L3. **Interpreting missingness is critical:** in many cases, it likely signifies that a product did not visit a specific station or that a measurement was not applicable, rather than a data error. Features with 100% missing values were identified.
*   **Numeric Features:**
    *   Features with zero or very low variance were identified.
    *   Correlations with the 'Response' variable were generally low to moderate, suggesting complex, potentially non-linear relationships.
    *   Distributions of numeric features varied.
*   **Categorical Features:**
    *   Features were classified by cardinality (low, moderate, high), with high cardinality being a significant characteristic.
    *   Chi-Squared tests showed limited statistically significant associations with 'Response' for low to moderate cardinality features.
    *   Analysis of Mean 'Response' per Category identified low cardinality features with specific categories exhibiting notably higher defect rates than the overall average.
*   **Date-Originated Features:**
    *   Engineered simple temporal features (earliest/latest timestamp, timestamp count per product) showed differing distributions between defective and non-defective products.
    *   Temporal patterns in the defect rate over time were observed, indicating the time dimension is important.
*   **Station-Related Features:**
    *   Features were grouped by station, revealing a significant imbalance in feature counts (L1 having the most).
    *   Missingness patterns varied considerably across stations, with L2 having minimal missing data compared to L0, L1, and L3.
    *   Analysis of feature correlation within stations showed varying levels of interdependencies.

These insights highlight the data's challenges (sparsity, imbalance, high cardinality) and guide the approach for feature engineering and model selection.



## Next Steps

Following the exploratory data analysis, the next steps for this project include:

1.  **Feature Engineering and Preprocessing:** Implement the strategies identified during EDA to handle missing values, encode categorical features (including specialized techniques for high cardinality features), engineer temporal features from the date columns, and apply feature selection or dimensionality reduction techniques.
2.  **Model Selection:** Evaluate different modeling approaches suitable for imbalanced, sparse, and high-dimensional data (e.g., tree-based models).
3.  **Model Training and Evaluation:** Train the selected model(s) on the prepared data, using appropriate evaluation metrics for imbalanced classification (e.g., Precision, Recall, F1-score, AUC-PR) and cross-validation.
4.  **Hyperparameter Tuning:** Optimize the performance of the chosen model(s) through hyperparameter tuning.
5.  **Deployment:** Aim Plus


## Directory Structure

/
├── datasets/                      # Contains raw and processed data
│   ├── data/                      # Empty placeholder for original 14 GB dataset
│   └── processed_data/            # Contains processed CSV files
│       ├── cat_sampled.csv
│       ├── date_sampled.csv
│       ├── merged_sampled.csv
│       └── num_sampled.csv
├── images/                        # Folder for storing visual assets,images included but not listed here for brevity
│   
├── notebooks/                     # Jupyter notebooks for data handling and analysis
│   ├── Handling_data_in_stratified_chunks_sampled_merged_bosch.ipynb
│   └── EDA_bosch.ipynb
└── README.md                      # Project overview and instructions



**Notes to Directory Structure**

- `datasets/`: This folder has two folders - data and processed_data. data/ is intentionally left empty. The original dataset is approximately 14 GB and should be placed here manually, if you want.
- `processed_data/`: Contains cleaned, sampled, and merged versions of the original data for easier and ready made handling and analysis without the original dataset.
- `images/`: Stores visualizations, plots, and other graphical assets.
- `notebooks/`: Includes Jupyter notebooks used for inital data handling, data exploration, preprocessing, and modeling.

## Getting Started

- The notebook `Handling_data_in_stratified_chunks_sampled_merged_bosch.ipynb` has already been configured and executed using Kaggle API credentials. It accesses the Bosch dataset without downloading the full 14 GB file.

- All necessary steps — including setting up the Kaggle token, installing the CLI, and selectively accessing data — have been completed within the notebook- Handling_data_in_stratified_chunks_sampled_merged_bosch.ipynb itself.

- No manual setup is required to rerun the notebook, provided the Kaggle token is available.

- To begin working with this project:
1. Use the notebooks in `notebooks/` to handle, process and analyze the data.
3. Refer to `processed_data/` for ready-to-use data files.

## Notes

- Ensure you have sufficient disk space before downloading the full dataset.
- All processing steps are documented in the notebooks.

