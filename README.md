# Free and Low-Cost Food Programs Data Analytics Pipeline

## **Project Overview**

This project focuses on creating a complete Data Analytics Pipeline (DAP) for analyzing **Free and Low-Cost Food Programs** in Vancouver, leveraging various AWS services. The pipeline covers all essential stages, including data ingestion, profiling, cleaning, enrichment, protection, governance, and observability.

## **Objective**

The objective of this project is to design a scalable data pipeline that processes, analyzes, and visualizes data related to free and low-cost food programs. The aim is to uncover insights such as service availability, geographic coverage, and program accessibility.

## **Dataset Description**

- **Source:** [Vancouver Open Data Platform](https://opendata.vancouver.ca/explore/dataset/free-and-low-cost-food-programs/information/?sort=program_name)
- **Key Features:**
  - Program Name
  - Description
  - Program Status
  - Organization Name
  - Program Population Served
  - Address Extra Info
  - Location Address
  - Local Areas
  - Provides Meals
  - Provides Hampers
  - Delivery Available
  - Takeout Available
  - Wheelchair Accessible
  - Meal Cost
  - Hamper Cost

## **Methodology**

### **1. Data Ingestion**

- Created S3 bucket `opendata-flcfp-raw-msk`.
- Uploaded raw dataset `free-and-low-cost-food-programs.xlsx`.

![Data Ingestion](https://muhammadshahzebkhan-msk.github.io/Data-Analyst/image.png)


### **2. Data Profiling**

- Used **AWS Glue DataBrew** for profiling.
- Extracted statistics such as null values, data types, and distributions.
- Stored profiling results in S3 (`opendata-flcfp-trf-msk/Data-Profiling`).

### **3. Data Cleaning**

- Applied 22 transformations using AWS Glue DataBrew.
- Stored cleaned data in two formats:
  - Parquet with Snappy compression (system folder).
  - CSV (user folder).
- Organized data by `Local Areas`.

### **4. Data Pipeline Design**

- Built an **AWS Glue** ETL pipeline for descriptive and exploratory analysis.
- Dropped irrelevant columns and calculated counts per local area.
- Stored final outputs in S3 (`opendata-flcfp-trf-msk/Descriptive & Exploratory`).

### **5. Data Enriching**

- Created a secure virtual network and configured an instance for data collection.
- Merged user activity data into the dataset using DynamoDB, Athena, and crawlers.

### **6. Data Protection**

- Applied **AWS KMS (Key Management Service)** for data encryption.
- Created automated S3 bucket backups for disaster recovery.

### **7. Data Governance**

- Designed a data quality pipeline with rules for uniqueness and completeness.
- Stored validated datasets in S3 (`Quality Folder`).

### **8. Data Observability**

- Monitored pipeline activities using **Amazon CloudWatch** alarms.
- Built custom dashboards for real-time monitoring.

## **Tools & Technologies**

- **Data Storage:** Amazon S3
- **Data Processing:** AWS Glue, AWS Glue DataBrew, Amazon Athena
- **Data Monitoring:** Amazon CloudWatch, Amazon CloudTrail
- **Data Security:** AWS KMS, IAM Roles
- **Data Visualization:** QuickSight, Custom Dashboards

## **Deliverables**

- Processed datasets (CSV, Parquet formats).
- Fully automated ETL pipeline.
- Data visualization dashboards.
- Comprehensive project documentation.

## **Key Insights and Findings**

- Identified geographic disparities in food program availability.
- Highlighted areas with limited meal-providing services.
- Enabled better decision-making through comprehensive data analysis.

---

### **How to Access the Project**

1. Clone the repository.
2. Explore project files, including code, datasets, and detailed documentation.
3. Review the `data_analysis.ipynb` notebook for analysis steps.
4. Use the provided SQL queries for custom data exploration.


# Free and Low-Cost Food Programs Data Analysis

## **Project Description**

This project involves analyzing free and low-cost food programs in Vancouver to uncover patterns, trends, and insights. We will focus on geographic coverage, the number of food programs in each local area, and the types of organizations providing meals. Two separate pipelines have been created for the **Descriptive Analysis** and **Exploratory Data Analysis (EDA)** to better understand the data and provide actionable insights.

## **Objective**

The primary goal of this project is to:
1. **Descriptive Analysis**: Count how many food programs are available in each local area.
2. **Exploratory Data Analysis (EDA)**: Further explore how many organizations are providing free meals in each area.

Both analyses involve data cleaning, transformation, and visualization to explore these trends.

## **Dataset Description**

The dataset contains information about different free and low-cost food programs in Vancouver. Each entry includes:

- **Program Name**: The name of the program.
- **Description**: Details about the program's services.
- **Program Status**: Whether the program is open or closed.
- **Organization Name**: The organization operating the program.
- **Program Population Served**: Information about the target population served by the program.
- **Address Extra Info**: Additional location details.
- **Location Address**: Full address of the program.
- **Local Areas**: Areas or neighborhoods served by the program.
- **Provides Meals**: Whether the program offers meals (True/False).
- **Provides Hampers**: Whether the program offers food hampers (True/False).
- **Delivery Available**: Availability of delivery service (Yes/No).
- **Takeout Available**: Availability of takeout (Yes/No).
- **Wheelchair Accessible**: Accessibility for individuals with disabilities (Yes/No).
- **Meal Cost**: The cost of meals provided (e.g., Free, Low cost).
- **Hamper Cost**: The cost of hampers provided (e.g., Free, Low cost).

## **Methodology**

### **Descriptive Analysis Pipeline**

1. **Goal**: Count how many food programs are available in each local area.
2. **Steps**:
    - **Data Cleaning**: Filter out rows with missing or irrelevant values in key columns (e.g., Local Areas, Program Status).
    - **Data Transformation**: Group data by **Local Areas** and count the number of food programs in each area.
    - **Visualization**: Generate a bar plot showing the number of food programs per local area.
    - **Output**: A summary table and bar plot showing the distribution of programs by area.

   Example code for Descriptive Analysis:

   ```python
   # Descriptive Analysis Pipeline
   import pandas as pd
   import matplotlib.pyplot as plt

   # Load data
   df = pd.read_csv("food_programs.csv")

   # Clean data
   df_cleaned = df.dropna(subset=['Local Areas'])

   # Count programs in each local area
   program_count = df_cleaned.groupby('Local Areas')['Program Name'].count()

   # Visualize the data
   program_count.plot(kind='bar', figsize=(10, 6), color='skyblue')
   plt.title("Number of Food Programs per Local Area")
   plt.ylabel("Number of Programs")
   plt.xticks(rotation=45)
   plt.show()


