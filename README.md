# Data Analysis of Funding Projects in Mozambique (2016-2024)

This notebook analyzes funding, funding partners, and implementing partners of projects in Mozambique from 2016 to 2024. The data, compiled by the Health Partners Group (HPG), is used to facilitate communication and collaboration.  **Note:** This analysis excludes humanitarian projects and users should independently verify all information.

## 1. Data Cleaning and Preparation

### 1.1 Importing Libraries and Loading Dataset

The following libraries are used for data manipulation, visualization, and currency conversion:

- pandas
- numpy
- matplotlib
- seaborn
- forex-python
- requests

The dataset used in this analysis is available at [link to dataset](https://airtable.com/appxtAORRsJnCzZzJ/tbltG2FWrHZLm7bsO/viwGBlm2uYqMNfuvK?blocks=hide)

### 1.2 Data Overview and Initial Exploration

- The dataset contains 153 rows and 23 columns.
- Various currencies are present in the 'Currency' column, requiring conversion to USD.
- Descriptive statistics are computed to understand data distributions.
- A line plot shows the trend of 'Total Value of Project'.
- Data types are examined using `df.info()`.

### 1.3 Handling Missing Values

- Missing values are identified and visualized using a horizontal bar chart.
- Projects with missing start dates are observed.
- Duplicate project names are checked.  There are multiple instances where project names are the same but implemented by different partners.

### 1.4 Data Standardization

- **Column Renaming:** Years columns ('Year Started', 'Year Ending (Estimate)', and 'Total Value of Project') are renamed for clarity.
- **Year Conversion:** 'Start Date' and 'Estimated End Date' are converted to datetime format.
- **Currency Conversion:** All currencies are converted to USD using the `exchangerate-api.com`.
- **District Column:** The dataset is reshaped to create a separate 'District' column from province columns.  Empty cells are filled with 'Not Specified' to indicate that the districts were not specified by the funding partners.
- **Unique Project Names:**  Unique project names are created to avoid confusion due to duplicated project names but different implementing partners. 


### 1.5 Data Subsetting and Export

- Relevant columns for visualization are selected and saved into a new dataframe `df_reshaped`.
- The cleaned and prepared dataset (`df_reshaped`) is exported as 'cleaned_dataset_viz.csv' for future visualizations.

## 2. Data Analysis and Feature Engineering

### 2.1 Project Count per Province

- Calculates the number of projects in each province. Takes into account if the partner specified districts or not.

### 2.2 Average Funding per Province

- Calculates the average funding amount per province.  Similar to the project counting, it only considers projects with specified districts or when the partner didn't provide districts.

### 2.3 Final Dataset Preparation

- The calculated average funding per province is added as a new column, "Average Funding", to the main dataframe.
- This final dataframe (`df_final`) is saved as 'final_dataset.csv'.
