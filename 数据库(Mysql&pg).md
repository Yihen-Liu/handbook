#### 性能优化

1. 查询过慢，修改了如下的pg配置项，性能提升了2个数量级；

```
# Total Memory (RAM): 32 GB
# 内存变动时，仅调整这3行
shared_buffers = 8GB
effective_cache_size = 24GB
maintenance_work_mem = 2GB

autovacuum_vacuum_scale_factor = 0
autovacuum_analyze_scale_factor = 0
autovacuum_vacuum_threshold = 1000
autovacuum_analyze_threshold = 1000
autovacuum_vacuum_cost_limit = 1000

min_wal_size = 1GB
max_wal_size = 4GB
wal_buffers = 16MB
checkpoint_completion_target = 0.9

max_connections = 1000
work_mem = 64MB
random_page_cost = 1.1
default_statistics_target = 100
effective_io_concurrency = 200
```



#### 手册

1. Postgres中文手册 http://www.postgres.cn/docs/9.4/index.html
