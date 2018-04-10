- ### 字段数据类型
  - #### [string类型](#1.1)
  - #### [text类型](#1.2)
  - #### [keyword类型](#1.3)
  - #### [数字类型](#1.4)
  - #### [object类型](#1.5)
  - #### [date类型](#1.6)
  - #### [array类型](#1.7)
  - #### [binary类型](#1.8)
  - #### [ip类型](#1.9)
  - #### [range类型](#1.10)
  - #### [nested类型](#1.11)
  - #### [token_count类型](#1.12)
  - #### [geo point类型](#1.13)

- ### meta-feild元数据
    - #### [1._all](#2.1)
    - #### [2._field_names](#2.2)
    - #### [3._id](#2.3)
    - #### [4._index](#2.4)
    - #### [5._parent](#2.5)
    - #### [6._routing](#2.6)
    - #### [7._source](#2.7)
    - #### [8._type](#2.8)
    - #### [9._uid](#2.9)
- ### mappings参数
    - #### [1.analyzer](#3.1)
    - #### [2.normalizer](#3.2)
    - #### [3.boost](#3.3)
    - #### [4.coerce](#3.4)
    - #### [5.copy_to](#3.5)
    - #### [6.doc_values](#3.6)
    - #### [7.dynamic](#3.7)
    - #### [8.enabled](#3.8)
    - #### [9.fielddata](#3.9)
    - #### [10.format](#3.10)
    - #### [11.ignore_above](#3.12)
    - #### [12.ignore_malformed](#3.13)
    - #### [13.include_in_all](#3.14)
    - #### [14.index](#3.15)
    - #### [15.index_options](#3.16)
    - #### [16.fields](#3.17)
    - #### [17.norms](#3.18)
    - #### [18.null_value](#3.19)
    - #### [19.position_increment_gap](#3.19)
    - #### [20.properties](#3.20)
    - #### [21.search_analyzer](#3.21)
    - #### [22.similarity](#3.22)
    - #### [23.store](#3.23)
    - #### [24.term_vector](#3.24)
- ### 动态mapping
    - #### [1.default mapping](#4.1)
    - #### [2.dynamic field mapping](#4.2)
    - #### [3.dynamic templates](#4.3)
    - #### [4.override default template](#4.4)
    

<h4 id="1.1">1.1 string类型</h4>
>  ELasticsearch 5.X之后的字段类型不再支持string，由text或keyword取代。 如果仍使用string，会给出警告

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "component": {
      "properties": {
        "package": {
          "type":  "string"
        }
      }
    }
  }
}'

#结果
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "cisscool"
}

```

<h4 id="1.2">1.2 text类型</h4>

> text取代了string，当一个字段是要被全文搜索的，比如Email内容、产品描述，应该使用text类型。设置text类型以后，字段内容会被分析，在生成倒排索引以前，字符串会被分析器分成一个一个词项。text类型的字段不用于排序，很少用于聚合（termsAggregation除外）

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "component": {
      "properties": {
        "package": {
          "type":  "text"
        }
      }
    }
  }
}'

#结果
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "cisscool"
}
```

<h4 id="1.3">1.3 keyword类型</h4>

> keyword类型适用于索引结构化的字段，比如email地址、主机名、状态码和标签。如果字段需要进行过滤(比如查找已发布博客中status属性为published的文章)、排序、聚合。keyword类型的字段只能通过精确值搜索到

<h4 id="1.4">1.4 数字类型</h4>

> ==注意==：在满足需求的情况下，尽可能选择范围小的数据类型。比如，某个字段的取值最大值不会超过100，那么选择byte类型即可。迄今为止吉尼斯记录的人类的年龄的最大值为134岁，对于年龄字段，short足矣。字段的长度越短，索引和搜索的效率越高。
优先考虑使用带缩放因子的浮点类型。

