### 数组合集

#### 创建一个数组
```
set a[0]=1
set list=1 2 3 4 
(for %%a in (%list%) do ( 
   echo %%a 
))
#结果
1
2
3
4
```

#### 访问数组
```
@echo off
set a[0]=1 
set a[1]=2 
set a[2]=3 
echo The first element of the array is %a[0]% 
echo The second element of the array is %a[1]% 
echo The third element of the array is %a[2]%
```

#### 修改数组
```
@echo off 
set a[0]=1 
set a[1]=2 
set a[2]=3 
Rem Setting the new value for the second element of the array 
Set a[1]=5 
echo The new value of the second element of the array is %a[1]%
#结果
The new value of the second element of the array is 5
```

#### 迭代数组
```
@echo off 
setlocal enabledelayedexpansion 
set topic[0]=comments 
set topic[1]=variables 
set topic[2]=Arrays 
set topic[3]=Decision making 
set topic[4]=Time and date 
set topic[5]=Operators 

for /l %%n in (0,1,5) do ( 
   echo !topic[%%n]! 
)
#结果
Comments 
variables 
Arrays 
Decision making 
Time and date 
Operators
```

#### 数组长度
```
@echo off 
set Arr[0]=1 
set Arr[1]=2 
set Arr[2]=3 
set Arr[3]=4 
set "x=0" 
:SymLoop 

if defined Arr[%x%] ( 
   call echo %%Arr[%x%]%% 
   set /a "x+=1"
   GOTO :SymLoop 
)
echo "The length of the array is" %x%
#结果
The length of the array is 4
```
