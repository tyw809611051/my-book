#### 定义
语法格式
```
class ClassName:
    <statement-1>
    .
    .
    .
    <statement-N>
```

#### 类对象
属性引用和实例化
属性引用使用和 Python 中所有的属性引用一样的标准语法：obj.name。
```
class MyClass:
    """A simple example class"""
    i = 12345
    def f(self):
        return 'hello world'
#实例化类
x = MyClass()
```
类定义了 __init__() 方法的话，类的实例化操作会自动调用 __init__() 方法

#### 类的方法
使用def关键字可以为类定义一个方法，与一般函数定义不同，类方法必须包含参数self,且为第一个参数
```
#类定义
class people:
    #定义基本属性
    name = ''
    age = 0
    #定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0
    #定义构造方法
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print("%s is speaking: I am %d years old" %(self.name,self.age))
 
 
p = people('tom',10,30)
p.speak()
```

#### 继承
语法格式
```
class DerivedClassName(BaseClassName1):
    <statement-1>
    .
    .
    .
    <statement-N>
```

**示例**
```
#单继承示例
class student(people):
    grade = ''
    def __init__(self,n,a,w,g):
        #调用父类的构函
        people.__init__(self,n,a,w)
        self.grade = g
    #覆写父类的方法
    def speak(self):
        print("%s is speaking: I am %d years old,and I am in grade %d"%(self.name,self.age,self.grade))
 
 
 
s = student('ken',20,60,3)
s.speak()
```

#### 类属性与方法

**类的私有属性**
__private_attrs：两个下划线开头，声明该属性为私有，不能在类地外部被使用或直接访问。在类内部的方法中使用时 self.__private_attrs。

**类的方法**
在类地内部，使用def关键字可以为类定义一个方法，与一般函数定义不同，类方法必须包含参数self,且为第一个参数

**类的私有方法**
__private_method：两个下划线开头，声明该方法为私有方法，不能在类地外部调用。在类的内部调用 slef.__private_methods。

类的专有方法：
|方法|解释|
|---|---|
|__init__ |构造函数，在生成对象时调用|
|__del__ |析构函数，释放对象时使用|
|__repr__ |打印，转换|
|__setitem__|按照索引赋值|
|__getitem__|按照索引获取值|
|__len__|获得长度|
|__cmp__|比较运算|
|__call__|函数调用|
|__add__|加运算|
|__sub__|减运算|
|__mul__|乘运算|
|__div__|除运算|
|__mod__|求余运算|
|__pow__|称方|