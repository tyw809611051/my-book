定义函数使用 def 关键字，一般格式如下
```
def  函数名（参数列表）：
    函数体
```

**函数中带上参数变量**

```
def area(width, height):
    return width * height
 
def print_welcome(name):
    print("Welcome", name)
 
print_welcome("Fred")
w = 4
h = 5
print("width =", w, " height =", h, " area =", area(w, h))
```

#### 函数变量作用域
定义在函数内部的变量拥有一个局部作用域，定义在函数外的拥有全局作用域
```
#!/usr/bin/env python3
a = 4  # 全局变量
 
def print_func1():
    a = 17 # 局部变量
    print("in print_func a = ", a)
def print_func2():   
    print("in print_func a = ", a)
print_func1()
print_func2()
print("a = ", a)
```

#### 关键字参数

```
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.")
    print("-- Lovely plumage, the", type)
    print("-- It's", state, "!")
```

#### 返回值
使用return语句，可以将函数作为一个值赋值给指定变量
```
def return_sum(x,y):
    c = x + y
    return c
 
res = return_sum(4,5)
print(res)
```

返回空值
```
def empty_return(x,y):
    c = x + y
    return
 
res = empty_return(4,5)
print(res)
```

#### 可变参数列表

不常用的选择是可以让函数调用可变个数的参数.这些参数被包装进一个元组(查看元组和序列).在这些可变个数的参数之前,可以有零到多个普通的参数

```
def arithmetic_mean(*args):
    sum = 0
    for x in args:
        sum += x
    return sum
 
print(arithmetic_mean(45,32,89,78))
print(arithmetic_mean(8989.8,78787.78,3453,78778.73))
print(arithmetic_mean(45,32))
print(arithmetic_mean(45))
print(arithmetic_mean())
```