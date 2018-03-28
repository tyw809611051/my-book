#### 函数
- **函数声明**：告诉编译器一个函数的名字，返回类型和参数
- **函数定义**：提供函数的实际主体

```
:function_name 
Do_something 
EXIT /B 0
```

**调用一个函数**
```
call :function_name
```
如何在主程序调用一个函数
```
@echo off 
SETLOCAL 
CALL :Display 
EXIT /B %ERRORLEVEL% 
:Display 
SET /A index=2 
echo The value of index is %index% 
EXIT /B 0
```
注意：定义主程序时需要注意的一点是确保在主程序中放入EXIT / B%ERRORLEVEL%语句，以便将主程序的代码与函数分开

**传递参数**
```
Call :function_name parameter1, parameter2… parametern
```
**通过使用代字符(~)字符以及参数的位置，来在函数内部访问参**
```
@echo off
SETLOCAL
CALL :Display 5 , 10
EXIT /B %ERRORLEVEL%
:Display
echo The value of parameter 1 is %~1
echo The value of parameter 2 is %~2
EXIT /B 0
#结果
The value of parameter 1 is 5
The value of parameter 2 is 10
```

**返回值**
```
@echo off
SETLOCAL
CALL :SetValue value1,value2
echo %value1%
echo %value2%
EXIT /B %ERRORLEVEL%
:SetValue
set "%~1=5"
set "%~2=10"
EXIT /B 0
#结果
5
10
```