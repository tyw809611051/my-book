> 模块是一个包含所有你定义的函数和变量的文件，其后缀名是.py。模块可以被别的程序引入，以使用该模块中的函数等功能。这也是使用python标准库的方法

```
#!/usr/bin/python3
# Filename: using_sys.py
 
import sys
 
print('命令行参数如下:')
for i in sys.argv:
	print(i)
 
print('/n/nThe PYTHONPATH is', sys.path, '/n')

#执行结果
E:\python33\src>python using_sys.py 参数1 参数2
命令行参数如下:
using_sys.py
参数1
参数2
/n/nThe PYTHONPATH is ['E:\\python33\\src', 'C:\\Windows\\system32\\python33.zip
', 'E:\\python33\\DLLs', 'E:\\python33\\lib', 'E:\\python33', 'E:\\python33\\lib
\\site-packages'] /n

```

1、import sys引入python标准库中的sys.py模块；这是引入某一模块的方法。
2、sys.argv是一个包含命令行参数的列表。
3、sys.path包含了一个Python解释器自动查找所需模块的路径的列表。

导入模块的所有函数，变量
```
>>> from fibo import *
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

导入模块内指定的函数，变量
```
>>> from fibo import fib, fib2
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

**__name__属性**
模块被引入时，模块中的某一程序块不执行,__name__属性来使该程序块仅在该模块自身运行时执行

```
#!/usr/bin/python3
# Filename: using_name.py
 
if __name__ == '__main__':
	print('程序自身在运行')
else:
	print('我来自另一模块')
```

**dir() 函数**
内置的函数 dir() 可以找到模块内定义的所有名称。以一个字符串列表的形式返回
```
>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']

#没有给定参数，会罗列出当前定义的所有名称
>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir() # 得到一个当前模块中定义的属性列表
['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
```