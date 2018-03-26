#### echo 和 @
> @ 隐藏它后面的这一行的命令本身(只能影响当前行)
echo 输出/回显

```
#关闭/开启回显
echo off/on 

#输出
echo list
```

#### 文档注释
```
rem 这是注释
```

#### 命令行参数
批处理支持命令行参数的概念，其参数可以再被调用时传递给批处理文件。参数可以通过变量%1,%2,%3等从批处理文件调用
```
@echo off
echo %1
echo %2
echo %3
```
将上面存储为文件,并运行

```
C:\Users\Administrator\Desktop>a.cmd 1 2 3
#结果
1
2
3
请按任意键继续. . .
```

#### SET命令
> 显示、设置或删除 cmd.exe 环境变量。

**基本用法**
```
SET [variable=[string]]

  variable  指定环境变量名。
  string    指定要指派给变量的一系列字符串。
```

**示例**
```
@echo off 
set message=Hello World 
echo %message%
#结果
Hello World 
```
也可进行表达式设置
> SET /A expression
```
@echo off 
SET /A a=5 
SET /A b=10 
SET /A c=%a% + %b% 
echo %c%
#结果
15
```

#### 局部、全局和环境变量
调用SETLOCAL命令，使变量在局部范围之内，变量在ENDLOCAL语句后被销毁
```
@echo off 
set globalvar=5
SETLOCAL
set var=13145
set /A var=%var% + 5
echo %var%
echo %globalvar%
ENDLOCAL
#结果
13150
5
```
**如果有跨批处理文件使用的变量，最好使用环境变量**