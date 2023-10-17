# dbt (Data Build Tool) Bootcamp: Zero to Hero (Udemy)

## Slowly Changing Dimensions (SCD)

### Type 0 - Retain Original:
- **Description:** Do not update the Data Warehouse (DWH) table when a dimension changes.

### Type 1 - Overwrite:
- **Description:** Update the DWH table when a dimension changes, overwriting the original data.

### Type 2 - Add New Row:
- **Description:** Keep full history by adding additional (historic data) rows for each dimension change.
- **Note:** DBT can handle this using `dbt_valid_from` and `dbt_valid_to` columns.

### Type 3 - Add New Attribute:
- **Description:** Keep limited data history by adding separate columns for original and current values.

## Materialization Types

### 1. View
- **Use Case:**
  - Lightweight representation.
  - Infrequent data reuse.
- **Avoid When:**
  - Frequent reads from the same model.

### 2. Table
- **Use Case:**
  - Repeated reads from the model.
- **Avoid When:**
  - Building models for one-time use.
  - Populating models incrementally.

### 3. Incremental (Table Appends)
- **Use Case:**
  - Fact tables.
  - Appending data to tables.
- **Avoid When:**
  - Need to update historical records.

### 4. Ephemeral (CTEs)
- **Use Case:**
  - Creating an alias for your data.
- **Avoid When:**
  - Frequent reads from the same model.

## Seeds and Sources

### Seeds:
- Seeds are local files, such as CSV files, that you upload to the data warehouse using dbt.

### Sources:
- Sources provide an abstraction layer on top of input tables and can be defined in the `sources.yml` file.

### Checking Source Freshness:
- You can check the freshness of your sources using the `dbt source freshness` command. To set up freshness checks, define `warn_after` and `error_after` settings in the `sources.yml` file.
