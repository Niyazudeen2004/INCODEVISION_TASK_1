# INCODEVISION
Data Cleaning and Preprocessing Pipeline (10,000 Rows)
Task 1 - #incodevision
Project Overview
This project focuses on the most critical step in the Data Science lifecycle: Data Cleaning and Preprocessing. Using a synthetic dataset of 10,000 rows generated to simulate "real-world" messiness, I developed a Python-based pipeline to transform raw, inconsistent data into a structured, analysis-ready format.

Technical Stack
Language: Python

Libraries: Pandas (Data Manipulation), NumPy (Numerical Operations), Seaborn/Matplotlib (Visualization)

Tool: Jupyter Notebook 

Phase 1: Messy Data Generation
To test the pipeline's robustness, I first created a script to generate 10,000 rows of "dirty" data. The dataset includes:

Inconsistent Text: Mixed casing and extra whitespaces in names and cities.

Mixed Data Types: Age represented as both integers and words (e.g., "twenty").

Inconsistent Dates: Various formats like YYYY-MM-DD, DD-MM-YYYY, and invalid dates like 2023-13-40.

Missing Values: Systematic NaN and None values across all columns.

Outliers: Randomly inserted "abc" or extremely high values in PurchaseAmount.

Phase 2: The Cleaning Pipeline
The pipeline follows a step-by-step logic to ensure data quality:

1. Standardization of Text
I used .str.strip() to remove leading/trailing spaces and .str.title() to ensure uniform casing for Name and City columns.

df["Name"] = df["Name"].str.strip().str.title()
df["City"] = df["City"].str.strip().str.title()

2. Numerical Conversion (Coercion)
Using pd.to_numeric with errors="coerce", I forced inconsistent entries (like "twenty") into NaN so they could be handled mathematically later.

df["Age"] = pd.to_numeric(df["Age"], errors="coerce")
df["PurchaseAmount"] = pd.to_numeric(df["PurchaseAmount"], errors="coerce")

3. Date Standardization
I unified the JoinDate column into a single datetime64 format. Any date that did not fit a real calendar (like the 13th month) was coerced to NaT.

df["JoinDate"] = pd.to_datetime(df["JoinDate"], format="%Y-%m-%d", errors="coerce")
4. Handling Missing Values (Imputation)

Instead of simply deleting data, I applied statistical imputation:

Numerical: Replaced nulls with the Median to avoid bias from outliers.

Categorical: Replaced nulls with the Mode (most frequent value).

5. Outlier Removal (IQR Method)
To ensure the data is ready for modeling, I applied the Interquartile Range (IQR) method to filter out extreme anomalies in Age and PurchaseAmount

q1 = df[col].quantile(0.25)
q3 = df[col].quantile(0.75)
iqr = q3 - q1
df = df[(df[col] >= (q1 - 1.5 * iqr)) & (df[col] <= (q3 + 1.5 * iqr))]

Key Learning Outcomes:

1.Data Integrity: Learned how to handle 10,000 rows without losing significant information.

2.Library Proficiency: Deepened my skills in Pandas for transformation and Seaborn for validating data distribution.

3.Efficiency: Automated a process that would take hours to do manually in Excel.

How to Run:

1.Clone this repository.

2.Ensure you have pandas, numpy, and seaborn installed.

3.Run the Jupyter Notebook TASK 1.ipynb.

4.The script will generate messy_dataset.csv and output a finalized cleaned_dataset.csv.

Contact: Niyazudeen Kamaludeen | www.linkedin.com/in/niyazudeen-kamaludeen
