Mysql监控-自带工具Query Profiler的使用
Query Profiler是MYSQL自带的一种query诊断分析工具，通过它可以分析出一条SQL语句的性能瓶颈在什么地方。通常我们是使用的explain,以及slow query log都无法做到精确分析，但是Query Profiler却可以定位出一条SQL语句执行的各种资源消耗情况，比如CPU，IO等，以及该SQL执行所耗费的时间等。不过该工具只有在MYSQL 5.0.37以及以上版本中才有实现。
默认的情况下，MYSQL的该功能没有打开，需要自己手动启动。可以通过如下方法查看当前mysql服务器是否开启了该功能。
复制代码
mysql> show variables like '%profiling%';
+------------------------+-------+| Variable_name          | Value |+------------------------+-------+| 
profiling              | OFF   ||
 profiling_history_size | 15    |
+------------------------+-------+2 rows in set (0.03 sec)

mysql> SHOW VARIABLES LIKE '%profiling%';
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| have_profiling         | YES   |
| profiling                   | OFF   |
| profiling_history_size | 15    |
+------------------------+-------+
3 rows in set (0.00 sec)

profiling参数值为OFF，说明没有打开该功能。
profiling_history_size参数值为15表示，记录最近15次的查询历史。该值可以修改。
下边说说如何打开profiling功能：
MYSQL提示符下执行如下命令：
mysql> set profiling=1;
Query OK, 0 rows affected (0.00 sec)

mysql> set profiling=1;
Query OK, 0 rows affected (0.00 sec)

然后再次检验下执行的效果：
复制代码
mysql> show variables like '%profiling%';
+------------------------+-------+| Variable_name          | Value |+------------------------+-------+| profiling              | ON    || profiling_history_size | 15    |+------------------------+-------+2 rows in set (0.00 sec)
mysql> show variables like '%profiling%';
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| have_profiling         | YES   |
| profiling              | ON    |
| profiling_history_size | 15    |
+------------------------+-------+
3 rows in set (0.00 sec)

profiling值为ON说明已经启动该功能。
下边说说如何使用show profiles;
1.首先执行一查询语句：
复制代码
mysql> select * from user;
+------+-----------+| id   | name      |+------+-----------+|   1 | a          ||   2 | b          ||   3 | c          ||   4 | d          ||   5 | e          ||   6 | f          ||   7 | g          |+------+-----------+7 rows in set (0.06 sec)
复制代码

mysql> SELECT goods_name FROM ecs_goods;
+-------------------------------------+
| goods_name                          |

