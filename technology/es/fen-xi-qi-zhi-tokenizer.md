**1.standard**

|设置|描述|
|----|----|
|max\_token\_length|最大的标记长度。如果一个令牌被超过这个长度再分割max\_token\_length间隔.默认值为二百五十五|

**2.edgeNGram**

|设置|描述|默认值|
|---|---|---|
|min_gram|在一个单一的N-gram的码点的最小尺寸|1|
|max_gram|在一个单一的N-gram的码点的最大尺寸|2
|token_chars|字符类保持thetokens，Elasticsearch将字符不属于任何阶级分裂。|[]（把所有字符）
|token_chars接受下列字符类：||
|letter	|例如a，B，ï或京
|digit	|例如3或七|
|whitespace	|例如" "或“\n”|
|punctuation	|例如!或“|
|symbol	|例如$或√|

**3.keyword**

|设置|描述|
|---|---|
|buffer_size|缓冲区大小的术语。默认值为256|

**4.letter**
定义：相邻字母的最大字符串

**5.lowercase**

**6.nGram**
同edgengram

**7.pattern**

|设置|描述|
|---|---|
|pattern|正则表达式模式，默认为\W+|
|flags|正则表达式的旗帜|
|group|提取到令牌的组。默认值为-1（分裂）|

```
pattern = '([^']+)'
group   = 0
input   = aaa 'bbb' 'ccc'
```

**8.uax_url_email**

|设置|描述|
|---|---|
|max\_token\_length|最大的标记长度。如果一个令牌被超过这个长度然后丢弃。默认值为255|

**9.Path Hierarchy**

|设置|描述|
|--|--|
|delimiter|人物使用的分隔符，默认为/|
|replacement|一个可选的替换字符使用。默认的delimiter|
|buffer_size|缓冲区大小使用，默认为1024|
|reverse|以相反的顺序生成令牌，默认为false|
|skip|控件的初始记号跳过，默认为0|

**10.classic**

特别处理公司名称、电子邮件地址和域名