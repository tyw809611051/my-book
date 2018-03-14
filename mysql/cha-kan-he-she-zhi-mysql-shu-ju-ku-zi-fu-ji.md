查看和设置MySQL数据库字符集
　
Liunx下修改MySQL字符集：
1.查找MySQL的cnf文件的位置
find / -iname '*.cnf' -print
/usr/share/mysql/my-innodb-heavy-4G.cnf
/usr/share/mysql/my-large.cnf
/usr/share/mysql/my-small.cnf
/usr/share/mysql/my-medium.cnf
/usr/share/mysql/my-huge.cnf
/usr/share/texmf/web2c/texmf.cnf
/usr/share/texmf/web2c/mktex.cnf
/usr/share/texmf/web2c/fmtutil.cnf
/usr/share/texmf/tex/xmltex/xmltexfmtutil.cnf
/usr/share/texmf/tex/jadetex/jadefmtutil.cnf
/usr/share/doc/MySQL-server-community-5.1.22/my-innodb-heavy-4G.cnf
/usr/share/doc/MySQL-server-community-5.1.22/my-large.cnf
/usr/share/doc/MySQL-server-community-5.1.22/my-small.cnf
/usr/share/doc/MySQL-server-community-5.1.22/my-medium.cnf
/usr/share/doc/MySQL-server-community-5.1.22/my-huge.cnf
　
2. 拷贝 small.cnf、my-medium.cnf、my-huge.cnf、my-innodb-heavy-4G.cnf其中的一个到/etc下，命名为my.cnf
cp /usr/share/mysql/my-medium.cnf /etc/my.cnf
　
3. 修改my.cnf
vi /etc/my.cnf
在[client]下添加
default-character-set=utf8
在[mysqld]下添加
default-character-set=utf8
　
4.重新启动MySQL
[root@bogon ~]# /etc/rc.d/init.d/mysql restart
Shutting down MySQL                                        [ 确定 ]
Starting MySQL.                                            [ 确定 ]
[root@bogon ~]# mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.1.22-rc-community-log MySQL Community Edition (GPL)
Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
　
5.查看字符集设置
mysql> show variables like 'collation_%';
+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| collation_connection | utf8_general_ci |
| collation_database   | utf8_general_ci |
| collation_server     | utf8_general_ci |
+----------------------+-----------------+
3 rows in set (0.02 sec)
mysql> show variables like 'character_set_%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.02 sec)
mysql>
其他的一些设置方法：
修改数据库的字符集
   mysql>use mydb
   mysql>alter database mydb character set utf-8;

创建数据库指定数据库的字符集
   mysql>create database mydb character set utf-8;
通过配置文件修改:
修改/var/lib/mysql/mydb/db.opt
default-character-set=latin1
default-collation=latin1_swedish_ci
为
default-character-set=utf8
default-collation=utf8_general_ci
重起MySQL:
[root@bogon ~]# /etc/rc.d/init.d/mysql restart
　
通过MySQL命令行修改:
mysql> set character_set_client=utf8;
Query OK, 0 rows affected (0.00 sec)
mysql> set character_set_connection=utf8;
Query OK, 0 rows affected (0.00 sec)
mysql> set character_set_database=utf8;
Query OK, 0 rows affected (0.00 sec)
mysql> set character_set_results=utf8;
Query OK, 0 rows affected (0.00 sec)
mysql> set character_set_server=utf8;
Query OK, 0 rows affected (0.00 sec)
mysql> set character_set_system=utf8;
Query OK, 0 rows affected (0.01 sec)
mysql> set collation_connection=utf8;
Query OK, 0 rows affected (0.01 sec)
mysql> set collation_database=utf8;
Query OK, 0 rows affected (0.01 sec)
mysql> set collation_server=utf8;
Query OK, 0 rows affected (0.01 sec)

查看:
mysql> show variables like 'character_set_%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.03 sec)
mysql> show variables like 'collation_%';
+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| collation_connection | utf8_general_ci |
| collation_database   | utf8_general_ci |
| collation_server     | utf8_general_ci |
+----------------------+-----------------+
3 rows in set (0.04 sec)
　
MYSQL 字符集问题
　
MySQL的字符集支持(Character Set Support)有两个方面：
     字符集(Character set)和排序方式(Collation)。
对于字符集的支持细化到四个层次:
     服务器(server)，数据库(database)，数据表(table)和连接(connection)。
