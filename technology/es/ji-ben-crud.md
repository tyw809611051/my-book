#### CRUD
**接口URL格式**
```
curl -X<VERB> '<PROTOCOL>://<HOST>/<PATH>?<QUERY_STRING>' -d '<BODY>'  
```
- VERB HTTP方法：GET(获取), POST(更新), PUT(创建), HEAD, DELETE(删除)
- PROTOCOL： http或者https协议（只有在Elasticsearch前面有https代理的时候可用）
- HOST： Elasticsearch集群中的任何一个节点的主机名，如果是在本地的节点，那么就叫localhost
- PORT： Elasticsearch HTTP服务所在的端口，默认为9200
- QUERY_STRING： 一些可选的查询请求参数，例如?pretty参数将使请求返回更加美观易读的JSON数据
- BODY： 一个JSON格式的请求主体（如果请求需要的话）

**添加文档**
```
curl -XPUT '127.0.0.1:9200/cisscool/component/1?pretty' -d 
'{
    "title" : "component"
}'
```
**删除文档**
```
curl -XDELETE '127.0.0.1:9200/cisscool/component/1?pretty'
```
**修改文档**
```
curl -XPOST '127.0.0.1:9200/cisscool/component/1/_update?pretty' -d 
'{
  "doc" : {
       "title" : "component"
  }
}'
```
**获取文档**
```
curl -XGET '127.0.0.1:9200/cisscool/component/1?pretty'
```
### 批量操作
|action(行为)|解释|
|----|----|
|create|当文档不存在时创建|
|index|创建新文档或替换已有文档|
|update|局部更新文档|
|delete|删除文档|
```
#请求体格式
{action:{metadata}}\n
{request body}\n
```

**1.1批量获取不同index文档**
```
curl -XGET '127.0.0.1:9200/_mget?pretty' -d
'{
    "docs" : {
        {
            "_index" : "cisscool",
            "_type"  : "component",
            "_id"    : 1
        },
        {
            "_index" : "cissdata",
            "_type"  : "component",
            "_id"    : 1
            
        }
    }
}'
```
**1.2批量获取相同index相同type下不同ID的文档**
```
curl -XGET '127.0.0.1:9200/cisscool/component/_mget?pretty' -d
'{
    "docs" : {
        {
            "_id"    : 1
        },
        {
            "_id"    : 2
        }
    }
}'
或
curl -XGET '127.0.0.1:9200/cisscool/component/_mget?pretty' -d
'{
   "ids" : ["6","28"]
}'
```

**2.批量新建数据**
```
curl -XPOST '127.0.0.1:9200/cisscool/component/_bulk?pretty'
{"index" : {"_id" : 1}}
{"title" : "cool"}
{"create" : {"_index":"cisscool","_type":"component","_id" : 1}}
{"title":"cool"}

```
**3.批量删除数据**
```
curl -XPOST '127.0.0.1:9200/cisscool/component/_bulk?pretty'
{"delete" : {"_index":"cisscool","_type" : "component" ,"_id" : 1}}
```



#### Elasticsearch的内置字段及类型
|||
|--|--|
|内置字段|_uid,_id,_type,_source,_all,_analyzer,_boost,_parent,_routing,_index,_size,_timestamp,_ttl|
|字段类型|String,Integer/long,Float/double,Boolean,Null,Date|