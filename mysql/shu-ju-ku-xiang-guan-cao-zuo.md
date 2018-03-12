### 1.查看当前MySQL数据库（当前用户权限）

show databases;

### 2.显示数据创建的指令

show create database 数据库名

![](/img/Language/MySQL/databases_operation/7755eb5b-3644-4883-be15-1ea59eaf60ea.png)

 说明：

    1.当在sql语句中，出现了'' 叫反引号，使得关键字也可作为表名

    2.蓝色框：如果MySQL的版本 &gt;=4.01.00 就执行DEFAULT CHARACTER SET utf8 这个语句 



### 3.删除数据库

    drop database if exists dd1;

  1.if exists :如果存在就执行，反之，就不执行

### 4.查看当前数据库连接进程情况

    show processlist;

    查看有多少用户连接到我们数据库

![](/img/Language/MySQL/databases_operation/4bfc80e9-4067-4494-b7b5-55e067c50d91.png)

 可以得到如下信息

    1.用户名

    2.host字段可以得到用户从哪里登录ip；



  
1.2修改，备份，恢复数据库（重要）

    1.修改数据库

![](/img/Language/MySQL/databases_operation/6b39f6e4-43f5-4ca7-bb41-6a404a00c39a.png)

 红字是关键字，不能修改

![](/img/Language/MySQL/databases_operation/61bf85e8-2379-4d68-97d3-0b834d2f7a9b.png)

![](/img/Language/MySQL/databases_operation/283b8d8a-7ec7-4605-9e12-96f187852ea0.png)

##   1.3  备份和恢复数据库，表

**1. 备份和恢复数据库（单库）**


- 将库备份到文件中

    mysqldump -u root -p 数据库 &gt;指定导出到哪个文件中（路径）

- 恢复步骤：
  - 1，先创建一个空库（名字最好为删掉了那个）
  - 2.选择新建的库
  - 3.导入数据库 source 路径/文件名

**  2.备份和恢复数据库中的指定表**

![](/img/Language/MySQL/databases_operation/989641e5-4190-4b54-89f7-236596ee496f.png)

**    3.备份和恢复多个数据库（多库）**

![](/img/Language/MySQL/databases_operation/5ef4f157-d498-40a7-9a5f-4945b2a31f9c.png)