|类型|取值范围|
|----|----|
|long|	-2^63至2^63-1|
|integer|	-2^31至2^31-1|
|short|	-32,768至32768|
|byte|	-128至127|
|double|	64位双精度IEEE 754浮点类型|
|float|	32位单精度IEEE 754浮点类型|
|half_float|	16位半精度IEEE 754浮点类型|
|scaled_float|	缩放类型的的浮点数（比如价格只需要精确到分，price为57.34的字段缩放因子为100，存起来就是5734）|
对于float、half_float和scaled_float,-0.0和+0.0是不同的值，使用term查询查找-0.0不会匹配+0.0，同样range查询中上边界是-0.0不会匹配+0.0，下边界是+0.0不会匹配-0.0。|

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "component": {
      "properties": {
        "number_of_bytes": {
          "type": "integer"
        },
        "time_in_seconds": {
          "type": "float"
        },
        "price": {
          "type": "scaled_float",
          "scaling_factor": 100
        }
      }
    }
  }
}'

#结果
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "cisscool"
}
```

<h4 id="1.5">1.5 Object类型</h4>

JSON天生具有层级关系，文档会包含嵌套的对象:
```
curl -XPUT http://192.168.0.122:9200/cisscool/component/1?pretty -d '{
  "region": "US",
  "manager": { 
    "age":     30,
    "name": { 
      "first": "John",
      "last":  "Smith"
    }
  }
}'
```
<h4 id="1.6">1.6 date类型</h4>

- JSON中没有日期类型，所以在ELasticsearch中，日期类型可以是以下几种:

    1.日期格式的字符串：e.g. “2015-01-01” or “2015/01/01 12:10:30
    
    2.long类型的毫秒数( milliseconds-since-the-epoch)
    
    3.integer的秒数(seconds-since-the-epoch) 
    
日期格式可以自定义，如果没有自定义，默认格式如下：
```
"strict_date_optional_time||epoch_millis"
```
```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "my_type": {
      "properties": {
        "created": {
          "type": "date" ,
          "index" : false,
          "format" : "yyyy-MM-dd HH:mm:ss"
        }
      }
    }
  }
}'

#插入数据
curl -XPUT 192.168.0.122:9200/cisscool/component/1?pretty -d'{
  "created": "2016-10-10 18:04:27"
}'
```

<h4 id="1.7">1.7 Array类型</h4>

ELasticsearch没有专用的数组类型，默认情况下任何字段都可以包含一个或者多个值，但是一个数组中的值要是同一种类型。例如：
    
    1.字符数组: [ “one”, “two” ]
    2.整型数组：[1,3]
    3.嵌套数组：[1,[2,3]],等价于[1,2,3]
    4.对象数组：[ { “name”: “Mary”, “age”: 12 }, { “name”: “John”, “age”: 10 }]

==注意事项：==

- 动态添加数据时，数组的第一个值的类型决定整个数组的类型
- 混合数组类型是不支持的，比如：[1,”abc”]
- 数组可以包含null值，空数组[ ]会被当做missing field对待。

<h4 id="1.8">1.8 binary类型</h4>

binary类型接受base64编码的字符串，默认不存储也不可搜索。

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "my_type": {
      "properties": {
        "name": {
          "type": "text"
        },
        "blob": {
          "type": "binary"
        }
      }
    }
  }
}'

#不可搜索
curl -XPUT 192.168.0.122:9200/cisscool/component/1?pretty -d'{
  "name": "Some binary blob",
  "blob": "U29tZSBiaW5hcnkgYmxvYg==" 
}'
```

<h4 id="1.9">1.9 ip类型</h4>

> ip类型的字段用于存储IPV4或者IPV6的地址

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "my_type": {
      "properties": {
        "ip_addr": {
          "type": "ip"
        }
      }
    }
  }
}'

curl -XPUT 192.168.0.122:9200/cisscool/component/1?pretty -d'{
  "ip_addr": "192.168.1.1"
}'
```

<h4 id="1.10">1.10 range类型</h4>

**支持类型**
|类型|范围|
|----|----|
|integer_range|	-2^31至2^31-1|
|float_range|	32-bit IEEE 754|
|long_range|	-2^63至2^63-1|
|double_range|	64-bit IEEE 754|
|date_range|	64位整数，毫秒计时|

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "component": {
      "properties": {
        "expected_attendees": {
          "type": "integer_range"
        },
        "time_frame": {
          "type": "date_range", 
          "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis"
        }
      }
    }
  }
}'

curl -XPUT 192.168.0.122:9200/cisscool/component/1?pretty -d'{
  "expected_attendees" : { 
    "gte" : 10,
    "lte" : 20
  },
  "time_frame" : { 
    "gte" : "2015-10-31 12:00:00", 
    "lte" : "2015-11-01"
  }
}'
```

