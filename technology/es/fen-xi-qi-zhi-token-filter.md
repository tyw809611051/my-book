token filter：ES内置的token filter列表。

| token filter          | logical name  | description                           |
| ----|:----:| :----|
| standard filter       | standard      |                                      |
| ascii folding filter  | asciifolding  |                                       |
| length filter         | length        | 去掉太长或者太短的                      |
| lowercase filter      | lowercase     | 转成小写                               |
| ngram filter          | nGram         |                                       |
| edge ngram filter     | edgeNGram     |                                       |
| porter stem filter    | porterStem    | 波特词干算法                            |
| shingle filter        | shingle       | 定义分隔符的正则表达式                  |
| stop filter           | stop          | 移除 stop words                        |
| word delimiter filter | word_delimiter| 将一个单词再拆成子分词                   |
| stemmer token filter  | stemmer       |                                        |
| stemmer override filter| stemmer_override|                                     |
| keyword marker filter | keyword_marker|                                        |
| keyword repeat filter | keyword_repeat|                                        |
| kstem filter          | kstem         |                                        |
| snowball filter       | snowball      |                                        |
| phonetic filter       | phonetic      | [插件](https://github.com/elasticsearch/elasticsearch-analysis-phonetic) |
| synonym filter        | synonyms      | 处理同义词                              |
| compound word filter  | dictionary_decompounder, hyphenation_decompounder | 分解复合词  |
| reverse filter        | reverse       | 反转字符串                              |
| elision filter        | elision       | 去掉缩略语                              |
| truncate filter       | truncate      | 截断字符串                              |
| unique filter         | unique        |                                        |
| pattern capture filter| pattern_capture|                                       |
| pattern replace filte | pattern_replace| 用正则表达式替换                        |
| trim filter           | trim          | 去掉空格                                |
| limit token count filter| limit       | 限制token数量                           |
| hunspell filter       | hunspell      | 拼写检查                                |
| common grams filter   | common_grams  |                                        |
| normalization filter  | arabic_normalization, persian_normalization |          |