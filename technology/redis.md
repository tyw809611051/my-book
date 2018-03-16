                                                                                                     
### 1概述

redis,很流行的内存缓存技术.相对于memcached,有2个应用层面的不同:

A,支持多种数据类型.\(重点,选择redis的原因\)可以实现更多的业务逻辑.典型的例如,队列\(队列\),排行榜类程序,很容易使用redis实现.

B,支持持久化缓存数据.在服务器重启时,之前的数据还是会存在.持久化存储不是缓存的特征.



功能上, redis可以全面替代memcached.



# 2安装

## 2.1windows

![](/img/Technology/nosql/redis/1.png)

**解压需要的**版本,放置在指定位置即可, \(绿色版\)

![](/img/Technology/nosql/redis/2.png)



也是在service/redis

![](/img/Technology/nosql/redis/3.png)

## 2.2linux

获取源码

![](/img/Technology/nosql/redis/4.png)

上传到centos, tar zxvf解压,进入目录

![](/img/Technology/nosql/redis/5.png)



提供的源码,直接编译就可以生成执行文件.不需要执行到配置安装的过程

直接make即可

![](/img/Technology/nosql/redis/6.png)

make完毕后,生成了可以直接运行的二进制程序

需要将其放置在合理的位置即可.

![](/img/Technology/nosql/redis/7.png)





规划redis的安装目录

创建需要的目录即可,参考windows的目录结构,可以规划成其他结构,比如创建bin存储执行程序.

![](/img/Technology/nosql/redis/8.png)



将执行文件\(程序\)拷贝到特定目录

![](/img/Technology/nosql/redis/9.png)



将配置文件也拷贝过

在源码根目录

![](/img/Technology/nosql/redis/10.png)



![](/img/Technology/nosql/redis/11.png)



## 2.3常规管理

### 2.3.1windows,将redis目录,加入环境变量

![](/img/Technology/nosql/redis/12.png)



### 2.3.2linux,设置环境PATH

![](/img/Technology/nosql/redis/13.png)





### 2.3.3开机启动, rc.local

![](/img/Technology/nosql/redis/14.png)





# 3C/S操作

## 3.1服务器端

redis-server

通常开启时需要指定配置文件

redis-server配置文件

![](/img/Technology/nosql/redis/15.png)



可以增加&,后端执行

![](/img/Technology/nosql/redis/16.png)



### 3.1.1开启

直接运行redis-server

![](/img/Technology/nosql/redis/17.png)

### 3.1.2关闭

kill掉.可以用/var/run/redis-6379.pid获取PID值

![](/img/Technology/nosql/redis/18.png)

## 3.2必要的配置

### 3.2.1使用守护进程的方式后台执行

![](/img/Technology/nosql/redis/19.png)

启动时,不需要增加&,就会自动在后端运行.启动

![](/img/Technology/nosql/redis/20.png)



### 3.2.2进程PID的文件

![](/img/Technology/nosql/redis/21.png)

redis-server会将redis的运行的PID,存储到该文件中,便于获取该PID,对进程进行管理.例如结束:

通过反引号包裹需要执行的命令,将其作为需要被kill的PID使用.

![](/img/Technology/nosql/redis/22.png)





### 3.2.3port,监听的端口

6379是redis的默认端口

![](/img/Technology/nosql/redis/23.png)



### 3.2.4bind,监听的IP端口绑定

![](/img/Technology/nosql/redis/24.png)

一块电脑多个网卡,我们的redis,监听从那块网卡进入的操作请求链接.

为了让宿主电脑也可以访问到,同时监听eth0. \(服务器所在的IP地址\)

![](/img/Technology/nosql/redis/25.png)



### 3.2.5logfile,日志文件地址

如果非守护进程方式执行\(前端执行\),日志会打印到终端上.shell上.



如果是守护方式\(deamonize yes\)端执行,生成的日志,都被舍弃了.

强烈建议,保留日志,通过配置日志文件完成

![](/img/Technology/nosql/redis/26.png)

![](/img/Technology/nosql/redis/27.png)



