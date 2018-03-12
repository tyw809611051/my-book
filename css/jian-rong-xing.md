说明：一般情况说的兼容性是指多种浏览器显示一样

浏览器分类：IE和非IE

IE:67891011

非IE：火狐、谷歌、欧朋。。

兼容调试的是IE 6 7 8

**特点：**

**1、左右margin加倍**

![](/img/Language/CSS/compatibility/17d58a0f-6152-4194-8d39-1a135a6533f8.png)

直接告诉浏览器是什么元素：div 为display：block line为display：inline；

![](/img/Language/CSS/compatibility/31454540-e809-4c66-b385-965e7920f03d.jpg)

**2.上下margin合并**

> **使得上下margin和padding值不一样**  
> 网站必须要出事话设置  
>     body {font-size:12px}  
>     border:0px;  
>     在div里面加个小高度  
> &lt;div style="height=1px;"&gt;  
> &lt;/div&gt;  
>     ul,li,ol {list-style:none;}

**3.IE浏览器的margin和padding和字体大小都不一样**

**4.宽度的计算。IE会把padding放到宽里面**

```
边框+外边距+（内容+内边距）
```



