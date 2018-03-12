源文件指定编码
```
# -*- coding: cp-1252 -*-
```

#### 标识符
- 第一个字符必须是字母表中字母或下划线
- 其他部分由字母、数字和下划线组成
- 对大小写敏感

#### 关键字
> 命名不要与关键字相同
```
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

#### 注释
- 单行注释：#开头
- 多行注释:三个单/双引号'''xxx'''

#### 字符串
- python中单引号和双引号使用完全相同。
- 使用三引号('''或""")可以指定一个多行字符串。
- 转义符 '\'
- 自然字符串， 通过在字符串前加r或R。 如 r"this is a line with \n" 则\n会显示，并不是换行。
- python允许处理unicode字符串，加前缀u或U， 如 u"this is an unicode string"。
- 字符串是不可变的。
- 按字面意义级联字符串，如"this " "is " "string"会被自动转换为this is string。