## 3.3PHP程序客户端

安装reids扩展,成为redis客户端.

安装方式与安装memcached扩展一致

### 3.3.1windows

![](/img/Technology/nosql/redis/28.png)

解压,放在php/ext

![](/img/Technology/nosql/redis/29.png)



php.ini开启

![](/img/Technology/nosql/redis/30.png)



重启apache

测试

![](/img/Technology/nosql/redis/31.png)



### 3.3.2linux

phpize\(php扩展化\)

![](/img/Technology/nosql/redis/32.png)

解压,进入源码, phpize,配置,编译,安装

tar zxvf redis-2.2.7.tgz

cd redis-2.2.7

phpize

./configure

./configure --with-php-config=/usr/local/php/bin/php-config

make && make install



修改php.ini

![](/img/Technology/nosql/redis/33.png)

重启apache

测试

![](/img/Technology/nosql/redis/34.png)





## 3.4命令行管理客户端

键入redis-cli进入到命令行的客户端,测试,管理时常用.

![](/img/Technology/nosql/redis/35.png)





# 4操作

大量的操作指令.针对与不同的类型,具备不同的操作.较多.



## 4.1连接redis服务器

![](/img/Technology/nosql/redis/36.png)



请看各种类型的操作



# 5字符串类型与缓存项操作,重点,数据缓存

字符串类型,是最常用的类型.如果redis仅仅有字符串,与memcached是一致的.

作为数据缓存的通用类型.



## 5.1字符串:set,设置

![](/img/Technology/nosql/redis/37.png)



redis支持数据类型,不是PHP的类型．

选择，　存储一个数组进入：

![](/img/Technology/nosql/redis/38.png)

此时，　存储在redis中的仅仅是：Array　字符串

![](/img/Technology/nosql/redis/39.png)

原因是，将数组强行转换成字符,结果就是Array.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image077.jpg)



实操是,往往将PHP的数据,序列化后,再存储到redis中.获取时反序列化.

因为去分不开,是否被序列化了,就全部处理.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image079.jpg)

## 5.2字符串:get,获取

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image081.jpg)



## 5.3字符串:递增,递减, incr, decr, incrby, decrby

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image083.jpg)



## 5.4字符串: setNx,设置,不存在时设置

设置前,需要检测该key是否存在,不存在,才可以设置上.

类似于memacache的add.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image085.jpg)



实操应用:

通常,处理资源争用时,实现锁定,比较常用的方法.

当一个脚本使用某个资源时,先尝试, setNx\(memcache的add\)一个key,如果可以设置上,说明当前没有其他脚本\(进程\)在使用该资源.此脚本可以使用.反之设置失败,当前资源被使用\(占用\),该脚本就不能使用.

如果一个脚本已经使用完毕资源,执行delete操作,将锁定key删除.



## 5.5字符串:追加append

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image087.jpg)

## 5.6字符串:长度strlen

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image089.jpg)

## 5.7缓存项:del, delete,删除

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image091.jpg)



## 5.8缓存项:有效期expire, expireAt, ttl

时间段有效期: expire

时间点有效期: expireAt



独立设置缓存项的有效期..而不是在设置时.



![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image093.jpg)



不指定的有效期,表示永不失效.手动删除



有效期的指定, redis支持精确到毫秒.



同时支持获取当前缓存项的有效期, ttl, time to live.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image095.jpg)



# 6list\(链表\)结构\(类型\)的操作

一段连续的存储空间,称之为一个链表list. \(类似PHP的索引数组,下标由0开始,逐1递增,连续存储\)

一个key,对应多个值.\(复合结构\)



## 6.1压入元素: lpush, rpush

将元素压入list. \(PHP: array\_push\(\), array\_unshift\(\)数组操作函数\)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image097.jpg)



## 6.2弹出元素: lpop\(\), rpop\(\)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image099.jpg)



## 6.3索引下标操作: lset, lget

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image101.jpg)



强调,下标索引操作,仅仅可以操作已经存在的元素.不能执行添加.但支持一个插入linsert的工作,参考linsert.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image103.jpg)



