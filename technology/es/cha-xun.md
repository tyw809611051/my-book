**1. 简单查询**

像传递URL参数一样去传递查询语句
```
GET /cisscool/component/_search?q=package:0805 
```

**2. term查询**

term是代表包含操作，即不进行分词器分析，文档中必须包含整个搜索的词汇
```
GET /cisscool/component/_search
{
    "query": {
        "term": {
           "package": "0805"
        }
    }
}
```


**3. match查询**

match和term的区别是,match查询的时候,elasticsearch会根据你给定的字段提供合适的分析器,而term查询不会有分析器分析的过程

match查询相当于模糊匹配,只包含其中一部分关键词就行
```
GET /cisscool/component/_search
{
    "query": {
        "match": {
           "package":{ 
                "query": "0805",
                "operator" : "and" #or/not
                "minimum_should_match" : "75%" #最小匹配参数
            }
        }
    }
}
```

**4. match_all查询**

查询指定索引下的所有文档
```
GET /cisscool/component/_search
{
    "query": {
        "match_all": {}
    }
}
```

**match\_phrase查询**

短语查询,slop定义的是关键词之间隔多少未知单词
```
POST /cisscool/component/_search
{
    "match_phrase" : {
        "package" : {
            "query" : "this is a 0805",
            "analyzer" : "my_analyzer"
        }
    } 
}

```

**match_phrase_prefix**

前缀短语查询
```
POST /cisscool/component/_search
{
    "match_phrase_prefix" : {
        "package" : {
            "query" : "this is a 0805",
            "analyzer" : "my_analyzer"
        }
    } 
}
```

**multi_match查询**

**bool查询**

可以接受多个其他过滤器作为参数
```
POST /cisscool/component/_search
{
  "query": {
    "filtered": {
      "filter": {
        "bool": {
          "must": [
            {
              "multi_match": {
                "query": "RMK1608-M-B-103-F",
                "fields": [
                  "exact_specification_model_no",
                  "specification_model_no^4"
                ],
                "slop": 0
              }
            }
          ],
          "must_not": [
            {
              "term": {
                "category_id": ""
              }
            }
          ]
        }
      }
    }
  }
}
```

**filter过滤查询**

执行速度非常快，不会计算相关度（直接跳过了整个评分阶段）而且很容易被缓存

**constant_score**

非评分模式,以统一评分1返回
```
POST /cisscool/component/_search
{
    "query" : {
        "constant_score" : { 
            "filter" : {
                "term" : { 
                    "package" : 0805
                }
            }
        }
    }
}
```

**must查询**

等价于 and
```
POST cisscool/component/_search
{
"query": {
  "bool": {
    "must": [
      {"term": {
        "specification_model_no": {
          "value": "rmk"
        }
      }}
    ]
  }
} 
}
```

**must_not查询**

```
POST cisscool/component/_search
{
"query": {
  "bool": {
    "must_not": [
      {"term": {
        "specification_model_no": {
          "value": "rmk"
        }
      }}
    ]
  }
} 
}
```

**should查询**
```
POST cisscool/component/_search
{
"query": {
  "bool": {
    "should": [
      {"term": {
        "specification_model_no": {
          "value": "rmk"
        }
      }}
    ]
  }
} 
}
```

**range**
```
POST /cisscool/component/_search
{
    "query" : {
        "constant_score" : {
            "filter" : {
                "range" : {
                    "price" : {
                        "gte" : 20,
                        "lt"  : 40
                    }
                }
            }
        }
    }
}
```
- gt: > 大于（greater than）
- lt: < 小于（less than）
- gte: >= 大于或等于（greater than or equal to）
- lte: <= 小于或等于（less than or equal to）

**exists查询**

等价于 IS NOT NULL
```
POST /cisscool/component/_search
{
   "query" : {
        "constant_score" : {
            "filter" : {
                "exists" : { "field" : "package" }
            }
        }
    }
}
```

**missing查询**

等价于 IS NULL
```
POST /cisscool/component/_search
{
   "query" : {
        "constant_score" : {
            "filter" : {
                "missing" : { "field" : "package" }
            }
        }
    }
}
```
**wildcard**

**aggs聚合**
