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
    