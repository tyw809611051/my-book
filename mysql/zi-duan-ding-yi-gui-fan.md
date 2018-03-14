原则

    1.字段小而精，保持表的身材苗条，更小的数据类型通常更快，他们占用更少的磁盘空间，IO消耗低，占用内存更少，数据遍历快，alter table 快，表损坏修复快；
    2.单表字段个数尽量控制在32个内；
    3.避免隐式的数据类型转换，过滤字段必须和字段值使用一致的字段类型；int型字段的值禁止加引号，字符型的值需用单引号；

数值型

    tinyint(1byte)、smallint(2B)、mediumint(3B)、int(4B)、bigint(8B)
     注意：int（5）定义zerofill属性才会生效，写入数字9显示为00009；
    整型相比字符串具有更高的性能优势（占用空间更小，查询更快），能使用int型的尽量不要用字符型，类型，状态等字段可用tinyint(1)代替char(1)
    整型的比较代价小于字符比较，因为字符集和排序规则使字符比较更复杂；
    可用int类型存储IP（使用无符号 int unsinged）,也可使用between and来进行范围查询，MySQL内建函数 INET_ATON、INET_NTOA进行数字与IP地址的转换；
    存储金融数据必须使用DECIMAL,浮动float与double数据会偏差

字符型

    在定义字符类型的字段按照实际需要的长度来定义，如果是定长（N）来定义，如果是变长则根据实际可能最大长度设置该字段长度
    尽量不使用text/blob类型，诺业务必须要用到 text/blob，可考虑拆分到单独的表存放；
    varchar的最大长度是64K（65535），UTF字符集一个汉字占3个字节，最大可存储21845个汉字，可以满足大部分需求；
    可用binary或者 varbinary 来存储需区分大小写的字段

NULL

    非必要情形下，在定义字段的时候设置NOT BULL; NULL列需要额外的存储空间，使得索引、索引统计和值比较都更复杂（可定义数字类型默认值为0，字符类型为空字符串）；

时间类型

    date(3B) time(3B);  timestamp(4B)  datetime(8B)
    时间类型尽量用  timestamp 需要注意的是 timestamp 支持时间范围
    ‘1970-1-1 00：00：00’ ~‘2015-09-23 11：21：07’；
    timestamp 可定义当前时间为默认值，并可赋予自动更新属性；
     
    create time timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP;

    update time timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;
    注意：5.6以前一个表只能定义一个timestamp 字段默认值为DEFAULT CURRENT_TIMESTAMP ;目前版本为5.5为主，
    


