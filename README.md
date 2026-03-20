# Azure_Project
## Azure Data Factory Pipeline: SQL to ADLS Gen2

This is an **end-to-end ADF pipeline** that extracts data from an **Azure SQL Database**, applies incremental loading using **CDC (Change Data Capture)**, and loads it into **ADLS Gen2** as Parquet files.  

Key features:
- Parameterized pipelines for multiple tables
- Incremental loading using CDC columns
- Dynamic folder and file naming
- Integration with **Logic Apps** for alerting
<img width="1138" height="362" alt="image" src="https://github.com/user-attachments/assets/5e583909-621c-4bf8-90b6-d20b5b84b492" />

## Pipeline Activities

This pipeline uses the following activities:

- ForEach (ForEach1) – Loop through multiple tables  
- Lookup (last_cdc) – Get last processed value  
- Set Variable (current) – Store current timestamp  
- Copy (AzureSql_to_Adlsgen2) – Load data from SQL to ADLS  
- If Condition (if_incremental_data) – Check if data is loaded  
- Delete (Delete_Empty_file) – Remove empty file  
- Script (max_cdc) – Get latest value from source  
- Copy (update_last_cdc) – Update latest value  
- Web Activity (Web1) – Send pipeline status  

---

## Flow

1. Loop tables using ForEach  
2. Get last value using Lookup  
3. Set current time  
4. Load data using Copy  
5. Check data using If Condition  
6.  
   - No data → Delete file  
   - Data → Update latest value  
7. Send notification using Web Activity  