<h4 id="1.12">1.12 token_count类型</h4>

> token_count用于统计词频

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "component": {
      "properties": {
       "name": { 
          "type": "text",
          "fields": {
            "length": { 
              "type":     "token_count",
              "analyzer": "standard"
            }
          }
        }
      }
    }
  }
}'

curl -XPUT 192.168.0.122:9200/cisscool/component/2?pretty -d'{
  "name": "Rachel Alice Williams"
}'
```

<h4 id="1.13">1.13 geo point 类型</h4>

> 地理位置信息类型用于存储地理位置信息的经纬度

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "component": {
      "properties": {
       "location": {
          "type": "geo_point"
        }
      }
    }
  }
}'

#插入4种不同的数据
curl -XPUT 192.168.0.122:9200/cisscool/component/3?pretty -d'{
  "text": "Geo-point as an object",
  "location": { 
    "lat": 41.12,
    "lon": -71.34
  }

  "text": "Geo-point as a string",
  "location": "41.12,-71.34" 
  
 "text": "Geo-point as a geohash",
  "location": "drm3btev3e86"

   "text": "Geo-point as an array",
  "location": [ -71.34, 41.12 ] 
}'

#搜索
curl -XPOST 192.168.0.122:9200/cisscool/_search?pretty -d '{
    "query": {
    "geo_bounding_box": { 
      "location": {
        "top_left": {
          "lat": 42,
          "lon": -72
        },
        "bottom_right": {
          "lat": 40,
          "lon": -74
        }
      }
    }
  }
}'
```

<h4 id="2.1">2.1 _all</h4>

> _all字段是把其它字段拼接在一起的超级字段，所有的字段用空格分开，_all字段会被解析和索引，但是不存储。当你只想返回包含某个关键字的文档但是不明确地搜某个字段的时候就需要使用_all字段

使用copy_to自定义_all字段
```
#可以尝试将5类数据聚合到一个字段
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "mappings": {
    "component": {
      "properties": {
        "title": {
          "type":    "text",
          "copy_to": "full_content" 
        },
        "content": {
          "type":    "text",
          "copy_to": "full_content" 
        },
        "full_content": {
          "type":    "text"
        }
      }
    }
  }
}'

#插入数据
curl -XPUT 192.168.0.122:9200/cisscool/component/3?pretty -d'{
  "title": "Master Java",
  "content": "learn Java"
}'

#搜索
curl -XPOST 192.168.0.122:9200/cisscool/_search?pretty -d '{
 "query": {
    "match": {
      "full_content": "java"
    }
  }
}'
```

<h4 id="2.2">2.2 _field_names</h4>

> _field_names字段用来存储文档中的所有非空字段的名字，这个字段常用于exists查询

```
curl -XPUT 192.168.0.122:9200/cisscool/component/3?pretty -d'{
  "title": "This is a document"
}'

curl -XPUT 192.168.0.122:9200/cisscool/component/4?refresh=true -d'{
  "title": "This is another document",
  "body": "This document has a body"
}'

#搜索
curl -XPOST 192.168.0.122:9200/cisscool/_search?pretty -d '{
  "query": {
    "terms": {
      "_field_names": [ "body" ] 
    }
  }
}'
```
<h4 id="2.3">2.3 _field_names</h4>

> 每条被索引的文档都有一个_type和_id字段，_id可以用于term查询、temrs查询、match查询、query_string查询、simple_query_string查询，但是不能用于聚合、脚本和排序


<h4 id="2.4">2.4 _index</h4>

> 多索引查询时，有时候只需要在特地索引名上进行查询，_index字段提供了便利，也就是说可以对索引名进行term查询、terms查询、聚合分析、使用脚本和排序

> _index是一个虚拟字段，不会真的加到Lucene索引中，对_index进行term、terms查询(也包括match、query_string、simple_query_string)，但是不支持prefix、wildcard、regexp和fuzzy查询


<h4 id="2.5">2.5 _parent</h4>

> _parent用于指定同一索引中文档的父子关系。下面例子中现在mapping中指定文档的父子关系，然后索引父文档，索引子文档时指定父id，最后根据子文档查询父文档