## 6.4指定位置插入元素: linsert

通过位置: after和before表示

常量: Redis::AFTER, Redis::BEFORE表示

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image105.jpg)



注意,如果当前参考元素值相同的多个元素,则在第一个元素前执行插入工作

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image107.jpg)



## 6.5获取部分元素:lrange

range范围.

通过起止的索引值,表示范围. \(总结,表示子范围, 2中方案, a,起,止; b,起,范围\)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image109.jpg)

索引位置,可以由负数表示,表示倒数第几个的含义:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image111.jpg)



典型的,全部都获取: 0, -1

$list = $redis-&gt;lrange\('userList', 0, -1\);



## 6.6获取长度: llen, lsize

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image113.jpg)



## 6.7移除元素: lremove

值匹配删除:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image115.jpg)



如果出现重复的值,如何处理?默认删除全部匹配元素

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image117.jpg)



删除时,可以去指定,删除固定数量的匹配元素,通过第三个参数数量count来设置:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image119.jpg)



## 6.8队列queue操作,重点

队列queue,一种特殊的list\(链表\),限定了操作,只能在一端压入元素,而另一端弹出元素.

队列,先进先出, FIFO,一种数据结构.\(lru队列\).非常常用一种数据结构.通常用于解决并发问题. \(集中发送邮件,生成订单,进入处理队列\)

并发,并行发生.将并行发生的请求\(操作\),给排队.加入队列.逐一处理.



lpush + rpop构成队列.

rpush + lpop构成队列.





## 6.9栈stack

栈,先进后出. FILO.

限制压入和弹出操作仅仅在一端执行list结构.

lpush+lpop

rpush+rpop





# 7集合, set

也是一种复合结构.一个key可以存储多个值.

\(相对于list\).

具备如下的特征:

1,无序性.\(没有下标的操作\)

2,唯一性.元素值不能重复.

\(集合的以上的特征,不是redis定的.数据结构的层面,说到集合,就是上的特征.只是说redis实现了集合的操作\)



## 7.1sadd,添加成员到集合中

加入几个元素:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image121.jpg)



测试加入重复元素:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image123.jpg)



## 7.2sMembers,获取集合中的全部成员

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image125.jpg)



## 7.3弹出成员: spop

随机弹出某个成员.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image127.jpg)



## 7.4集合基\(基准\)数,成员个数:scard

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image129.jpg)



![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image131.jpg)



## 7.5删除集合成员: sremove

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image133.jpg)



## 7.6集合间运算:交集

2个集合重复的成员集合.

## 7.7集合间运算:并集

2个集合全部的成员,除重复!

## 7.8集合间运算:差集

A差B, A中去掉A与B重复的成员.

B差A, B中去掉B与A重复的成员

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image135.jpg)



# 8有序集合,加权\(分\)集合, sorted-set.重要

在集合的基础上,为每个成员,增加一个score分值的属性.

分值可以被设置.允许依据分值排序.

很适合完成:排行榜类逻辑,计数器.



## 8.1添加成员到有序集: zadd

第二个为score,第三个为成员.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image137.jpg)

分值,也可以是小数.

## 8.2指定范围成员: zrange, zRevRange

zrange升序排序后,获取指定排序的成员,使用起止位置.

此顺序是逻辑分值顺序,而不是物理插入顺序.

第四个参数,表示是否携带分值获取.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image139.jpg)



相对的zrevrange,是降序排序

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image141.jpg)



## 8.3分值增减: zIncrBy

increment

指定增量即可,可以为小数,整数,负数

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image143.jpg)



## 8.4获取成员分值: zscore

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image145.jpg)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image147.jpg)



## 8.5zRangeByScore, ZRevRangeByScore

过滤分数在某个范围的成员,

需要指定分值范围,闭区间\(包含临界值\)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image149.jpg)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image151.jpg)



同样携带分数返回:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image153.jpg)



限定结果选项\(分页\)

增加选项limit,提供, offset和limit: \(where socre between 0, 20 order by score asc limit 0, 2\)

