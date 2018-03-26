### 字符串合集
- 创建字符串
    **示例**
```
@echo off 
:: This program just displays Hello World 
set message=Hello World 
echo %message%
```

- 空字符串
    **示例**
    ```
 @echo off 
SET a= 
SET b=Hello 
if [%a%]==[] echo "String A is empty" 
if [%b%]==[] echo "String B is empty "
#结果
String A is empty
```
要检查是否存在空字符串，需要在方括号中包含变量名，并将其与方括号中的值进行比较

- 字符串插值
    **示例**
    ```
@echo off 
SET a=Hello 
SET b=World 
SET /A d=50 
SET c=%a% and %b% %d%
echo %c%
#结果
Hello and World 50
```
- 字符串长度
> 没有定义用于查找字符串长度的长度函数。 可以使用自定义的函数实现这个目的

```
@echo off
set str=Hello World
call :strLen str strlen
echo String is %strlen% characters long
exit /b

:strLen
setlocal enabledelayedexpansion

:strLen_Loop
   if not "!%1:~%len%!"=="" set /A len+=1 & goto :strLen_Loop
(endlocal & set %2=%len%)
goto :eof
#结果
String is 11 characters long
```

- 截取字符串

```
%variable:~num_chars_to_skip% 
%variable:~num_chars_to_skip,num_chars_to_keep%
Bat
这可以包括负数 -

%variable:~num_chars_to_skip, -num_chars_to_keep%
%variable:~-num_chars_to_skip,num_chars_to_keep%
%variable:~-num_chars_to_skip,-num_chars_to_keep%
```

- 字符串替换功能

```
@echo off 
set str=Batch scripts is easy. It is really easy. 
echo %str% 
:: 替换is
set str=%str:is=% 
echo %str%
:: 替换空格
set str=%str:=% 
echo %str%
#结果
Batch scripts is easy. It is really easy. 
Batch scripts easy. It really easy.
```
