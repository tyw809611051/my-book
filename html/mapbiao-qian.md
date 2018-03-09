作用：点击图像中的某些区域可跳转到指定链接
前置条件：须有个图像
属性：
![](/img/Language/HTML/map/b1e5f3ff-8ac7-475a-bf5d-c9c8c4e51621.png)

例子：
```
<!--须有个图形,且img中有usemap-->
<img src="目标链接" usemap="#标识" alt="警告语">
<map name="标识" id="标识">
    <area shape="circle/rect" coords="坐标" href="链接" alt="告示语">
</map>
```


 