# Azure Data Factory – dfproadfs

This repository contains Azure Data Factory assets (pipelines, datasets, data flows) from the **dfproadfs** Data Factory instance.

## Overview

- Data Factory name: **dfproadfs**  
- Branch: `main` (Git integration enabled in the ADF UI).
- Main focus: Ingestion into Delta Lake, REST API integrations, scheduled processing, and schema management.


- This Data Factory orchestrates ingestion of source data into Delta Lake, exposes REST API–based data integrations, and runs scheduled pipelines for downstream analytics.

## Repository structure

Adapt this to your repo layout:

- `pipelines/` – JSON definitions of all pipelines (Deltalake, demo, Ingestion, RESTAPI, Router, Scheduled, Schema).  
- `datasets/` – Dataset JSONs referenced by pipelines.  
- `dataflows/` – Mapping Data Flow definitions (currently 1 data flow).
- `linkedServices/` – Linked service configurations (without secrets).  
- `docs/` – Documentation and screenshots.

## Pipelines

Below are the pipelines detected in your factory.  
Adjust each description to match exactly what your pipeline does.

### 1. `Deltalake`

- Purpose: Ingest data into Delta Lake tables (bronze/silver/gold layers – update as needed).  
- Typical activities:
  - Copy data from source systems to Data Lake / Delta format.
  - Optional Data Flow or stored procedure activities for transformations.
- Triggers: Scheduled (daily/hourly) or event‑based (update as needed).
<img width="1857" height="827" alt="image" src="https://github.com/user-attachments/assets/ee9f03df-d605-4d07-b353-9ae855ab2116" />


### 2. `demo`

- Purpose: Demo or sample pipeline used for testing, POCs, or training.  
- Typical activities:
  - Simple copy or lookup activities to showcase ADF features.
  - May include parameters to demonstrate dynamic pipelines.
- Triggers: Usually manual (debug runs) or ad‑hoc.

### 3. `Ingestion`

- Purpose: Central ingestion pipeline that loads raw data from multiple sources into a landing/raw zone.  
- Typical activities:
  - Multiple copy activities for different sources (SQL, files, APIs).
  - Logging and error‑handling activities.
- Triggers: Daily or near‑real-time ingestion (update as needed).
<img width="1828" height="632" alt="image" src="https://github.com/user-attachments/assets/7fbc70a2-07ee-437e-bc1c-f8cc2aabb8c0" />


### 4. `RESTAPI`

- Purpose: Integrate with REST APIs to pull or push data.  
- Typical activities:
  - Web / REST connector activities calling external APIs.
  - Pagination and parameterization for dynamic endpoints.
  - Writing API responses to storage or databases.
- Triggers: Scheduled or event-based (e.g., every 15 minutes – update as needed).
<img width="1811" height="776" alt="image" src="https://github.com/user-attachments/assets/b690302a-eda9-4b5c-87a3-6df3dc2db08b" />


### 5. `Router`

- Purpose: Routing/ orchestration pipeline that decides which downstream pipelines to run based on conditions.  
- Typical activities:
  - If/Else, Switch, or Filter activities.
  - Invoking other pipelines using Execute Pipeline activities.
  - Handling *fan‑out* or *fan‑in* patterns.
- Triggers: Called by other pipelines or scheduled as a controller pipeline.
<img width="1827" height="722" alt="image" src="https://github.com/user-attachments/assets/c8a5b506-e70f-4222-b7b9-33dccc13a740" />


### 6. `Scheduled`

- Purpose: Consolidated pipeline for scheduled jobs (batch processing, housekeeping, daily loads).  
- Typical activities:
  - Execute pipeline activities for ingestion, transformations, and reporting.
  - Time‑based logic (e.g., using system variables for date ranges).
- Triggers: Cron‑like schedules (daily, weekly, monthly – update as needed).
<img width="1516" height="737" alt="image" src="https://github.com/user-attachments/assets/6b506f7d-a9a4-44f8-ab34-61a3793d6888" />


### 7. `Schema`

- Purpose: Schema management and metadata‑driven operations.  
- Typical activities:
  - Activities to manage table structures (DDL), schema evolution, or metadata tables.
  - Possible integration with Delta Lake schema updates.
- Triggers: On‑demand or during releases/migrations (update as needed).
<img width="1475" height="670" alt="image" src="https://github.com/user-attachments/assets/e783f468-d448-45c9-bcfd-01b072481084" />

## Datasets

Your factory currently has 8 datasets.
Document key datasets here; example structure:

- `DS_Source_SQL`: Source SQL table/view used in Ingestion.  
- `DS_Delta_Bronze`: Delta Lake bronze table for raw data.  
- `DS_Delta_Silver`: Curated Delta Lake table after transformations.  
- `DS_RESTAPI_Response`: Storage location for API responses.

Update names and purposes to match your actual datasets.

## Data flows

Your factory has 1 data flow.
Describe it here:

- `DF_MainTransform` (replace with actual name):
  - Performs transformations (joins, filters, aggregations) on ingested data.
  - Writes output to curated tables or Delta Lake layers.

## Linked services

Document only non‑secret information:

- `LS_AzureSqlDb`: Azure SQL Database (connection details stored in Key Vault).  
- `LS_DataLake`: Azure Data Lake Storage Gen2 / Delta Lake.  
- `LS_RestService`: REST API linked service used by the `RESTAPI` pipeline.  
- `LS_KeyVault`: Azure Key Vault for managing secrets.

## Deployment

1. Import JSON assets (pipelines, datasets, dataflows, linked services) into a target Data Factory or use CI/CD with ARM/Bicep.  
2. Update linked services to match the target subscription, resource group, and credentials.  
3. Configure triggers for `Ingestion`, `Scheduled`, and other pipelines according to your environment.  
4. Publish changes from the `main` branch in the ADF UI.

```markdown
