---
title: "Redis"
date: 2021-12-31T15:43:22-05:00
draft: true
---

Redis ZSet consists of SkipList and HashSet. Two copies of data. SkipList for range, HashSet for get  

https://redis.io/topics/cluster-tutorial
Redis Cluster:
Sharding: 16384 hash slots, slot=CRC16(key)%16384, Each node is responsible for a subset of slots
Replication: a node has 1 master - N slaves
Async replication has high performance, while sync replication (WAIT cmd) has strong consistency  

```  
struct sdshdr { 
    int len;   
    int free;  
    char buf[];  
};
```
Why not use C-style string? Allow "abc\0def", \0 is not string terminator.   

In Redis, duplicate object can be shared, the cost is to compare objects.  
Redis can set max memory and will release unused memory.  
Single threaded. v6 is multi-threaded  

Redis hash table structure   
```
ht[0] is used
ht[1] is unused, only for rehash
dictht's default size is 4.
dict(Dictionary)->dictht(HashTable)->dictEntry(HashTableEntry)
```
![](https://pbs.twimg.com/media/E4RWYBgXoAAmjTN?format=jpg&name=medium)  



