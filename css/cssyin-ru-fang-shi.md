**1.内嵌式**

说明：把CSS样式表当成HTML一个标签来使用，把样式表写到

&lt;head&gt;

&lt;/head&gt;

标签中

语法：

&lt;style type="text/css"&gt;

&lt;/style&gt;

注意：内嵌方式只能在当前（有CSS样式）页面使用

**2.外联方式**

说明：把CSS样式写到一个以.css为后缀的文件中，在HTML文件中引入

语法：

&lt;link rel="stylesheet" type="text/css" href="引入文件的路径"&gt;

注意：在CSS文件中不用写

&lt;style type="text/css"&gt;

```
    一个css文件可以给多个html文件使用
```

**3.行内方式**

说明：把样式当成HTML标签的一个属性来使用

语法：

&lt;div style="border:1px;"&gt;

4.@import

说明：一个CSS文件可以引入另一个CSS文件

语法：@import URL（"路径"）；