1.MySQL默认字符集
MySQL对于字符集的指定可以细化到一个数据库，一张表，一列，应该用什么字符集。
但是，传统的程序在创建数据库和数据表时并没有使用那么复杂的配置，它们用的是默认的配置，那么，默认的配置从何而来呢？    (1)编译MySQL 时，指定了一个默认的字符集，这个字符集是 latin1；
    (2)安装MySQL 时，可以在配置文件 (my.ini) 中指定一个默认的的字符集，如果没指定，这个值继承自编译时指定的；
    (3)启动mysqld 时，可以在命令行参数中指定一个默认的的字符集，如果没指定，这个值继承自配置文件中的配置,此时 character_set_server 被设定为这个默认的字符集；
    (4)当创建一个新的数据库时，除非明确指定，这个数据库的字符集被缺省设定为character_set_server；
    (5)当选定了一个数据库时，character_set_database 被设定为这个数据库默认的字符集；
    (6)在这个数据库里创建一张表时，表默认的字符集被设定为 character_set_database，也就是这个数据库默认的字符集；
    (7)当在表内设置一栏时，除非明确指定，否则此栏缺省的字符集就是表默认的字符集；
简单的总结一下，如果什么地方都不修改，那么所有的数据库的所有表的所有栏位的都用 latin1 存储，不过我们如果安装 MySQL，一般都会选择多语言支持，也就是说，安装程序会自动在配置文件中把 default_character_set 设置为 UTF-8，这保证了缺省情况下，所有的数据库的所有表的所有栏位的都用 UTF-8 存储。
2.查看默认字符集(默认情况下，mysql的字符集是latin1(ISO_8859_1)
通常，查看系统的字符集和排序方式的设定可以通过下面的两条命令：
     mysql> SHOW VARIABLES LIKE 'character%';
+--------------------------+---------------------------------+
| Variable_name            | Value                           |
+--------------------------+---------------------------------+
| character_set_client     | latin1                          |
| character_set_connection | latin1                          |
| character_set_database   | latin1                          |
| character_set_filesystem | binary                    |
| character_set_results    | latin1                          |
| character_set_server     | latin1                          |
| character_set_system    | utf8                            |
| character_sets_dir       | D:"mysql-5.0.37"share"charsets" |
+--------------------------+---------------------------------+
mysql> SHOW VARIABLES LIKE 'collation_%';
+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| collation_connection | utf8_general_ci |
| collation_database   | utf8_general_ci |
| collation_server     | utf8_general_ci |
+----------------------+-----------------+
3.修改默认字符集
(1) 最简单的修改方法，就是修改mysql的my.ini文件中的字符集键值，
如    default-character-set = utf8
      character_set_server = utf8
   修改完后，重启mysql的服务，service mysql restart
   使用 mysql> SHOW VARIABLES LIKE 'character%';查看，发现数据库编码均已改成utf8
+--------------------------+---------------------------------+
| Variable_name            | Value                           |
+--------------------------+---------------------------------+
| character_set_client     | utf8                            |
| character_set_connection | utf8                            |
| character_set_database   | utf8                            |
| character_set_filesystem | binary                          |
| character_set_results    | utf8                            |
| character_set_server     | utf8                            |
| character_set_system     | utf8                            |
| character_sets_dir       | D:"mysql-5.0.37"share"charsets" |
+--------------------------+---------------------------------+
   (2) 还有一种修改字符集的方法，就是使用mysql的命令
   mysql> SET character_set_client = utf8 ;
     mysql> SET character_set_connection = utf8 ;
     mysql> SET character_set_database = utf8 ;
     mysql> SET character_set_results = utf8 ;
     mysql> SET character_set_server = utf8 ;
     mysql> SET collation_connection = utf8 ;
     mysql> SET collation_database = utf8 ;
     mysql> SET collation_server = utf8 ;
一般就算设置了表的默认字符集为utf8并且通过UTF-8编码发送查询，你会发现存入数据库的仍然是乱码。问题就出在这个connection连接层上。解决方法是在发送查询前执行一下下面这句：
SET NAMES 'utf8';它相当于下面的三句指令：
SET character_set_client = utf8;
SET character_set_results = utf8;
SET character_set_connection = utf8;
总结:
因此，使用什么数据库版本，不管是3.x，还是4.0.x还是4.1.x，其实对我们来说不重要，重要的有二：
1) 正确的设定数据库编码.MySQL4.0以下版本的字符集总是默认ISO8859-1，MySQL4.1在安装的时候会让你选择。如果你准备使用UTF- 8，那么在创建数据库的时候就要指定好UTF-8(创建好以后也可以改，4.1以上版本还可以单独指定表的字符集)
2) 正确的设定数据库connection编码.设置好数据库的编码后，在连接数据库时候，应该指定connection的编码，比如使用jdbc连接时，指定连接为utf8方式.
