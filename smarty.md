smarty缓存技术

开启缓存步骤：

```
1.开启缓存：$smarty -&gt;caching = true;

2.设置缓存的目录：   $smarty -&gt;setCacheDir（‘cache’）;

3.设置有效期：    $smarty -&gt;cache\_lifetime = 10
```

有些地方需要实时更新，采用局部不缓存（需保证4个规范）：

```
1.函数文件保存的位置，smarty/plugins

2.函数文件的命名规范：insert.函数名.php

3.在文件中定义函数时，函数的命名规范：smarty\_insert\_函数名




4.函数的参数，必须在
```

&lt;

{insert}

&gt;

标签中传递

![](index_files/39952355.png)

![](index_files/39986581.png)

单模板多缓存技术（一个html模板产生多个缓存文件）：

```
实现：需啊在display的时候，增加第二个参数，
```

![](index_files/40134174.png)

```
 首先判断有无缓存文件，没有再去数据库取
```

![](index_files/40284496.png)

删除缓存文件：

![](index_files/3e1c6710-b910-4771-8bc1-0733ee7d72e2.png)

在html模板中使用smarty的保留变量

{$smarty.now}   获得当前的时间戳

{$smarty.const} 获得php文件中定义的常量

{$smarty.config}获得配置文件中的配置项

{$smarty.current\_dir}获得当前的目录

在html模板中还可以使用请求变量

可以通过php保留变量{$smarty}访问几个环境和请求变量

请求变量诸如$\_GET, $\_POST,$\_COOKIE, $\_SERVER, $\_ENV and $\_SESSION

举例说明：

![](index_files/0.4311708069872111.png)

![](index_files/0.1434014937840402.png)

自定义模板引擎类：

![](index_files/0.38336676941253245.png)

![](index_files/clip_image0021d362583-343a-492c-872c-bc490740c9db.jpg)

