Options:  
1. ElasticSearch, convinient, full text index, need more resources, CPU, disk   
2. HBase, less resources, few functionalities
3. Clickhouse refer to uber solution https://www.infoq.cn/article/l4thjgnr7hxpkgpmw6dz 

We can make use of ElasticSearch's powerful features, to avoid large disk files, just store essential fields and indexes in it, put entire record in hbase and associated with rowkey.  
