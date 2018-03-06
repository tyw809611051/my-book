**流程**

**1.连接数据库：mysql\_connect\(服务器地址，用户名，密码）；**

**2.选择数据库：mysql\_select\_db并设置通信编码（mysql\_query\("set names utf8"\)）;**

**3.准备的SQL语句（￥sql="select\*from 表名"）;**

**4.发送SQL语句到服务器\(mysql\_query\($sql\)\);**

**5.服务器接收SQL语句（进行解析-是有结果集--数据-假，没有结果集-真或假）**

**6.客户端接收结果（进行判断）**

**7.继续有结果集的结果进行解析（把资源变化成能看懂的数据）**

**8.关闭数据库连接；**

**               //html编码 **

**&lt;meta charset="utf-8"&gt;**

** //php编码 header\("Content-type:text/html;charset=utf-8"\);**

** //文本工具设置编码**

** //php操作数据库编码 mysql\_query\("set names utf8"\);**

** //数据库设置编码 添加库：create database 数据库民称 charset=utf8;**

**  
**

**1.连接数据库**

![](img/Language/PHP/databases/884c15cd-f00a-4cfc-bea3-af5e99f31f7c.png)

**  
**

![](img/Language/PHP/databases/ca089ca2-6f94-4e6d-ba24-d3ae4351e9bd.png)

![](img/Language/PHP/databases/2ff7fc7b-7870-4380-8e02-5335402b9101.jpg)

2.选择数据库

![](img/Language/PHP/databases/ca169940-2641-4f1a-98e8-9e803d0e128f.png)

  


![](img/Language/PHP/databases/05f9644e-28db-4049-87cd-f2f7f2e28fb4.jpg)

**3.设置通信编码**

**    用mysql\_query这个函数把设置字符集语句**

  


![](img/Language/PHP/databases/960eecc1-954c-49ae-b0b9-7ca657f132ef.png)

![](img/Language/PHP/databases/1f38a9c9-5c63-4b43-bc53-61f7f2b669bd.jpg)

![](img/Language/PHP/databases/1cb140f0-479f-4f43-9a27-8d4c4dd45ae9.png)

**4.准备SQL语句**

**    通过一个变量来存储字符串语句**

**  
**

**    如：$sql="create "**

  


![](img/Language/PHP/databases/fbdcb2f9-fee3-45d7-bb80-2c7c56e37095.jpg)

**5.发送SQL语句到服务器**

  


![](img/Language/PHP/databases/adb7f3cf-2be2-42ed-aeab-21d6414e1247.png)

  返回值：返回值分俩种结果

![](img/Language/PHP/databases/f86ffbb4-99d6-44eb-839e-4cd8aa2a4ed7.png)

  


 insert 等没有结果集，返回true，

select成功返回资源；

![](img/Language/PHP/databases/b5aada3f-6bba-462c-83b9-321566206f8f.png)

6。解析结果集资源

![](img/Language/PHP/databases/141a1554-be9d-4fe7-9a06-5f801ab2ba67.jpg)

![](img/Language/PHP/databases/0b4a907a-a208-4485-aa90-ead9a3b69263.png)

7.二维数组

    二维数组：每个值是数组

  


![](img/Language/PHP/databases/c732016c-866a-4641-8cc5-cba923f77f22.png)

8.关闭数据库链接

![](img/Language/PHP/databases/68dfaea2-27da-496a-b6e5-f646ac455eab.jpg)

![](img/Language/PHP/databases/5d58fed0-5279-487e-9169-2897623f8897.jpg)

