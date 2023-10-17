Welcome to your new dbt project!

### Using the starter project

Try running the following commands:
- dbt run
- dbt test


### Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](https://community.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices


### SCD (Slowly Changing Dimensions)

- **Type 0 - Retain Original:**
  - Description: Do not update the Data Warehouse (DWH) table when a dimension changes.

- **Type 1 - Overwrite:**
  - Description: Update the DWH table when a dimension changes, overwriting the original data.

- **Type 2 - Add New Row:**
  - Description: Keep full history by adding additional (historic data) rows for each dimension change.
  - Note: DBT can handle this using `dbt_valid_from` and `dbt_valid_to` columns.

- **Type 3 - Add New Attribute:**
  - Description: Keep limited data history by adding separate columns for original and current values.


### Materialization Types

1. **View**

   **Use Case:**
   - Lightweight representation.
   - Infrequent data reuse.

   **Avoid When:**
   - Frequent reads from the same model.

2. **Table**

   **Use Case:**
   - Repeated reads from the model.

   **Avoid When:**
   - Building models for one-time use.
   - Populating models incrementally.

3. **Incremental (Table Appends)**

   **Use Case:**
   - Fact tables.
   - Appending data to tables.

   **Avoid When:**
   - Need to update historical records.

4. **Ephemeral (CTEs)**

   **Use Case:**
   - Creating an alias for your data.

   **Avoid When:**
   - Frequent reads from the same model.


