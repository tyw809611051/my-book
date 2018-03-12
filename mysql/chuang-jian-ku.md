**语法：create database name**

![](/img/Language/MySQL/make_databases/465ed23f-abef-4e09-ba40-a4a345332069.png)

 说明：

        1，红色的字都是关键字，不能修改

        2.【】是可以选择，可以有，也可以没有

        3.CREATE 关键字大写是一种规范

        4.character set 表示该数据库的字符集是什么，通常我们是utf8,可以保存中文，

        5.collate ：表示校验规则，通常是utf8\_general\_ci\(默认，字母不区分大小写），utf8\_bin是区分大小写的，会对查询，排序有影响



不同的字符集和校验规则有什么影响

    1.如果数据库的字符集是utf8，那么表也是utf8，这样可以保存中文字符

    2.如果使用Latin字符集，不能添加中文字符

    3.字符集是用来控制，可以将什么样的字符添加到表中，而校验是影响查询和排序的



常用的校验规则：

    国内常用\_默认：utf8\_general\_ci//表示不区分大小写

        utf8\_bin//区分大小写，默认排序是按照ASCII码来排序



**创建表：**

**    语法：create table 表名（字段名称 字段类型 字段属性，名称1，类型2.，属性2）**

**    说明**

**    字段名称：给每列起一个名字**

**    字段类型：限制当前列中的数据方式，有：数值型（tinyint,int,bigint等）、字符串型（char,varchar,text等）、日期时间型（date，time）**

**    字段属性：**

**            null:允许为空**

**            not null:不允许为空**

**            default：默认值**

**            auto increment:自动增长（只能给数字）**

**            primary key:给某个字段加上“主键” 不能为空，不能重复，一般给id加，一张表只有一个主键  
**

![](/img/Language/MySQL/make_databases/f656e00d-3dc2-4752-83ad-4fe72b230ec6.jpg)

