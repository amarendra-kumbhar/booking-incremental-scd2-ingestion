# Workflow Details: Booking.com Incremental SCD2 Merge Ingestion

## Overview
This document describes the workflow for processing daily booking and customer data using Databricks, PySpark, and Delta Lake with SCD2 (Slowly Changing Dimension Type 2) logic.

### Workflow Steps

1. **Read Daily Files**
   - Daily booking and customer data files are stored in DBFS.
   - A scheduled workflow triggers the PySpark notebook, passing the `current_date` parameter to read the data from DBFS.

2. **Data Transformation and Quality Checks**
   - The PySpark notebook performs data transformations on booking and customer data.
   - Data quality checks are applied using PyDeequ to ensure data integrity (e.g., completeness, uniqueness, non-negativity).

3. **SCD2 Type Merge**
   - The processed customer data is merged into a Delta table using SCD2 logic:
     - Ensures that only one active record per customer exists at any time.
     - Keeps a history of changes by closing previous records (`end_date`).

4. **Scheduled Workflow**
   - The entire ETL process is managed by a Databricks workflow configured using the `workflow_Json.json` file.
   - This workflow is scheduled to run daily, passing the necessary parameters for incremental data processing.

### Configuration Details
- **Workflow JSON File:** The workflow configuration file (`workflow_Json.json`) specifies the task details, notebook path, parameters, and cluster settings for the daily ETL job.
- **Notebook Path:** `/Workspace/Users/amarendrakumbhar123@gmail.com/booking_data_processing`

### Additional Notes
- Ensure that all required libraries (e.g., PySpark, PyDeequ) are installed in your Databricks environment.
- Monitor the workflow using Databricks job logs to detect any issues in data processing.