获取匹配的前2个成员:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image155.jpg)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image157.jpg)





类似的limit,使用zrange也可以实现.但是需要注意的是: zrange使用的是:起始和结束的位置.需要计算出来.例如,每页2个.

zrange\(‘set’, 0, 1\);

zrange\(‘set’, 2, 3\);





## 8.6应用

记录商品的购买量

初始化一个大的\(成员的数量由商品数量决定\)有序集.

每当商品被销售将对应的成员分递增.



利用该结构:

1,买的最好的100件

2,买的最差的200件

3,卖了5w-7w的商品



非常建议使用缓存去做.购买量数据,不需要即时持久化.而且可以利用定时任务,定时将缓存的中购买量,同步到数据库中.

而且,以上数据redis自动会持久化存储.购买数量不会丢失.





# 9哈希表: hash-table

结构上就是关联数组.一个key对应一个value.键值对链表就是哈希表.

\(额外的:哈希是一类算法的称呼.一个字符串去映射称另一个值\(字符串\)的过程,称之为哈希的过程.如果输入字符串不变,输出字符串也不变.例如, md5, crc32,求余\)

\(list是索引数组\)



特征:键就是某个特定的字符串标志.支持键操作.

## 9.1设置元素: hset

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image159.jpg)



## 9.2获取全部元素:hgetAll\(\)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image159.jpg)

## 9.3获取一个元素:hget

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image161.jpg)

## 9.4删除元素: hdel

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image163.jpg)

## 9.5判断元素是否存在: hExists

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image165.jpg)

## 9.6长度:hLen





# 10基准数: HyperLog

集合的card操作.



仅仅实现了集合的add和card操作的数据类型.

该类型的目的,就是记录集合的元素个数.如果不关心成员,而去关心数量时,使用该类型.

例如:网站的独立访客,独立IP的统计时,就可以使用.描述网站的业务量.

独立访客:独立的会话session-id标志

独立IP:统计独立的请求IP数量.



提供: pfadd添加元素, pfCount获取基准数

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image167.jpg)





# 11bitmap,位图字符串

一种特殊字符串操作.

01010101101010101

11101101010101010

所有的字符由0,1构成.称之为:位图



支持的操作,设置某个位置为0,1,获取某个位置的值.

getbit, setbit

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image169.jpg)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image171.jpg)



# 12持久性存储\(数据库特征\)

由于redis也是具备数据库的某些特征,有时,也可以是一个数据库服务器.



## 12.1配置项dbfilename

数据库文件,当redis做持久性存储时,使用的文件. rdb: redis database

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image173.jpg)



## 12.2配置dir

工作目录.默认是./取决于在何处运行reids-server,工作目录就是运行redis-server的目录.建议设置在redis目录.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image175.jpg)



重启redis服务,生效

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image177.jpg)





## 12.3持久化存储测试

增加缓存项后,关闭启动redis-server服务器.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image179.jpg)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image181.jpg)

通过客户端,直接获取缓存项,发现:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image183.jpg)

可以获取到!

可见,默认情况, redis就支持持久性存储.



redis就将缓存项,存储到了:

dir/dbfilename配置所示

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image185.jpg)



提示:该文件,会在服务器关闭时,自动形成.



## 12.4配置项save,持久化时间策略

dump.rdb文件,在核实形成的. redis的是采用何种策略进行持久化存储的.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image187.jpg)

900s内,如果有1个以上的修改,则存储.

300s内,如果有10个以上的修改,则存储

60s内,如果有10000个以上的修改,则存储.

原则:修改频率越高,存储频率就越高.

1,不是修改立即存储,提升效率.

2,当修改量累计到一定时,进行一次存储.



含义是:在多少秒之内,发生了多少个修改,则执行存储工作.

save &lt;seconds&gt;&lt;changes&gt;



如果配置为了save “”,表示放弃自动存储机制.仅仅是一个缓存服务器.



除了这个时间策略之外, redis服务器关闭时,也会执行一次存储.



## 12.5命令save,立即存储