**适用场景：** 替换型号,父子关系数据
```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
   "mappings": {
    "my_parent": {},
    "my_child": {
      "_parent": {
        "type": "my_parent" 
      }
    }
  }
}'

curl -XPUT 192.168.0.122:9200/cisscool/my_parent/1?pretty -d'{
  "text": "This is a parent document"
}'
curl -XPUT 192.168.0.122:9200/cisscool/my_child/3?parent=1 -d'{
  "text": "This is another child document"
}'

curl -XPOST 192.168.0.122:9200/cisscool/my_parent/_search?pretty -d '{
   "query": {
    "has_child": { 
      "type": "my_child",
      "query": {
        "match": {
          "text": "child document"
        }
      }
    }
  }
}'
```

<h4 id="2.6">2.6 _routing</h4>

路由参数，ELasticsearch通过以下公式计算文档应该分到哪个分片上:
```
shard_num = hash(_routing) % num_primary_shards
```

默认的_routing值是文档的_id或者_parent，通过_routing参数可以设置自定义路由。例如，想把user1发布的博客存储到同一个分片上，索引时指定routing参数，查询时在指定路由上查询

```
#在Mapping中指定routing为必须的：增删改时需要指定routing
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
   "mappings": {
    "component": {
      "_routing": {
        "required": true 
      }
    }
  }
}'

#导入数据
curl -XPUT 192.168.0.122:9200/cisscool/component/1?routing=user1 -d'{
  "title": "This is a document"
}'

#搜索
curl -XPOST 192.168.0.122:9200/cisscool/component/_search?routing=user1 -d '{
  "query": {
    "match": {
      "title": "document"
    }
  }
}'
```
<h4 id="2.7">2.7 _source</h4>

> 存储的文档的原始值。默认_source字段是开启的，也可以关闭

但是一般情况下不要关闭，除法你不想做一些操作:

- 使用update、update_by_query、reindex
- 使用高亮
- 数据备份、改变mapping、升级索引
- 通过原始字段debug查询或者聚合

<h4 id="2.8">2.8 _type</h4>

> 条被索引的文档都有一个_type和_id字段，可以根据_type进行查询、聚合、脚本和排序

```
"query": {
    "terms": {
      "_type": [ "type_1", "type_2" ] 
    }
  },
  "aggs": {
    "types": {
      "terms": {
        "field": "_type", 
        "size": 10
      }
    }
  },
  "sort": [
    {
      "_type": { 
        "order": "desc"
      }
    }
  ],
  "script_fields": {
    "type": {
      "script": {
        "lang": "painless",
        "inline": "doc['_type']" 
      }
    }
  }
```

<h4 id="2.9">2.9 _uid</h4>

> _uid和_type和_index的组合。和_type一样，可用于查询、聚合、脚本和排序

<h4 id="3.1">3.1 analyzer</h4>

> 指定分词器(分析器更合理)，对索引和查询都有效

<h4 id="3.2">3.2 normalizer</h4>

> normalizer用于解析前的标准化配置，比如把所有的字符转化为小写等

```
curl -XPUT http://192.168.0.122:9200/cisscool/?pretty -d '{
  "settings": {
    "analysis": {
      "normalizer": {
        "my_normalizer": {
          "type": "custom",
          "char_filter": [],
          "filter": ["lowercase", "asciifolding"]
        }
      }
    }
  },
   "mappings": {
    "component": {
      "properties": {
        "foo": {
          "type": "keyword",
          "normalizer": "my_normalizer"
        }
      }
    }
  }
}'

curl -XPUT 192.168.0.122:9200/cisscool/component/1?pretty -d'{
   "foo": "BÀR"
}'
curl -XPUT 192.168.0.122:9200/cisscool/component/3? -d'{
  "foo": "bar"
}'

curl -XPOST 192.168.0.122:9200/cisscool/component/_search?pretty -d '{
  "query": {
    "match": {
      "foo": "BAR"
    }
  }
}'
```

<h4 id="3.3">3.3 boost</h4>

> boost字段用于设置字段的权重，比如，关键字出现在title字段的权重是出现在content字段中权重的2倍，设置mapping如下，其中content字段的默认权重是1

```
 "mappings": {
    "my_type": {
      "properties": {
        "title": {
          "type": "text",
          "boost": 2 
        },
        "content": {
          "type": "text"
        }
      }
    }
  }
```