2.通过show profiles命令查看系统中多个query的概要信息：
复制代码
mysql> show profiles;
+----------+------------+-----------------------------------+| Query_ID | Duration   | Query                             |+----------+------------+-----------------------------------+|        1 | 0.00013600 | set profiling=1                   ||        2 | 0.00092300 | show variables like '%profiling%' ||        3 | 0.08506075 | show databases                    ||        4 | 0.02698550 | SELECT DATABASE()                 ||        5 | 0.07408475 | show tables                       ||        6 | 0.05769725 | select * from user                |+----------+------------+-----------------------------------+6 rows in set (0.01 sec

mysql> show profiles;
+----------+-------------+-----------------------------------+
| Query_ID | Duration    | Query                             |
+----------+-------------+-----------------------------------+
|        1 |  0.00115050 | show variables like '%profiling%' |
|        2 |  0.12960900 | show databases                    |
|        3 |  0.00031275 | SELECT DATABASE()                 |
|        4 |  0.00480375 | desc tmpdb                        |
|        5 |  0.00088950 | show tables                       |
|        6 |  0.00060800 | select * from user                |
|        7 | 12.96188400 | select * from emp                 |
|        8 |  0.00145225 | show databases                    |
|        9 |  0.00031650 | SELECT DATABASE()                 |
|       10 |  0.00244650 | show tables                       |
|       11 |  0.07492475 | SELECT goods_name FROM ecs_goods  |
+----------+-------------+-----------------------------------+
11 rows in set (0.00 sec)
其中Query_ID表示查询ID，也就是个编号，Duration表示对应的query语句执行的时间，单位是秒，query表示具体的query语句。我们可以看到刚才我们最后执行的SELECT goods_name FROM ecs_goods语句执行的时间是0.07492475，单位是秒，也就是74ms
3.获取单个query的详细profile信息，可以通过如下语句：
复制代码
mysql> show profile cpu,block io for query 1;
+--------------------+----------+----------+------------+--------------+---------------+| Status             | Duration | CPU_user | CPU_system | Block_ops_in | Block_ops_out |+--------------------+----------+----------+------------+--------------+---------------+| starting           | 0.014438 |     NULL |       NULL |         NULL |          NULL || Opening tables     | 0.042860 |     NULL |       NULL |         NULL |          NULL || System lock        | 0.000007 |     NULL |       NULL |         NULL |          NULL || Table lock         | 0.000012 |     NULL |       NULL |         NULL |          NULL || init               | 0.000019 |     NULL |       NULL |         NULL |          NULL || optimizing         | 0.000005 |     NULL |       NULL |         NULL |          NULL || statistics         | 0.000018 |     NULL |       NULL |         NULL |          NULL || preparing          | 0.000011 |     NULL |       NULL |         NULL |          NULL || executing          | 0.000004 |     NULL |       NULL |         NULL |          NULL || Sending data       | 0.000232 |     NULL |       NULL |         NULL |          NULL || end                | 0.000007 |     NULL |       NULL |         NULL |          NULL || query end          | 0.000005 |     NULL |       NULL |         NULL |          NULL || freeing items      | 0.000073 |     NULL |       NULL |         NULL |          NULL || logging slow query | 0.000003 |     NULL |       NULL |         NULL |          NULL || cleaning up        | 0.000004 |     NULL |       NULL |         NULL |          NULL |+--------------------+----------+----------+------------+--------------+---------------+15 rows in set (0.02 sec)
复制代码
mysql> show profile cpu,block io for query 1;
+--------------------+----------+----------+------------+--------------+---------------
| Status             | Duration | CPU_user | CPU_system | Block_ops_in | Block_ops_out
+--------------------+----------+----------+------------+--------------+---------------
| starting           | 0.000079 | 0.000000 |   0.000000 |         NULL |          NULL
| Opening tables     | 0.000308 | 0.000000 |   0.000000 |         NULL |          NULL
| System lock        | 0.000017 | 0.000000 |   0.000000 |         NULL |          NULL
| init               | 0.000017 | 0.000000 |   0.000000 |         NULL |          NULL
| optimizing         | 0.000007 | 0.000000 |   0.000000 |         NULL |          NULL
| statistics         | 0.000017 | 0.000000 |   0.000000 |         NULL |          NULL
| preparing          | 0.000013 | 0.000000 |   0.000000 |         NULL |          NULL
| executing          | 0.000531 | 0.000000 |   0.000000 |         NULL |          NULL
| Sending data       | 0.000038 | 0.000000 |   0.000000 |         NULL |          NULL
| end                | 0.000006 | 0.000000 |   0.000000 |         NULL |          NULL
| query end          | 0.000004 | 0.000000 |   0.000000 |         NULL |          NULL
| closing tables     | 0.000003 | 0.000000 |   0.000000 |         NULL |          NULL
| removing tmp table | 0.000016 | 0.000000 |   0.000000 |         NULL |          NULL
| closing tables     | 0.000004 | 0.000000 |   0.000000 |         NULL |          NULL
| freeing items      | 0.000082 | 0.000000 |   0.000000 |         NULL |          NULL
| logging slow query | 0.000005 | 0.000000 |   0.000000 |         NULL |          NULL
| cleaning up        | 0.000004 | 0.000000 |   0.000000 |         NULL |          NULL
+--------------------+----------+----------+------------+--------------+---------------
17 rows in set (0.00 sec)

总结：Query Profiler对于SQL性能分析和诊断费用有用。另外，该命令还有如下参数可以选择：
ALL - displays all information
BLOCK IO - displays counts for block input and output operations
CONTEXT SWITCHES - displays counts for voluntary and involuntary context switches
IPC - displays counts for messages sent and received
MEMORY - is not currently implemented
PAGE FAULTS - displays counts for major and minor page faults
SOURCE - displays the names of functions from the source code, together with the name and line number of the file in which the function occurs
SWAPS - displays swap counts
使用SQLyog等工具可以直接看到Profiler页面，输入 Show profiles;语句后会显示更为详细的信息。