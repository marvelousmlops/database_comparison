# Database Comparison: DuckDB, SQLite, and LevelDB

## Introduction

This project compares 3 popular databases: DuckDB, SQLite, and LevelDB. The purpose is to compare their performance, strengths, and limitations to emphasize the importance of choosing the right database for specific needs.

## Database Systems Overview

### DuckDB: The Analytical Powerhouse

- **Overview:** DuckDB is an in-process SQL OLAP (Online Analytical Processing) database management system designed for efficient query processing on large datasets.

- **Pros:**
  - Optimized for analytical queries.
  - In-memory processing for fast query execution.
  - Full SQL support.
  - Supports ART (Adaptive Radix Tree) and Min-Max indexes.
- **Cons:**
  - Can be memory-intensive.
  - ART indexes complicate processing with transactions.
- **Suitable Use Cases:**
  - Analytical workloads.
  - Data science and machine learning.
  

### SQLite: The Lightweight Champion

- **Overview:** SQLite is a lightweight, disk-based database engine that is serverless, and requires no extra installation.
- **Pros:**
  - Easy to set up and use.
  - Minimal disk space and memory usage.
  - Serverless architecture.
  - Full SQL support.
- **Cons:**
  - Not suitable for high-concurrency, large-scale applications.
  - Concurrent writes can be a bottleneck.
- **Suitable Use Cases:**
  - Mobile applications as it occupies minimal memory.
  - Embedded systems.
  - Small to medium-sized websites.

### LevelDB: The High-Throughput Dynamo

- **Overview:** LevelDB is a fast key-value storage library by Google.

- **Pros:**
  - Optimized for fast read and write operations.
  - Supports highly concurrent operations.
  - Efficient storage using log-structured merge-tree (LSM).
- **Cons:**
  - No SQL support.
  - Limited features compared to relational databases.
- **Suitable Use Cases:**
  - High-throughput applications.
  - Caching systems.
  - Log storage.

## Performance Test Summary

### Test Environment

- **Dataset:** 1,000,000 records with various fields (TransactionID, CustomerID, TransactionDatetime, ProductID, Quantity, Price, StoreID, Discount).
- **Queries Tested:**
  1. Query by ID
  2. Query by ID and another column
  3. Query with multiple keys
  4. Aggregation query

### Performance Results

| Query Type                     | DuckDB (without index) | SQLite (without index) | LevelDB (without index) | DuckDB (with index) | SQLite (with index) |
|--------------------------------|------------------------|------------------------|-------------------------|---------------------|---------------------|
| Query by ID                    | 0.00281 seconds        | 0.03814 seconds        | 0.00188 seconds         | 0.00121 seconds     | 0.00056 seconds     |
| Query by ID and another column | 0.00268 seconds        | 0.06407 seconds        | 0.00132 seconds         | 0.00151 seconds     | 0.00046 seconds     |
| Query with multiple keys       | 0.01255 seconds        | 0.11039 seconds        | 0.01218 seconds         | 0.00922 seconds     | 0.00060 seconds     |
| Aggregation query              | 0.00427 seconds        | 0.26850 seconds        | 722.87220 seconds       | 0.00348 seconds     | 0.27129 seconds     |


### Summary

- **DuckDB:** Shows some improvement with indexing, particularly for point lookups and range queries.
- **SQLite:** Benefits greatly from indexing, with indexed queries performing much faster than non-indexed ones.
- **LevelDB:** Extremely fast for most queries without indexing but has a significant outlier with the aggregation query taking much longer.

## Conclusion

Each database system has its strengths and is suitable for different use cases. DuckDB excels in analytical workloads and data processing pipelines, SQLite is perfect for lightweight, embedded applications, and LevelDB is designed for high-performance key-value storage.

By understanding the pros and cons of each system, you can make an informed decision based on your application's requirements, ensuring optimal performance and efficiency.

## How to Run the Tests

1. **Setup the Environment:**
   - Ensure you have Python installed.
   - Install necessary packages: `pandas`, `duckdb`, `sqlite3`, `leveldb`

