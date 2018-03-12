## .约束的分类，

**1.当一个字段设置成主键约束后，该字段不可为空，也不可重复**

语法：字段名，字段类型，

primary key 

细节：
- 1,，不能重复，不能为空

- 2.一张表最多只能有一个主键，可以是复合主键，只要复合主键都不一样即可

- 3.一张表总有一个主键，通常为整型

- 4.主键的两种指定方式：（1）就在创建表时，直接在字段（列）后面指定。（2）在表的后面指定

- 5.如果一个字段设置成not null 并 union 使用效果上像主键

- 6.通过desc 表名，查看主键

  


**2.唯一（unique）约束，当一个字段设置成唯一约束后，该字段就不可以重复，    是否可以为null，取决于是否设置了not null**

3.not null约束，设置后，该字段不能为null

**4.外键约束，当2个表有数据依赖关系时设置，这时不能随意的删除或修改数据**

![](/img/Language/MySQL/constraint/836df9e1-c0cb-4f7c-afba-de65e92905b6.jpg)

![](/img/Language/MySQL/constraint/23dcc302-5b13-4155-a4a8-440983f5f817.png)

![](/img/Language/MySQL/constraint/dbea24d1-7379-43dd-8ba1-6eaa3fab20be.png)

5.check约束，支持语句校验

