# Delta Lake and Open Table Formats

## 1. What Is Delta Lake?

**Delta Lake is an open table format** that adds reliable table-management capabilities to data stored in Parquet files.

In Databricks, the terms **Delta Lake**, **Delta format**, and **Delta file format** are often used interchangeably.

A Delta table consists of two main components:

1. **Parquet files** — Store the actual data.
2. **Delta transaction log (`_delta_log`)** — Tracks changes and manages the table.

There is no separate `.delta` data-file extension.

## 2. How Delta Lake Stores Data

Suppose we convert a CSV dataset into a Delta table.

The original data is written as Parquet files, and Delta Lake creates a transaction log to manage them.

```text
sales/                         ← Delta table directory
│
├── part-00001.parquet          ← Actual data
├── part-00002.parquet          ← Actual data
│
└── _delta_log/                 ← Transaction log
    ├── 00000000000000000000.json
    ├── 00000000000000000001.json
    └── 00000000000000000002.json
```

**Important:** Multiple Parquet files can belong to one Delta table, and the table has one transaction-log directory.

## 3. What Is the Delta Transaction Log?

The **Delta log** is the metadata and transaction history used to manage a Delta table.

It records information such as:

- Which Parquet files were added or removed from the active table
- Table schema and metadata
- Changes made through transactions
- Table versions

Each successfully committed table version is represented by a numbered JSON transaction-log file. Delta Lake can also create checkpoint files to make reading the log more efficient.

### What happens when new data is inserted?

1. New data is written into Parquet files.
2. A new transaction is committed to the Delta log.
3. The log records which files were added.
4. Future queries can include those files when reading the table.

When data is deleted or updated, Delta Lake also records the relevant changes so readers can identify the correct current data.

## 4. How Delta Lake Reads Data

When a user queries a Delta table:

1. A Delta-compatible processing engine examines the transaction log.
2. It determines which data files belong to the requested table version.
3. It reads the required Parquet files.
4. It returns the query results.

The engine does not simply read every file in the folder. It uses the Delta log to determine the table's valid state.

**Note:** Delta Lake can use checkpoints and other optimizations, so it does not necessarily reread every historical JSON log file for each query.

## 5. Why Does Delta Lake Use Parquet?

**Apache Parquet is a columnar file format**, meaning it physically organizes data by columns rather than storing complete rows together.

For example, imagine a dataset containing 100 columns.

If a query requests only three columns, Parquet can efficiently read the relevant columns without loading all 100.

### Benefits of Parquet

- Efficient analytical queries
- Column-based reading
- Compression
- Reduced unnecessary data reads
- Suitable for large-scale analytics

### Parquet vs. Avro

| Parquet | Avro |
|---|---|
| Column-oriented format | Row-oriented format |
| Optimized for analytical reads | Commonly used for data exchange and streaming |
| Efficient when selecting a few columns | Useful for processing complete records |
| Used to store Delta table data | Not the underlying data format of Delta tables |

## 6. Delta Lake vs. Parquet

| Feature | Parquet | Delta Lake |
|---|---|---|
| Type | File format | Open table format |
| Stores actual data | Yes | Uses Parquet files |
| Transaction log | No | Yes |
| Tracks table versions | No | Yes |
| Supports ACID transactions by itself | No | Yes |
| Supports reliable table updates | Not by itself | Yes |

**Parquet determines how data is physically stored. Delta Lake determines how those data files are managed together as a reliable table.**

## 7. DP-750 Key Takeaways

- Delta Lake is an open table format used in Azure Databricks.
- Delta table data is stored in **Parquet** format.
- `_delta_log` maintains transaction history and table metadata.
- JSON commit files record changes to the table.
- Delta-compatible engines use the log to determine the valid table state.
- Parquet's columnar storage is efficient for analytical queries.
- Delta Lake provides the foundation for reliable transactions and table versioning.

**Remember: Delta Table = Parquet Data Files + Delta Transaction Log.**