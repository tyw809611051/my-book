1.所有多索引API支持以下url查询字符串参数:
```
ignore_unavailable
```
控制是否忽略任何指定的索引不可用，这包括不存在的索引或封闭的索引。任一true或false 可以被指定

```
allow_no_indices
```
控制是否失败，如果通配符索引表达式导致没有具体的索引。任一true或false可以被指定。例如，如果foo\*指定了通配符表达式，并且foo根据此设置，没有可用的索引可用，则请求将失败。当或未指定索引时_all，此设置也适用*。此设置也适用于别名，以防别名指向封闭的索引

```
expand_wildcards
```
控制什么样的具体索引通配符索引表达式扩展到。如果open被指定，则通配符表达式将扩展为仅打开索引，如果closed指定，则通配符表达式仅扩展为闭合索引。也open,closed可以指定值（）以扩展到所有索引

```
以适合人类（例如"exists_time": "1h"或"size": "1kb"）和计算机（例如"exists_time_in_millis": 3600000或"size_in_bytes": 1024）
```

```
#flat_settings标志影响设置列表的呈现

{
  "persistent" : { },
  "transient" : {
    "discovery.zen.minimum_master_nodes" : "1"
  }
}
```

```
preference
_primary:该操作将仅在主分片上执行
_local:在本地分配的分片上执行
```

#### URL中允许的参数：
|名称|描述|
|----|----|
|df|在查询中未定义字段前缀时使用的默认字段|
|analyzer|分析查询字符串时使用的分析器名称|
|lowercase\_expanded_terms|条款是否会自动降低。默认为true|
|analyze_wildcard|应该分析通配符和前缀查询。默认为false|
|default_operator|要使用的默认运算符可以是AND或 OR。默认为OR|
|lenient|如果设置为true将导致基于格式的失败（例如，提供文本到数字字段）被忽略。默认为false|
|explain|对于每个命中，包含如何计算点击评分的说明|
|\_source|设置为false禁用\_source字段的检索。还可以使用\_source\_include＆\_source_exclude|
|fields|要为每个命中返回的文档的选择性存储字段，以逗号分隔。不指定任何值将不会返回任何字段|
|sort|排序|
|track_scores|当排序时，设置为true仍然跟踪分数，并将其作为每个命中的一部分返回|timeout|搜索超时时间|
|terminate_after|每个分片收集的最大文档数量，到达查询执行将提前终止|
|search\_type|要执行的搜索操作的类型。可以 dfs\_query\_then\_fetch，query\_then_fetch|

