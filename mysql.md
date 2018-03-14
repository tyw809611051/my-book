- 索引不是越多越好，每个表只能用到一个mysql认为最优的索引；能不加的尽量不加（如不要对“性别”’建立单独索引）；

- 一般索引使用idx 前缀（如：idx_col）,唯一索引使用uniq_ 前缀（如：uniq_col）;

- 经常用作过滤条件的字段上应有索引；update 语句 where 字段应有索引，尽量使用主键作为update 条件

- varchar 列上建索引，尽量使用索引前缀，如：index idx_name(name(16));

- 复合索引：存在idx_a_b_c(a,b,c)索引的情况下，不需要再对a列建立idx_a(a) 和index_a_b(a,b)建立；经常使用的条件列放复合索引最前面；

- GROUP BY b, ORDER BY b 字段一般与WHERE a 字段建复合索引 idx_a_b(a,b)

- MySQL 禁止使用外键，尽量由程序来保证约束；外键会带来额外开销，高并发场景下会引起死锁；