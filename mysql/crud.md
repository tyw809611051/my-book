说明：

    对数据的操作主要是增加\(insert\)、修改（update）、删除\(delete\)、查询（select）



## insert语句：

    1.插入的数据应与字段的数据类型相同

        即如果一个字段是float的类型，集不能将string类型插入



**update语句**

![](/img/Language/MySQL/crud/49ff71f2-2f6f-4aad-a3ef-167fae94fd6d.png)

 1.红色字是关键字

  2.set后面可以有多列，表示一次修改多列，列名=后可以带表达式

  3.where表条件，不写，表示对所有修改



![](/img/Language/MySQL/crud/3e8ed050-9ca6-4259-a0d8-0c633233397a.png)

delete语句

    说明：删除表的记录，不是删除表本身

语法：delete from 表名 where语句

快速复制一张表

    1.创建一个相同的表，create table temp\_employee like employee;

    2.将数据导入表中：insert into 表名 select \* from 数据表

    3.导入部分字段，则要求其他字段有默认值

![](/img/Language/MySQL/crud/273f3d5c-7cfd-43e4-b1db-64c6d54724eb.png)

![](/img/Language/MySQL/crud/10de54c5-4af7-4de0-b5d1-d3b5b3025b10.jpg)

# select语句

![](/img/Language/MySQL/crud/24f8e2ba-765a-4d66-bef0-b854177f905d.png)

    distinct是一个关键字，作用：去掉重复的记录，当结果完全相同时 才过滤

    \*表示将该表的所有字段都返回，也可指定字段，实际中，较少

    通常会带where子句

![](/img/Language/MySQL/crud/1de34b3d-c4a5-481c-87f8-0755e43ee865.png)

![](/img/Language/MySQL/crud/c802134d-aa83-4d1a-9e7a-7c7a17639ecb.png)

![](/img/Language/MySQL/crud/a81bd9d8-1187-405b-b379-c0a1c7487e79.png)

![](/img/Language/MySQL/crud/e91ee9ae-5d06-4edd-9680-412f14eb1ec9.png)

![](/img/Language/MySQL/crud/1cf81994-7ec8-4edd-9e32-a02b3cfc2beb.png)

### select-where子句

![](/img/Language/MySQL/crud/e731bf8e-8af2-4dd0-8758-3c7b1e119724.png)

Order by子句

    用于对检索的结果排序

\(1\)一般来说，我们的order by是放在where子句后面.

\(2\)order by column asc\|desc说明, order by后面跟的是字段名，表示对哪个字段进行排序,默认是asc升序排序。

\(3\)order by可以跟多个字段，表示对多个字段排序，排序是先排前面的字段，再排后面的字段.

\(4\)默认排序是升序\(不写\),如果希望降序排列，则需要写上desc

### ![](/img/Language/MySQL/crud/0.48123532766476274.png)  函数：作用在select后面的列名上

count（）:统计有多少单元，\*与列的区别就是列对null

![](/img/Language/MySQL/crud/0.8558786793146282.png)

count函数可以count\(\*\)或者count\(列名\);

count\(\*\):统计满足条件的记录总数.

count\(列名\)：统计满足条件列，共有多少条,注意:如果列的值为null ,则不统计这里.

区别：count\(\*\)是统计满足条件的总记录数.

count\(列名\)，是统计满足条件的列有多少条，同时会去掉null列.

sum（）：统计总和

![](/img/Language/MySQL/crud/0.38696343055926263.png)

   \(1\)    sum\(列名\) 是用于求和, 列的类型应该是数值还有意义.

   \(2\)    sum\(列名1..+列名2\), 可以对多列一次性求和.

AVG（）：求平均值

max（）/min（）：返回一列的的最大值；

对数值型的字段有效



1.1group by子句

l基本的说明：当我们要对查询的结果，进行分组时\(分组显示或者分组统计\)，那么我们就会使用到group by子句.

![](/img/Language/MySQL/crud/0.17638612305745482.png)

\(2\)    group by 列1\(字段1\), 列2\(字段2\)  根据那列来进行分组.

\(3\)    having 是可选项, 该关键字用于对分组后的结果进行过滤