当执行save时,将内存中的缓存项,立即持久化到dump.rdb中

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image189.jpg)



## 12.6存储的方式策略

dump.rdb的文件,称之为快照存储.

一旦执行save工作,无论手动还是自动.

将缓存中的所有缓存项都持久化到dump.rdb中.

优势,任何时候,只要拥有dump.rdb就可以得到全部的缓存项.

因此,通常采用备份dump.rdb的方式,备份redis数据.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image191.jpg)

还原时,将备份文件,放在dir/dbfilename指定的位置,重启redis即可欢原数据.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image193.jpg)





快照存储有劣势:

当基础缓存项的数量很大,但是修改更新的缓存项数量较少时.

出现大量的重复无用操作.要去重新存储,大量的没有修改的缓存项.

redis使用aof,来解决.



## 12.7AOF存储机制

append only file

仅仅处理增加的缓存项.

将这些修改,存储到硬盘上.

在原始数据的基础上,进行修改即可完成数据还原.



默认是没有开启的.通过配置项: appendonly可以开启

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image195.jpg)

重启测试

操作设置redis

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image197.jpg)

查看生成的文件:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image199.jpg)



该文件是修改命令记录文件:

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image201.jpg)



# 13事务\(批处理\)

目前的实现是批处理.



事务: transaction,一组操作的集合,具有原子性,要不全部成功,影响数据库.要不所有的操作都不产生影响.将已经产生影响的结果撤销.



在redis,也可以将操作集合到一个命令组中.

命令如下: multi, exec, discard

multi开启批处理\(事务\)

exec执行

discard放弃

演示如下

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image203.jpg)







![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image205.jpg)



# 14认证

需要提供密码才可以访问.



## 14.1服务器配置一个密码

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image207.jpg)

重启生效

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image209.jpg)





## 14.2客户端提供密码

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image211.jpg)



命令auth

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image213.jpg)

直接操作即可

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image215.jpg)

PHP程序中,使用

$redis-&gt;auth\('foobared'\);

完成



# 15应用

## 15.1数据缓存\(redis的字符串类型\)

与memcache可以相互替换.

在S\(\)函数初始化缓存配置时,使用redis类型即可

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image217.jpg)

实操时, PHP代码不需要修改.通常将缓存服务器的配置,定义在配置系统中.



## 15.2计数器-排行榜类型程序

商品的访问\(收藏,购买, \)排行或者计数.



### 15.2.1一,初始化每个商品的访问次数

每当后台添加商品,立即在缓存中,增加该商品的访问计数器.

后台的控制器,完成添加商品功能,之后,完成计数器初始化

Back/Goods/add

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image219.jpg)



ceshi

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image221.jpg)



### 15.2.2二,计数器累加

没当前台的商品信息页执行,则对应的商品被访问,计数器+1

\(实操时还需要计算,通过IP+浏览器+session信息+4h,重复累加\)



Home/Goods/view

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image223.jpg)



### 15.2.3三,\(应用\)排行版

获取最热的3个商品

看的多就热.

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image225.jpg)

### 15.2.4三, \(应用\)计数过滤

获取访问量在100-200间的商品

方法: zRevRangeByScore\(\)



### 15.2.5四,同步到数据库

周期性的同步.

在商品表上,增加一个字段,记录访问次数.

| goods\_id | name | price | …. | view |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 23 |  |  |  | 21 |  |
| 77 |  |  |  | 15 |  |



\(增加一个额外的商品访问次数表,独立访问次数

| goods\_id | view |
| :--- | :--- |
| 23 | 21 |
| 77 | 15 |
| 71 | 5 |

\)



配合计划任务执行.

写个PHP脚本,更新访问次数的脚本

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image227.jpg)



使用计划任务完成

\(上传脚本到linux\)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image229.jpg)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image231.jpg)



编写计划任务

每天同步一次即可\(每4个小时\)

![](file:///C:\Users\ADMINI~1\AppData\Local\Temp\msohtmlclip1\01\clip_image233.jpg)



## 15.3队列应用

后边说!


