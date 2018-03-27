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