Options:  
1. ElasticSearch, convinient, full text index, need more resources, CPU, disk   
2. HBase, less resources, few functionalities

We can make use of ElasticSearch's powerful features, to avoid large disk files, just store essential fields and indexes in it, put entire record in hbase and associated with rowkey.  
