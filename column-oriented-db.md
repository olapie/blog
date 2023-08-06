Clickhouse is a column oriented database, while MySQL, PostgreSQL are row oriented database.
Clickhouse is a Relational Database and supports SQL.   
Clickhouse is for OLAP(online analytical processing), while MySQL, PostgreSQL are OLTP.

Same column of all records are stored together,   
e.g. name:  tom:001, jim:002, lucy:003  
     score: 89:001, 90:002, 78:003  
It's a similar with MySQL index, every column is indexed, that's why it's fast to query in clickhouse. 
Each column is stored in a seperate data file.  
Refer to: https://clickhouse.com/docs/en/optimize/sparse-primary-indexes  

supports composite primary key
doesn't support transaction at present

https://www.timescale.com/blog/what-is-clickhouse-how-does-it-compare-to-postgresql-and-timescaledb-and-how-does-it-perform-for-time-series-data/  
```
ClickHouse’s limitations / weaknesses include:

    Worse query performance than TimescaleDB at nearly all queries in the Time-Series Benchmark Suite, except for complex aggregations.
    Poor inserts and much higher disk usage (e.g., 2.7x higher disk usage than TimescaleDB) at small batch sizes (e.g., 100-300 rows/batch).
    Non-standard SQL-like query language with several limitations (e.g., joins are discouraged, syntax is at times non-standard)
    Lack of other features one would expect in a robust SQL database (e.g., PostgreSQL or TimescaleDB): no transactions, no correlated sub-queries, no stored procedures, no user defined functions, no index management beyond primary and secondary indexes, no triggers.
    Inability to modify or delete data at a high rate and low latency - instead have to batch deletes and updates
    Batch deletes and updates happen asynchronously
    Because data modification is asynchronous, ensuring consistent backups is difficult: the only way to ensure a consistent backup is to stop all writes to the database
    Lack of transactions and lack of data consistency also affects other features like materialized views, because the server can't atomically update multiple tables at once. If something breaks during a multi-part insert to a table with materialized views, the end result is an inconsistent state of your data.
```


ClickHouse, PostgreSQL, and TimescaleDB architectures

At a high level, ClickHouse is an excellent OLAP database designed for systems of analysis.

PostgreSQL, by comparison, is a general-purpose database designed to be a versatile and reliable OLTP database for systems of record with high user engagement.

TimescaleDB is a relational database for time-series: purpose-built on PostgreSQL for time-series workloads. It combines the best of PostgreSQL plus new capabilities that increase performance, reduce cost, and provide an overall better developer experience for time-series.

So, if you find yourself needing to perform fast analytical queries on mostly immutable large datasets with few users, i.e., OLAP, ClickHouse may be the better choice.

Instead, if you find yourself needing something more versatile, that works well for powering applications with many users and likely frequent updates/deletes, i.e., OLTP, PostgreSQL may be the better choice.

And if your applications have time-series data - and especially if you also want the versatility of PostgreSQL - TimescaleDB is likely the best choice.
