#### 内置分析器
**1. standard**

优点：能进行较好拆分
缺点：不能分词“-”和“/”

|设置|描述|
|----|----|
|stopwords|一个初始化停止过滤和停用词列表。默认值为空的停用词列表检查停止分析仪更多的细节|
|max\_token\_length|最大的标记长度。如果一个标记被认为exceedsthis长度然后分裂max\_token_length间隔.默认值为二百五十五|
**2. Simple**

优点：连字符较好拆分
缺点：不识别数字，特殊字符

**3.Whitespace**

特点：空格拆分

**4. Stop**

特点：不区分数字，特殊字符

**5. Keyword**

特点：不拆分

**6. Pattern**

特点：可以使用正则来匹配

**7. Language**

**8. Snowball**

**9. Custom**