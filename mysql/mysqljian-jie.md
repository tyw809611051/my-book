数据库是存放数据的仓库，数据不是直接放到数据库中，数据库中放的是表，表中存放的是数据
常见的DBMS（DataBase Management System）:
- Access:小型的数据库，微软的免费
- SQL server：大型的数据库，微软的收费
- MySQL:中小型数据库，
- Oracle:大型数据库；
- DB2：IBM公司

#### MySQL打开方式
数据库管理系统可以通过：
- 语言打开并访问数据库，
- 可以通过可视化访问数据库：浏览器访问
- 命令行模式访问数据库：ms-dos
```
    基本语法：mysql -h 主机名（ip） -u 用户名 -P 端口 -p 密码
        -h 后面可以写上连接的主机名或是ip，默认时候，localhost 本机
        -u 用户名，比如root，
        -P P是大写，连接MySQL的端口，默认3306 
        -p 密码
```

#### 管理数据库流程
- 1.选择要打开方式
- 2.选择数据库：用户名和密码链接数据库，默认为root
- 3.向服务器发送SQL语句：命令（CRUD:增，删，改，查）
- 4.服务器接手命令执行后把结果返回给打开方式
- 5.打开方式接手到结果，进行编译：可以看明白的方式
- 6.关闭数据库


发展史：
- 1.层次模型
- 2.网状模型
- 3.关系模型

**SQL分为三个部分**

- DDL: Data Definition Language, 数据定义语言, 用来维护存储数据的结构(数据库,表), 代表指令: create, drop, alter等

- DML: Data Manipulation Language, 数据操作语言, 用来对数据进行操作(数据表中的内容), 代表指令: insert, delete,update等: 其中DML内部又单独进行了一个分类:

- DQL(Data Query Language: 数据查询语言, 如select)
DCL: Data Control Language, 数据控制语言, 主要是负责权限管理(用户), 代表指令: grant,revoke等
