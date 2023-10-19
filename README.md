# dbt (Data Build Tool) Bootcamp: Zero to Hero (Udemy)

## Slowly Changing Dimensions (SCD)

#### Type 0 - Retain Original:
- Do not update the Data Warehouse (DWH) table when a dimension changes.

#### Type 1 - Overwrite:
- Update the DWH table when a dimension changes, overwriting the original data.

#### Type 2 - Add New Row:
- Keep full history by adding additional (historic data) rows for each dimension change.

#### Type 3 - Add New Attribute:
- Keep limited data history by adding separate columns for original and current values.

## Materialization Types

### View
- **Use Case:**
  - Lightweight representation.
  - Infrequent data reuse.
- **Avoid When:**
  - Frequent reads from the same model.

### Table
- **Use Case:**
  - Repeated reads from the model.
- **Avoid When:**
  - Building models for one-time use.
  - Populating models incrementally.

### Incremental (Table Appends)
- **Use Case:**
  - Fact tables.
  - Appending data to tables.
- **Avoid When:**
  - Need to update historical records.

### Ephemeral (CTEs)
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
 
## Snapshots
- Snapshots allow you to capture the current state of your data and store it in a way that is queryable and version-controlled (SCD type 2)
- use `dbt snapshot` to create and update snapshots
- DBT_VALID_TO is NULL when the data is still valid, and will be set to a date whenever the data is modified

## Tests

### Singular/Bespoke Tests
- SQL queries stored in the tests folder which are expected to return an empty resultset

### Generic Tests

There are 4 built-in generic tests:

- unique
- not_null
- accepted_values
- Relationships

Generic tests are defined in the `models/schema.yml` file.

You can also define your own generic tests or import tests from dbt packages. 

Note: `model` and `column_name` are passed as default arguments to macros called from `models/schema.yml`.

## Macros

- Macros are jinja templates created in the macro folder
- There are many built-in macros in DBT
- You can use macros in model definitions and tests
- A special macro called test, can be used for implementing your own generic tests
- dbt packages can be installed easily to get access to a plethora of macros and tests

## Documentation

- Documentations can be defined in two ways:
    - In yaml files (like schema.yml)
    - IN standalone markdown files
- Dbt ships with a lightweight documentation web server
- For customizing the landing page, a special file, `overview.md` is used
- You can add you own assets (like images) to a special project folder

- use `dbt docs generate` to generate the doc and `dbt docs serve` to serve the doc dbt server

## Analysis

- Analyses are useful for writing ad-hoc analytical queries in dbt 
- Can be compiled into runnable SQL in the target folder by running `dbt compile`

## Hooks

- Hooks are SQLs that are executed at predefined times
- Hooks can be configured on the project, subfolder, or model level
- Hook types:
    - on_run_start: executed at the start of dbt {run, seed, snapshot}
    - on_run_end: executed at the start of dbt {run, seed, snapshot}
    - pre-hook: executed before a model/seed/snapshot is built
    - post-hook: executed after a model/seed/snapshot is built

## Exposures

- Exposures in dbt are a way to define and describe a downstream use of your dbt project, such as in a dashboard
- Exposure are created using yml files, such as `dashboard.yml`
- Exposures are included in the documentation
