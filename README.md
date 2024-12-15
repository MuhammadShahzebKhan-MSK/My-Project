# Free and Low-Cost Food Programs Data Analytics Pipeline

Project Overview

This project focuses on creating a complete Data Analytics Pipeline (DAP) for analyzing Free and Low-Cost Food Programs in Vancouver, leveraging various AWS services. The pipeline covers all essential stages, including data ingestion, profiling, cleaning, enrichment, protection, governance, and observability.

Objective

The objective of this project is to design a scalable data pipeline that processes, analyzes, and visualizes data related to free and low-cost food programs. The aim is to uncover insights such as service availability, geographic coverage, and program accessibility.

Dataset Description

Source: Vancouver Open Data Platform
![Vancouver Open Data Platform](https://muhammadshahzebkhan-msk.github.io/Data-Analyst/Screenshot%202024-11-25%20115149.png)
Key Features:

Program Name
Data Analytical Platform (DAP)
Description: Explain in below DAP Image
![Description: Explain in below DAP Image](https://muhammadshahzebkhan-msk.github.io/Data-Analyst/image.png)

Program Status

Organization Name

Program Population Served

Address Extra Info

Location Address

Local Areas

Provides Meals

Provides Hampers

Delivery Available

Takeout Available

Wheelchair Accessible

Meal Cost

Hamper Cost

Methodology

1. Data Ingestion

Created S3 bucket opendata-flcfp-raw-msk.

Uploaded raw dataset free-and-low-cost-food-programs.xlsx.

2. Data Profiling

Used AWS Glue DataBrew for profiling.

Extracted statistics such as null values, data types, and distributions.

Stored profiling results in S3 (opendata-flcfp-trf-msk/Data-Profiling).

3. Data Cleaning

Applied 22 transformations using AWS Glue DataBrew.

Stored cleaned data in two formats:

Parquet with Snappy compression (system folder).

CSV (user folder).

Organized data by Local Areas.

4. Data Pipeline Design

Built an AWS Glue ETL pipeline for descriptive and exploratory analysis.

Dropped irrelevant columns and calculated counts per local area.

Stored final outputs in S3 (opendata-flcfp-trf-msk/Descriptive & Exploratory).

5. Data Enriching

Created a secure virtual network and configured an instance for data collection.

Merged user activity data into the dataset using DynamoDB, Athena, and crawlers.

6. Data Protection

Applied AWS KMS (Key Management Service) for data encryption.

Created automated S3 bucket backups for disaster recovery.

7. Data Governance

Designed a data quality pipeline with rules for uniqueness and completeness.

Stored validated datasets in S3 (Quality Folder).

8. Data Observability

Monitored pipeline activities using Amazon CloudWatch alarms.

Built custom dashboards for real-time monitoring.

Tools & Technologies

Data Storage: Amazon S3

Data Processing: AWS Glue, AWS Glue DataBrew, Amazon Athena

Data Monitoring: Amazon CloudWatch, Amazon CloudTrail

Data Security: AWS KMS, IAM Roles

Data Visualization: QuickSight, Custom Dashboards

Deliverables

Processed datasets (CSV, Parquet formats).

Fully automated ETL pipeline.

Data visualization dashboards.

Comprehensive project documentation.

Key Insights and Findings

Identified geographic disparities in food program availability.

Highlighted areas with limited meal-providing services.

Enabled better decision-making through comprehensive data analysis.
