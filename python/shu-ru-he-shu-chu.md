#### 输出格式
- 表达式语句和 print() 函数。(第三种方式是使用文件对象的 write() 方法; 标准输出文件可以用 sys.stdout 引用。)

- 如果你希望输出的形式更加多样，可以使用 str.format() 函数来格式化输出值。

- 如果你希望将输出的值转成字符串，可以使用 repr() 或 str() 函数来实,str() 函数返回一个用户易读的表达形式。repr() 产生一个解释器易读的表达形式。

```
>>> s = 'Hello, world.'
>>> str(s)
'Hello, world.'
>>> repr(s)
"'Hello, world.'"
>>> str(1/7)
'0.14285714285714285'
>>> x = 10 * 3.25
>>> y = 200 * 200
>>> s = 'The value of x is ' + repr(x) + ', and y is ' + repr(y) + '...'
>>> print(s)
The value of x is 32.5, and y is 40000...
>>> #  repr() 函数可以转义字符串中的特殊字符
... hello = 'hello, world\n'
>>> hellos = repr(hello)
>>> print(hellos)
'hello, world\n'
>>> # repr() 的参数可以是 Python 的任何对象
... repr((x, y, ('spam', 'eggs')))
"(32.5, 40000, ('spam', 'eggs'))"
```

**旧式字符串格式化**
```
>>> import math
>>> print('The value of PI is approximately %5.3f.' % math.pi)
The value of PI is approximately 3.142.
```

**读和写文件**
open() 将会返回一个 file 对象，基本语法格式如下:
```
#第一个参数为要打开的文件名。
#第二个参数描述文件如何使用的字符。 mode 可以是 'r' 如果文件只读, 'w' 只用于写 (如果存在同名文件则将被删除), 和 'a' 用于追加文件内容; 所写的任何数据都会被自动增加到末尾. 'r+' 同时用于读写。 mode 参数是可选的; 'r' 将是默认值。
>>> f = open('/tmp/workfile', 'w')
```

**文件对象的方法**
**f.read():**读取一定数目的数据, 然后作为字符串或字节对象返回
**f.readline():**会从文件中读取单独的一行。换行符为 '\n'。f.readline() 如果返回一个空字符串, 说明已经已经读取到最后一行
**f.readlines():**f.readlines() 将返回该文件中包含的所有行。如果设置可选参数 sizehint, 则读取指定长度的字节, 并且将这些字节按行分割
**f.write():**将 string 写入到文件中, 然后返回写入的字符数
**f.tell():**返回文件对象当前所处的位置, 它是从文件开头开始算起的字节数
**f.seek():**如果要改变文件当前的位置, 可以使用 f.seek(offset, from_what) 函数,form_what是 0 表示开头, 如果是 1 表示当前位置, 2 表示文件的结尾
**f.close():**在文本文件中 (那些打开文件的模式下没有 b 的), 只会相对于文件起始位置进行定位

#### pickle 模块
> 实现了基本的数据序列和反序列化

```
#使用pickle模块将数据对象保存到文件
 
import pickle
 
data1 = {'a': [1, 2.0, 3, 4+6j],
         'b': ('string', u'Unicode string'),
         'c': None}
 
selfref_list = [1, 2, 3]
selfref_list.append(selfref_list)
 
output = open('data.pkl', 'wb')
 
# Pickle dictionary using protocol 0.
pickle.dump(data1, output)
 
# Pickle the list using the highest protocol available.
pickle.dump(selfref_list, output, -1)
 
output.close()

#使用pickle模块从文件中重构python对象
 
import pprint, pickle
 
pkl_file = open('data.pkl', 'rb')
 
data1 = pickle.load(pkl_file)
pprint.pprint(data1)
 
data2 = pickle.load(pkl_file)
pprint.pprint(data2)
 
pkl_file.close()
```