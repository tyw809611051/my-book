```
rest.action.multi.allow_explicit_index：false
```
设置为false，Elasticsearch将拒绝具有在请求正文中指定的显式索引的请求

```
node.data：true //是否存储数据
```
```
node.master:true
```

```
node.attr.rack:test-hot
```

```
path.conf:
```
```
path.data:
```

```
path.logs:
```

```
node.max_local_storage_node:1
```

```
gateway.recover_after_nodes:1
```

```
gateway_recover_after_time:10m
```

```
gateway.expected_nodes:1   
```
```
#设置查询超时时间
search.default_search_timeout:50s
```
#### cache设置
```
#fielddata可以使用的缓存大小,也可设置为M
indices.fielddata.cache.size:20%
```

```
#断路器,超过该大小，则断开
indices.breaker.fielddata.limit:40%
```

```
indices.breaker.request.limit:30%
```

```
indices.breaker.request.limit:30%
```

#### 跨域设置
```
http.cors.enabled:true
```
```
http.cors.allow-origin:"*"
```

```
http.max_content_length:1024mb
```

#### 线程池设置
```
thread_pool_bulk.queue_size:4096
```

```
thread_pool.index.queue_size:1024
```

```
thread_pool.search.queue_size:1024
```

```
thread_pool.get.queue_size:1024
```

#### 安全设置
```
#是否自动创建索引,默认为true
action.auto_create_index:false
```

```
#是否需要完全匹配才能删除，设置为true
action.destructive_requires_name:true
```