<h4 id="3.4">3.4 coerce</h4>

> coerce属性用于清除脏数据，coerce的默认值是true。整型数字5有可能会被写成字符串“5”或者浮点数5.0.coerce属性可以用来清除脏数据

- 字符串会被强制转换为整数
- 浮点数被强制转换为整数

<h4 id="3.6">3.6 doc_values</h4>

> doc_values是为了加快排序、聚合操作，在建立倒排索引的时候，额外增加一个列式存储映射，是一个空间换时间的做法。默认是开启的，对于确定不需要聚合或者排序的字段可以关闭

**==注意:==** text类型不支持doc_values

```
 "mappings": {
    "my_type": {
      "properties": {
        "status_code": { 
          "type":       "keyword"
        },
        "session_id": { 
          "type":       "keyword",
          "doc_values": false
        }
      }
    }
  }
```

<h4 id="3.7">3.7 dynamic</h4>

dynamic属性用于检测新发现的字段，有三个取值：
- true:新发现的字段添加到映射中。（默认）
- flase:新检测的字段被忽略。必须显式添加新字段。
- strict:如果检测到新字段，就会引发异常并拒绝文档。

```
"mappings": {
    "my_type": {
      "dynamic": false, 
      "properties": {
        "user": { 
          "properties": {
            "name": {
              "type": "text"
            },
            "social_networks": { 
              "dynamic": true,
              "properties": {}
            }
          }
        }
      }
    }
  }
```

<h4 id="3.8">3.8  enabled</h4>

> ELasticseaech默认会索引所有的字段，enabled设为false的字段，es会跳过字段内容，该字段只能从_source中获取，但是不可搜。而且字段可以是任意类型。

**==注意：==** 很多字段不需要搜索，只需要获取

```
 "mappings": {
    "session": {
      "properties": {
        "user_id": {
          "type":  "keyword"
        },
        "last_updated": {
          "type": "date"
        },
        "session_data": { 
          "enabled": false
        }
      }
    }
  }
```

<h4 id="3.9">3.9  fielddata</h4>

**==针对text字段==**

<h4 id="3.10">3.10  format</h4>

> format属性主要用于格式化日期

[更多内置的日期格式](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-date-format.html)

<h4 id="3.11">3.11 ignore_above</h4>

> ignore_above用于指定字段索引和存储的长度最大值，超过最大值的会被忽略

```
  "mappings": {
    "my_type": {
      "properties": {
        "message": {
          "type": "keyword",
          "ignore_above": 15
        }
      }
    }
  }
```

<h4 id="3.12">3.12 ignore_malformed</h4>

> ignore_malformed可以忽略不规则数据:即指定类型字段仍可接受其他类型数据,默认false

<h4 id="3.13">3.13 include_in_all</h4>

> include_in_all属性用于指定字段是否包含在_all字段里面，默认开启，除索引时index属性为no

<h4 id="3.14">3.14 index</h4>

> index属性指定字段是否索引，不索引也就不可搜索，取值可以为true或者false。

<h4 id="3.15">3.15 index_options</h4>

> index_options控制索引时存储哪些信息到倒排索引中

|参数|	作用|
|-----|-----|
|docs|	只存储文档编号|
|freqs|	存储文档编号和词项频率|
|positions|	文档编号、词项频率、词项的位置被存储，偏移位置可用于临近搜索和短语查询|
|offsets|	文档编号、词项频率、词项的位置、词项开始和结束的字符位置都被存储，offsets设为true会使用Postings highlighter|

<h4 id="3.16">3.16 fields</h4>

> fields可以让同一文本有多种不同的索引方式，比如一个String类型的字段，可以使用text类型做全文检索，使用keyword类型做聚合和排序。

```
  "mappings": {
    "my_type": {
      "properties": {
        "city": {
          "type": "text",
          "fields": {
            "raw": { 
              "type":  "keyword"
            }
          }
        }
      }
    }
  }
```

<h4 id="3.17">3.17 norms</h4>

> norms参数用于标准化文档，以便查询时计算文档的相关性。norms虽然对评分有用，但是会消耗较多的磁盘空间，如果不需要对某个字段进行评分，最好不要开启norms

<h4 id="3.18">3.18 null_value</h4>

