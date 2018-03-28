###注册表
|选项|描述|
|---|---|
|REG QUERY |查询注册表|
 | REG ADD |添加|
 | REG DELETE |删除|
 | REG COPY |复制|
 | REG SAVE |保存配置信息|
 | REG RESTORE 还原||
 | REG LOAD |加载配置文件|
 | REG UNLOAD |卸载配置文件中信息|
 | REG COMPARE |比较|
 | REG EXPORT |从文件导出注册表|
  |REG IMPORT |从文件导入注册表|
**读取注册表**
语法
```
REG QUERY KeyName [/v [ValueName] | /ve] [/s][/f Data [/k] [/d] [/c] [/e]] [/t Type] [/z] [/se Separator][/reg:32 | /reg:64]
```
|选项|描述|
|---|---|
| KeyName | [\\Machine\]FullKeyMachine - 远程机器名称，省略当前机器的默认值。在远程机器上只有 HKLM 和 HKU 可用。FullKey - 以 ROOTKEY\SubKey 名称形式ROOTKEY - [ HKLM | HKCU | HKCR | HKU | HKCC ]SubKey  - 在选择的 ROOTKEY 下的注册表项的全名
| /v   |    具体的注册表项值的查询。如果省略，会查询该项的所有值。只有与 /f 开关一起指定的情况下，此开关的参数才是可选的。它指定，只在值名称中搜索。
  |/ve    |  查询默认值或空值名称(默认)。|
  |/s    |   循环查询所有子项和值(如 dir /s)。|
 | /se    |  为 REG_MULTI_SZ 在数据字符串中指定分隔符(长度只为 1 个字符)。默认分隔符为 "\0"。|
  |/f      | 指定搜索的数据或模式。如果字符串包含空格，请使用双引号。默认为 "*"。|
  |/k  |     指定只在项名称中搜索。|
|  /d   |    指定只在数据中搜索。|
 | /c      | 指定搜索时区分大小写。默认搜索为不区分大小写。|
  |/e  |     指定只返回完全匹配。默认是返回所有匹配。|
  |/t   |    指定注册表值数据类型。有效的类型是:REG_SZ, REG_MULTI_SZ, REG_EXPAND_SZ,REG_DWORD, REG_QWORD, REG_BINARY, REG_NONE默认为所有类型。|
 | /z     |  详细: 显示值名称类型的数字等值。|
| /reg:32 | 指定应该使用 32 位注册表视图访问的注册表项。|
| /reg:64  |指定应该使用 64 位注册表视图访问的注册表项。|


**添加**
语法
```
REG ADD [ROOT\]RegKey /v ValueName [/t DataType] [/S Separator] [/d Data] [/f]
REG ADD [ROOT\]RegKey /ve [/d Data] [/f]
```

|选项|描述|
|---|---|
|ValueName |- 在选定的RegKey下的值，进行编辑。|
|/d Data |- 要存储为“字符串”，整数等的实际数据。|
|/f |- 强制更新而不提示“值存在，覆盖Y/N”。|
|/S Separator| - 在REG_MULTI_SZ值中用作分隔符的字符。 默认值是"\0"。|
|/t DataType| - 这些是根据注册表标准定义的数据类型，可以是REG_SZ (默认)、REG_DWORD、REG_EXPAND_SZ、REG_MULTI_SZ|

**删除**
> 删除是通过REG DEL命令完成的。 请注意，为了从注册表中删除值，需要在系统上拥有足够的权限来执行此操作
```
REG DELETE KeyName [/v ValueName | /ve | /va] [/f] [/reg:32 | /reg:64]
 ```
 |选项|描述|
 |---|---|
 |ValueName | 所选项下面的要删除的值名称。如果省略，则删除该项下面的所有子项和值。|
 | /ve    |    删除空值名称的值(默认)。|
 | /va   |     删除该项下面的所有值。|
 | /f     |    不用提示，强制删除。|
 
 **复制**
 语法
 ```
 REG COPY KeyName1 KeyName2 [/s] [/f] [/reg:32 | /reg:64]
 ```
 |选项|描述|
|---|---|
|/s    |     复制所有子项和值。|
 | /f       |  不用提示，强制复制。|