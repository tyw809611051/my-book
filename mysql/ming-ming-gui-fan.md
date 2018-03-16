库，表，字段的命名禁止使用MySQL保留字：

    常见保留字：desc  describe  analyze  explain show  key keys  div dec 
distinct  use using  order  index....

数据库命名

    1.尽量简洁明义，与对应产品线命名保持一致，能够一眼看出来这个数据库是用来做什么的
    2.使用英文字母，全部小写，控制在3-12个字母以内；
    3.如果有多个单词，则使用下划线隔开；
    
数据表命名

    1.表名简洁，使用英文小写单词，对相关功能的表应当使用相同前缀，下划线分隔，如user xxx 其中前缀通常为这个表的模块或依赖主实体对象的名字；
    2.库表默认使用UTF8字符集，默认使用InnoDB引擎；
    3.InnoDB表必须有主键，且必须使用int auto_increment属性。
    4.所有的表都必须有中文备注comment,写明这个表中存放的数据内容；

数据库字段命名

    数据库字段命名与表名命名类似：
    1.字段名简洁，使用小写英文单词，如果有多个单词使用下划线分隔或者驼峰式（注：可根据项目选择其一，保持项目内部统一）；
    2.字段应当有注释comment，描述该字段的用途及可能存储的内容；
    3.对带 _id后缀的字段尽量使用整型；