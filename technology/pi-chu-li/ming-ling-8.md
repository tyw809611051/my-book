###文件集合

**删除文件**
语法
> DEL [/P] [/F] [/S] [/Q] [/A[[:]attributes]] names

|选项|描述|
|---|---|
|Names|指定一个或多个文件或目录的列表。 通配符可能被用来删除多个文件。 如果指定了一个目录，则该目录内的所有文件都将被删除|
|/P|提示在删除每个文件之前进行确认。|
|/F|强制删除只读文件。|
|/S|删除所有子目录中的特定文件。|
|/Q|安静模式，不要问是否可以删除全局通配符。|
|/A|根据属性选择要删除的文件。|
|attributes|R只读文件，S系统文件，H隐藏文件，A文件准备归档 - 前缀含义不是|

```
del c:\*.bat
#*(星号)是一个模式的字符。 *.bat表示要删除c:\目录下的所有以.bat结尾的文件
del c:\?est.tmp
#?(问号)是一个字母的单个通配符。在上面的例子中使用这个命令会删除任何以est.tmp结尾的文件，比如pest.tmp或者test.tmp这样的文件都会被删除。
```
**重命名文件**
```
RENAME [drive:][path][directoryname1 | filename1] [directoryname2 | filename2]
```

**移动文件**
```
MOVE [/Y | /-Y] [drive:][path]filename1[,...] destination
```
|选项|	描述|
|---|---|
|[drive:][path]filename1|	指定要移动的文件的位置和名称|
|destination|	指定文件的新位置。 目标可以由驱动器号和冒号，目录名称或组合组成。 如果只移动一个文件，则在移动文件时，如果要重命名文件，也可以包含一个文件名。|
|[drive:][path]dirname1	|指定要重命名的目录。|
|dirname2|	指定目录的新名称。|
|/Y	|禁止提示以确认要覆盖现有的目标文件。|
/-Y	|提示确认要覆盖现有的目标文件。|