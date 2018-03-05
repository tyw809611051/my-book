##### 变量：

   说明：变量就 上一个可以临时存储数据的一个名称，存储的数据有（整型，浮点型，字符串型等8种），运算过程中可以发生变化的的名称；

   不能只定义变量而不赋值；

  


变量的命名规则：数字，字母，下划线，不能以数字开头；

    帕斯卡命名方式：首个单词首字母小写，其他单词首字母小写
    驼峰式命名方式：首字母小写，其他单词首字母大写
    下划线命名方式：每个单词之间用下划线隔开

**数据类型**

标量类型： 整型（int）、浮点型（float）、布尔型（boolean）、字符串（string）

复合类型：数组（array）、对象（object）

特殊类型：null\(空）、资源（resource）

字符串：任何东西加上引号（单引号，双引号）之后都是字符串了；

单引号和双引号的区别：双引号解析了变量，单引号没有解析变量

如果是纯字符串建议用单引号，如果需要解析用双引号；

Null型：定义一个变量，暂时不知道其类型，可设为Null

资源类型：任何的PHP外的数据都称为“资源”，如：数据库，上传文件等，给外部的内荣做了一个“统称”

类型转换：
    - 强制转换：
        -  用函数强制转换；
    - 自动转换：
        -  float类型的自动转换
        -  布尔型的自动转换

错误控制符：@

常用的几个函数：

    header:头信息，用的最多就是编码的设置

    header\("Content-type:text/html;charset=utf-8"\);

2.echo 打印输出内容

    可以输出一个或多个值，如 echo $a,$b;

3、var\_dump（）：打印输出内容的类型和值

    可以输出一个或多个，如（var\_dump（$a,$b）;）

4:isset\(\)：检测变量是否存在（设置）

    返回布尔值：存在返回true，

    mixed：混合类型的意思

    【】：方括号里的内容可有可无；

    用来判断用户是否填写的内容；

5.empty（）：检测变量是否为空

![](index_files/b58e1d21-735d-4258-b714-d4677d56374c.jpg)

# 预定义变量

说明：php的系统自带的变量，可以直接使用，

1.$\_GET

    说明：get方式，接收表单或超链接发送的get方式的数据

  


&lt;

form action="要把数据发送到哪个页面" method="提交的方法"

&gt;

  


&lt;

input type="" name=""

&gt;

&lt;

/form

&gt;

  


![](index_files/6bc08a89-376d-40ca-ab4d-f316f031eaa0.png)

![](index_files/85e6422b-0d8d-40ba-a413-cf7ce68ad809.png)

![](index_files/cf926b1f-6eae-4b93-bdbd-9d4aaaf1e563.png)

![](index_files/190a915b-c469-4b09-bc44-f5b01ad25f5f.jpg)

## $\_POST:

![](index_files/db525a12-79cf-4899-b96c-464ee2ea1fb0.png)

![](index_files/bb4352c6-5ab6-4a29-a8ba-6a5968e4b2f9.jpg)

### include和reqiuire 

![](index_files/0167efb1-4753-43a8-9d50-e40161f658ae.png)

 include:加冒号文件名；

##### PHP标记：

1.开始符

&lt;

?php ？结束符

&gt;

每行代码称为一条语句，每条语句用；结束

自定义是区分大小写的，系统自带的关键词不去分大小写的

  


注释：单行注释//或\#

单行注释一般用于代码的上部或者后面

多行注释一般用于函数或类或对象的解释

  


2.如果文件内容是纯PHP代码，最好在文件末尾删除PHP结束标记，避免意外加入空格或者换行符

##### 从HTML中分离

处于条件语句中间时，此时 PHP 解释器会根据条件判断来决定哪些输出，哪些跳过

  


四种不同的开始结束标记：，

&lt;

?php ?

&gt;

 和 

&lt;

script language="php"

&gt;

&lt;

/script

&gt;

总是可用的

短标记：

通过

php.ini

配置文件中的指令

[short\_open\_tag](mk:@MSITStore:C:\Users\Administrator\Desktop\handbook\handbook\PHP\php_enhanced_zh.chm::/res/ini.core.html#ini.short-open-tag)

打开后才可用，或者在 PHP 编译时加入了

**--enable-short-tags**

选项 5.3版本后支持

![](index_files/ab5efd35-e642-4018-81c0-f3e98ac4942d.jpg)

asp风格标记：

## 指令分隔符

需要在每个语句结尾加个分号；

结束标记表示一个分号

  


**变量的作用域：**

    局部变量：

**  
**

    全局变量：

  


    静态变量：一般在函数内使用，变量的特点是自动销毁，加上静态方式就不自动销毁 

  


    局部转换成全局：global 声明变量 不能同时赋值

  


  


![](index_files/37c506fc-69d2-446b-8ff4-86dcab588767.png)

 Nowdoc:单引号的写法

    说明：需要解析大量的html代码和字符串

  


    语法：

  


        $str = 

&lt;

&lt;

&lt;

'nowdoc'

  


                大量的代码

  


        Nowdoc定界符结束；

  


    注意：   1.nowdoc不能解析变量

  


                    2.开始定界符，必须夹单引号，

  


                    3.结束定界符不需要加单引号

  


                    4.其他的和heredoc一样

  


![](index_files/fa2b60e3-0256-4b52-99d0-40a82af670a0.png)

