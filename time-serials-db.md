Prometheus, InfluxDB  

Timestamp is the primary key  

Collecting metrics from Docker  
Enable endpoint of docker: http://127.0.0.1:9323/metrics  
Set up prometheus job to collect metrics from docker endpoint every 5s or 15s. 
Metrics output is : 
`le` means the value is `less or equal than` 
last number `1` is the count  
```
# HELP engine_daemon_container_actions_seconds The number of seconds it takes to process each container action
# TYPE engine_daemon_container_actions_seconds histogram
engine_daemon_container_actions_seconds_bucket{action="changes",le="0.005"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="0.01"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="0.025"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="0.05"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="0.1"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="0.25"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="0.5"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="1"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="2.5"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="5"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="10"} 1
engine_daemon_container_actions_seconds_bucket{action="changes",le="+Inf"} 1
engine_daemon_container_actions_seconds_sum{action="changes"} 0
engine_daemon_container_actions_seconds_count{action="changes"} 1
```
Prometheus stores this kind of metrics every 5 or 15 seconds, 1m... 

Prometheus also emit metrics of itself at http://localhost:9090/metrics  
quantile 0.25 means 25% (p25), 0.99 means 99% (p99)
E.g. 
```
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 1.7367e-05
go_gc_duration_seconds{quantile="0.25"} 0.000197103
go_gc_duration_seconds{quantile="0.5"} 0.000313192
go_gc_duration_seconds{quantile="0.75"} 0.000378644
go_gc_duration_seconds{quantile="1"} 0.000460161
go_gc_duration_seconds_sum 0.002652418
go_gc_duration_seconds_count 10
# HELP go_goroutines Number of goroutines that currently exist.
# TYPE go_goroutines gauge
go_goroutines 31
# HELP go_info Information about the Go environment.
# TYPE go_info gauge
go_info{version="go1.20.6"} 1
# HELP go_memstats_alloc_bytes Number of bytes allocated and still in use.
# TYPE go_memstats_alloc_bytes gauge
go_memstats_alloc_bytes 1.8564312e+07
# HELP go_memstats_alloc_bytes_total Total number of bytes allocated, even if freed.
# TYPE go_memstats_alloc_bytes_total counter
go_memstats_alloc_bytes_total 7.3542624e+07
# HELP go_memstats_buck_hash_sys_bytes Number of bytes used by the profiling bucket hash table.
# TYPE go_memstats_buck_hash_sys_bytes gauge
go_memstats_buck_hash_sys_bytes 1.47298e+06
# HELP go_memstats_frees_total Total number of frees.
# TYPE go_memstats_frees_total counter
go_memstats_frees_total 262747
# HELP go_memstats_gc_sys_bytes Number of bytes used for garbage collection system metadata.
# TYPE go_memstats_gc_sys_bytes gauge
go_memstats_gc_sys_bytes 8.982032e+06
# HELP go_memstats_heap_alloc_bytes Number of heap bytes allocated and still in use.
# TYPE go_memstats_heap_alloc_bytes gauge
go_memstats_heap_alloc_bytes 1.8564312e+07

# TYPE prometheus_engine_query_duration_seconds summary
prometheus_engine_query_duration_seconds{slice="inner_eval",quantile="0.5"} 5.562e-06
prometheus_engine_query_duration_seconds{slice="inner_eval",quantile="0.9"} 0.000137151
prometheus_engine_query_duration_seconds{slice="inner_eval",quantile="0.99"} 0.000137151
prometheus_engine_query_duration_seconds_sum{slice="inner_eval"} 0.000153869
prometheus_engine_query_duration_seconds_count{slice="inner_eval"} 4
``` 
