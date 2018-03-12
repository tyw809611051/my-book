#### while循环
```
while 判断条件：
    statements
```

计算 1 到 100 的总和：
```
#!/usr/bin/env python3
 
n = 100
 
sum = 0
counter = 1
while counter <= n:
    sum = sum + counter
    counter += 1
 
print("Sum of 1 until %d: %d" % (n,sum))

#结果
Sum of 1 until 100: 5050
```

#### for循环
```
for <variable> in <sequence>:
	<statements>
else:
	<statements>
```

**示例**
```
>>> languages = ["C", "C++", "Perl", "Python"] 
>>> for x in languages:
...     print x
... 
C
C++
Perl
Python
>>> 
```

#### range函数

遍历数字序列，可以使用内置range()函数。它会生成数列
```
>>> for i in range(5):
...     print(i)
...
0
1
2
3
4

#range指定区间的值
>>> for i in range(5,9) :
	print(i)
 
	
5
6
7
8

#range以指定数字开始并指定不同的增量(甚至可以是负数;有时这也叫做'步长')
>>> for i in range(0, 10, 3) :
	print(i)
 
	
0
3
6
9

#结合range()和len()函数以遍历一个序列的索引
>>> a = ['Mary', 'had', 'a', 'little', 'lamb']
>>> for i in range(len(a)):
...     print(i, a[i])
...
0 Mary
1 had
2 a
3 little
4 lamb

#range()函数来创建一个列表
>>> list(range(5))
[0, 1, 2, 3, 4]
>>>
```