> 值为null的字段不索引也不可以搜索，null_value参数可以让值为null的字段显式的可索引、可搜索

```
  "mappings": {
    "my_type": {
      "properties": {
        "status_code": {
          "type":       "keyword",
          "null_value": "NULL" 
        }
      }
    }
  }
```

<h4 id="3.19">3.19 position_increment_gap</h4>

> 为了支持近似或者短语查询，text字段被解析的时候会考虑此项的位置信息

**==针对text设置==**

<h4 id="3.20">3.20 properties</h4>

> Object或者nested类型，下面还有嵌套类型，可以通过properties参数指定


<h4 id="3.21">3.21 search_analyzer</h4>

> 大多数情况下索引和搜索的时候应该指定相同的分析器，确保query解析以后和索引中的词项一致。但是有时候也需要指定不同的分析器

<h4 id="3.22">3.22 similarity</h4>

similarity参数用于指定文档评分模型，参数有三个：

- BM25 ：ES和Lucene默认的评分模型(default_field)
- classic ：TF/IDF评分(classic_field)
- boolean：布尔模型评分 (boolean_sim_field)

<h4 id="3.23">3.23 store</h4>

> 默认情况下，自动是被索引的也可以搜索，但是不存储，这也没关系，因为_source字段里面保存了一份原始文档

<h4 id="3.24">3.24 term_vector</h4>

词向量包含了文本被解析以后的以下信息：

- 词项集合
- 词项位置
- 词项的起始字符映射到原始文档中的位置。

|参数取值	|含义|
|----|----|
no|	默认值，不存储词向量|
yes|	只存储词项集合|
with_positions|	存储词项和词项位置|
with_offsets|	词项和字符偏移位置|
with_positions_offsets|	存储词项、词项位置、字符偏移位置|

```
 "mappings": {
    "my_type": {
      "properties": {
        "text": {
          "type":        "text",
          "term_vector": "with_positions_offsets"
        }
      }
    }
  }
```

<h4 id="4.1">4.1 default mapping</h4>

> 在mapping中使用default字段，那么其它字段会自动继承default中的设置

```
  "mappings": {
    "_default_": { 
      "_all": {
        "enabled": false
      }
    },
    "user": {}, 
    "blogpost": { 
      "_all": {
        "enabled": true
      }
    }
  }
```
上面的mapping中，default中关闭了all字段，user会继承_default中的配置，因此user中的all字段也是关闭的，blogpost中开启_all，覆盖了_default的默认配置

当default被更新以后，只会对后面新加的文档产生作用

<h4 id="4.2">4.2 Dynamic field mapping</h4>

> 文档中有一个之前没有出现过的字段被添加到ELasticsearch之后，文档的type mapping中会自动添加一个新的字段。这个可以通过dynamic属性去控制，dynamic属性为false会忽略新增的字段、dynamic属性为strict会抛出异常。如果dynamic为true的话，ELasticsearch会自动根据字段的值推测出来类型进而确定mapping

|JSON格式的数据|	自动推测的字段类型|
|----|----|
|null|	没有字段被添加|
|true or false|	boolean类型|
|floating类型数字|	floating类型|
|integer|	long类型|
|JSON对象|	object类型|
|数组	|由数组中第一个非空值决定|
|string|	有可能是date类型（开启日期检测)、double或long类型、text类型、keyword类型|

日期检测默认是检测符合以下日期格式的字符串
```
[ "strict_date_optional_time","yyyy/MM/dd HH:mm:ss Z||yyyy/MM/dd Z"]
```

<h4 id="4.3">4.3 Dynamic templates</h4>

> 动态模板可以根据字段名称设置mapping，如下对于string类型的字段，设置mapping为

```
  "mappings": {
    "my_type": {
      "dynamic_templates": [
        {
          "longs_as_strings": {
            "match_mapping_type": "string",
            "match":   "long_*",
            "unmatch": "*_text",
            "mapping": {
              "type": "long"
            }
          }
        }
      ]
    }
  }
```

写入文档以后，long_num字段为long类型，long_text扔为string类型

<h4 id="4.4">4.4 Override default template</h4>

> 可以通过default字段覆盖所有索引的mapping配置

```
  "order": 0,
  "template": "*", 
  "mappings": {
    "_default_": { 
      "_all": { 
        "enabled": false
      }
    }
  }
```



