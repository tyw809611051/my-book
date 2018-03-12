**表类型与引擎有关，2大类：**

* 事务安全性储存引擎：InnoDB,BDB

* 非事务安全性储存引擎：MyISAM、memory

![](/img/Language/MySQL/engine/87445636-8e89-48c1-b480-4b2a5e16e6e6.png)

#### 各个引擎的特点：

**MyISAM:**

    不支持事务

    不支持外键

    支持默认的全文索引

    执行速度快（添加，修改）

    需要定时进行优化 optimize table 表名



**innodb:**

    1.支持事务

    2.支持外键

    3.并发性好

    4.如果我们需要支持事务，则选择这个



**mermory:**

    1.不支持事务

    2.不支持外键

    3.数据是在内存中，操作速度很快

        操作速度 内存 &gt;小文件&gt;数据库

![](/img/Language/MySQL/engine/34b3b8ec-74d1-47be-9355-0f11d2b00f7c.png)

![](/img/Language/MySQL/engine/7ef488f5-3579-450d-aae8-c2ba411ff75b.jpg)

修改储存引擎的语法：

    alter table 表名 engine =xx;

