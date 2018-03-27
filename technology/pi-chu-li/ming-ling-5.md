### IF语句

```
#检查整型变量
@echo off 
SET /A a=5 
SET /A b=10 
SET /A c=%a% + %b% 
if %c%==15 echo "The value of variable c is 15" 
#检查字符串变量
SET str1=String1 
SET str2=String2 
if %str1%==String1 echo "The value of variable String1" 
#检查命令行参数
echo %1  
if %1%==1 echo "The value is 1" 
```

**测试变量是否存在**
> if defined somevariable somecommand

**示例**
```
@echo off 
SET str1=String1 
SET str2=String2 
if defined str1 echo "Variable str1 is defined"
#结果
"Variable str1 is defined" 
```
**测试文件是否存在**
> If exist somefile.ext do_something

```
@echo off 
if exist C:\set2.txt echo "File exists" 
if exist C:\set3.txt (echo "File exists") else (echo "File does not exist")
#结果
"File exists"
"File does not exist"
```

**嵌套多个if语句**
```
所以只有当条件1和条件2都满足时，才会执行do_something块中的代码。
if(condition1) if (condition2) do_something
```

**if errorlevel**
```
if errorlevel n somecommand
用于测试运行的最后一个命令的退出代码。 各种命令发出整数退出代码来表示命令的状态。 通常，如果命令成功完成，则命令通过传递0;如果命令失败，命令通过传递1
```