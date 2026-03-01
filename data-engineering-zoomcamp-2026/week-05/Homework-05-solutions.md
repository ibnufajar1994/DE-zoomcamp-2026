# Bruin Pipeline Questions & Answers

## Question 1. In a Bruin project, what are the required files/directories?

According to the official documentation and example projects, a minimal Bruin project must include the following structure:

- A `.bruin.yml` file located at the root of the project.  
  This file defines environments, database connections, and secrets.

- A `pipeline/` directory that contains:
  - `pipeline.yml` — defines the pipeline’s metadata and configuration.
  - An `assets/` folder — contains all asset files such as Python scripts, SQL files, YAML configurations, and other related resources.

Therefore, the required components are:

**Answer:**  
`.bruin.yml` and `pipeline/` containing `pipeline.yml` and `assets/`

---

## Question 2. You're building a pipeline that processes NYC taxi data organized monthly based on `pickup_datetime`. Which incremental strategy is best for processing a specific time interval by deleting and reinserting data for that period?

The most appropriate incremental strategy for this scenario is `time_interval`.

The `time_interval` strategy is specifically designed for time-based data processing. It allows you to reprocess a defined time window (for example, a specific month) by deleting and reinserting records where `pickup_datetime` falls within that interval.

This strategy is suitable because:

- It deletes and reinserts data only for the specified time window.
- It uses a time column (`pickup_datetime`) to determine the interval boundaries.
- It does not modify data outside the selected period.

Therefore:

**Answer:**  
`time_interval`

---

## Question 3. You have a variable defined in `pipeline.yml`:

```yaml
variables:
  taxi_types:
    type: array
    items:
      type: string
    default: ["yellow", "green"]
```

How do you override this when running the pipeline to process only yellow taxis?

To override the default variable value at runtime, use the `--var` flag with the `bruin run` command:

```bash
bruin run --var 'taxi_types=["yellow"]'
```

Explanation:

- `bruin run` executes the pipeline or a specific asset.
- `--var` allows you to define or override a variable dynamically at execution time.
- `'taxi_types=["yellow"]'` sets the `taxi_types` variable to a list containing only `"yellow"`.

Therefore:

**Answer:**  
`bruin run --var 'taxi_types=["yellow"]'`

---

## Question 4. You've modified the `ingestion/trips.py` asset and want to run it plus all downstream assets. Which command should you use?

To execute the modified asset and all assets that depend on it, use the `--downstream` flag:

```bash
bruin run ingestion/trips.py --downstream
```

The `--downstream` option tells Bruin to run the specified asset along with every asset that depends on it in the dependency graph.

Therefore:

**Answer:**  
`bruin run ingestion/trips.py --downstream`

---

## Question 5. You want to ensure the `pickup_datetime` column in your trips table never contains NULL values. Which quality check should you add to your asset definition?

To enforce this constraint, you should add a column-level quality check using the built-in `not_null` rule on the `pickup_datetime` column.

Example configuration:

```yaml
name: not_null
```

This ensures that the specified column cannot contain NULL values during validation.

Therefore:

**Answer:**  
`name: not_null`

---

## Question 6. After building your pipeline, you want to visualize the dependency graph between assets. Which Bruin command should you use?

Bruin provides a dedicated command to visualize asset dependencies:

```bash
bruin lineage
```

The `bruin lineage` command generates a visual representation of how assets depend on one another within the pipeline.

Therefore:

**Answer:**  
`bruin lineage`

---

## Question 7. You're running a Bruin pipeline for the first time on a new DuckDB database. What flag should you use to ensure tables are created from scratch?

When running the pipeline for the first time (or when you want to fully rebuild tables), you should use the `--full-refresh` flag:

```bash
bruin run --full-refresh
```

The `--full-refresh` flag clears existing tables before execution, ensuring that all data is recalculated and rebuilt from scratch rather than processed incrementally.

Therefore:

**Answer:**  
`--full-refresh`
