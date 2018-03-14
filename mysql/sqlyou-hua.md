

- 尽可能简单应用mysql，复杂运算移动程序端cpu，例如 order by rand()
- 尽量不要频繁的update，例如下载量统计可以定时执行
- 拒绝3B，BIG SQL, BIG Transaction,BIG Batch
- 全文检索设计，sphinx，lucence
- 分页设计，limit start_pos,length+1
- 除非分布式架构，否则尽量不要用UUID
- 区分大小查找：字段设置COLLATE utf8_bin 不要select * from table where binary cloumn
- 不要使用触发器和存储过程
- 不要select *
- NoSQL
- lunce
- 不要使用 like %**% 函数，order by asc desc 组合索引，类型不匹配

2.sql技巧
- slect sql_no_cache；query_cache_size=0,have_query_cache=off 
- explain；explain extented，show warnings

3、分析profiling
- select @@profiling;setprofiling=1; showprofiles;showprofile for query 23;

4、反包含
- select * from table where ? likeconcat('%',column,'%’)
- select * from table where ?regexpcolumn

5、key存在则更新，不存在则插入，insert  into…on duplicate key update

6、excel导入MySQL
load data localinfile'data.txt' into tabletable_nameCHARACTER SETgbkfields terminated by '\t' LINES TERMINATED BY 'n' (cloumn1,cloumn2,……)
