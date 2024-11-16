# Slowly Changing Dimensions in Snowflake Using Streams and Tasks

A modern approach to implementing Slowly Changing Dimensions (SCD) in Snowflake, leveraging automated data pipelines and native Snowflake features for efficient change tracking and historical data management.

## Pipeline Overview

An end-to-end data pipeline that automatically captures and processes dimensional changes:

1. **Data Source** → **S3** → **Snowflake Staging** → **Production Tables**

## Key Components

### Data Ingestion Layer
- **Amazon S3**: Landing zone for source files
- **Snowpipe**: Real-time data ingestion service
  - Automatically detects new files in S3
  - Loads data into staging tables without manual intervention

### Change Detection Layer
- **Snowflake Streams**: 
  - Captures INSERT, UPDATE, DELETE operations
  - Maintains change tracking metadata
  - Enables efficient processing of incremental changes

### Processing Layer
- **Snowflake Tasks**:
  - Scheduled jobs for SCD processing
  - Handles type 1 (overwrite) and type 2 (historical) changes
  - Maintains referential integrity

### Storage Layer
- **Staging Tables**: Temporary landing zone for raw data
- **Dimension Tables**: Final tables with historical tracking
  - Includes effective dates
  - Maintains current and historical records
  - Supports point-in-time analysis

## Use Cases

Ideal for:
- Customer dimension management
- Product catalog versioning
- Employee data tracking
- Any dimension requiring historical change tracking

## Technical Stack

Required components:
- Snowflake Enterprise Edition
- Amazon S3 bucket
- Docker (for local development)
- Apache NiFi (optional, for additional data routing)
- Jupyter Notebook (for testing and validation)

## Architecture Diagram
![Untitled Diagram](https://github.com/user-attachments/assets/dcddb7a7-8269-4942-aa24-54ec18e03da2)


## Implementation Steps

1. **Environment Setup**
   ```sql
   -- Create required databases and schemas
   CREATE DATABASE scd_demo;
   USE DATABASE scd_demo;
   ```

2. **Configure Integrations**
   - Set up S3 integration
   - Configure Snowpipe
   - Create necessary roles and permissions

3. **Deploy Components**
   - Initialize staging tables
   - Create streams on staging tables
   - Configure and schedule tasks

4. **Monitor and Maintain**
   - Track task execution
   - Monitor data quality
   - Manage historical storage
