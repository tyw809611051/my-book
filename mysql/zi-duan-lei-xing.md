  


主要三大类：整数类型，浮点型，字符串型

![](/img/Language/MySQL/field_type/bc98c8ba-9785-4a06-b6e9-628aba850ee7.jpg)

**数值型-整数型**

**    Tinyint：有符号（有负号）**

**    Smallint**

**    int**

![](/img/Language/MySQL/field_type/edc3a265-2765-4219-abeb-10a6a1ff3b82.jpg)

** 数值型-小数型**

**    float:浮动型，普通的小数**

**    Decimal:定点型，语法：deicmal\(10,2\)有10位数，其中最后2位为小数  一般用于价格**



**字符串型**

    char\(\):字符串限制多少的字符的写法 定长：如果定好多少，不够，用空格填满（手机号）

    varchar:同上，变长：实际有多少，就占多少（文章标题）

    Text:超长型，大篇的文章



日期时间型：

date类型：支持的范围为'1000-01-01'到'9999-12-31'

time类型：支持的范围是'-838:59:59'到'838:59:59'

datetime类型：支持的范围是'1000-01-01 00:00:00'到'9999-12-31 23:59:59'

建议：如果日期时间都有的形式，用字符串型，原因：以后获取时间都是格林威治时间

