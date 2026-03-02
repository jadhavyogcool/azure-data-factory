# Azure Data Factory End-to-End Data Engineering Lab

## ETL & Transformation using Azure SQL and Mapping Data Flow

------------------------------------------------------------------------

## Project Overview

This hands-on lab demonstrates how to build a complete ETL pipeline
using:

-   Azure SQL Database
-   Azure Blob Storage
-   Azure Data Factory
-   Copy Activity
-   Mapping Data Flow (Spark-based transformation)

Students will implement filtering and derived column transformations and
load processed data into Azure SQL.

------------------------------------------------------------------------

## Architecture Diagram

    Local CSV File
          │
          ▼
    Azure Blob Storage
          │
          ▼
    Azure Data Factory
       ├── Copy Activity
       └── Mapping Data Flow (Spark)
               ├── Filter (Amount > 20000)
               └── Derived Column (GST)
          │
          ▼
    Azure SQL Database

------------------------------------------------------------------------

## Prerequisites

-   Azure Subscription
-   Basic understanding of SQL
-   Understanding of ETL concepts
-   Azure Portal access
-   Internet connection

------------------------------------------------------------------------

# Step 1: Create Azure SQL Database

## 1. Create Resource Group

-   Name: ADF-Demo-RG
-   Region: Central India

## 2. Create SQL Database

-   Database Name: SalesDB
-   Create New SQL Server
    -   Server Name: sales-sql-server-xxxxx (globally unique)
    -   Authentication: SQL Authentication
    -   Admin Username: sqladmin
    -   Strong Password

## 3. Networking Configuration

-   Public Endpoint: Enabled
-   Allow Azure Services: Enabled
-   Add Current Client IP: Enabled

------------------------------------------------------------------------

## Create Table

Run inside Query Editor:

    CREATE TABLE SalesData (
        CustomerID INT,
        CustomerName VARCHAR(100),
        City VARCHAR(100),
        Product VARCHAR(100),
        Amount INT
    );

------------------------------------------------------------------------

# Step 2: Create Azure Storage Account

-   Create Storage Account
-   Create container: sales-data
-   Upload file: sales_data.csv

Sample CSV:

    CustomerID,CustomerName,City,Product,Amount
    1,Amit Sharma,Mumbai,Laptop,75000
    2,Priya Singh,Delhi,Mobile,25000
    3,Rahul Verma,Pune,Tablet,30000
    4,Sneha Patil,Nashik,Monitor,15000
    5,Karan Mehta,Surat,Keyboard,2000

------------------------------------------------------------------------

# Step 3: Create Azure Data Factory

-   Create Data Factory
-   Launch Studio

------------------------------------------------------------------------

# Step 4: Create Linked Services

-   Azure Blob Storage
-   Azure SQL Database

Test connection before proceeding.

------------------------------------------------------------------------

# Step 5: Create Datasets

## Source Dataset

-   Type: Delimited Text
-   First row as header: Enabled

## Sink Dataset

-   Azure SQL Database
-   Table: SalesData

------------------------------------------------------------------------

# Step 6: Copy Data Pipeline

-   Add Copy Data Activity
-   Source → CSV
-   Sink → SQL Table
-   Debug → Publish → Trigger

------------------------------------------------------------------------

# Step 7: Mapping Data Flow Transformation

## Create New Pipeline

Name: PL_TransformSalesData

## Add Data Flow

Name: DF_SalesTransformation

### Add Source

Select CSV dataset

### Add Filter Transformation

Condition:

    Amount > 20000

### Add Derived Column

New Column:

    GST = Amount * 0.18

### Add Sink

Table Name:

    SalesData_Transformed

Enable Auto Create Table.

------------------------------------------------------------------------

# Validation

Run query:

    SELECT * FROM SalesData_Transformed;

Expected Result:

Only records with Amount \> 20000 and GST column added.

------------------------------------------------------------------------

# Troubleshooting Guide

  Issue                      Solution
  -------------------------- ---------------------------
  Login failed               Reset SQL server password
  Cannot connect             Check firewall rules
  Import schema failed       Ensure sink table exists
  Data preview not loading   Allow Azure services
  Column datatype issue      Verify dataset schema

------------------------------------------------------------------------




-   Monitoring and debugging pipelines

------------------------------------------------------------------------

# License

For educational purposes only.
