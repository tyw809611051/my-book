基本语法：
```
<!--action:提交目标地址（当前页可不写/斜杠/当前页链接） method：提交方式 注意所有的name是必须要写的，可以随意命名（尽量与意思一致），如果不写，传值会失败-->
<form action="提交地址" method="提交方式(gei/post)" align="">
存放我们的表单元素
    <input type="text" name="" value="框内的值" size="框的长度" maxlength="规定输入字符的长度">单行文本</input>
</form>\
```
|type|含义|
|---|---|
|button|```<button type="button">按钮</button>```|
|checkbox|```<input type="checkbox" name="须一样" value="最好为数字" checked(默认选中）可以有多个>定义复选框```|
|file|定义输入字段和“浏览按钮”，上传文件使用 name```<input type="file" value="文本" size="12"(文本框)maxlength="1000"(最大字符数) enctype="multipart/form-data"> hidden:<input type="hidden" name="" value="必须有">定义隐藏的输入字段```
|imag|```<input type="image" src="" alt='" width="" height="" border="0">图像形式的按钮```|
|password|```<input type="password" value="文本" size="12"(文本框) maxlength="1000"(最大字符数)>```|
|radio|```<input type="radio" name="单选的name值是一样" value="可以和内容不同，必须要有最好为数字">有值```|
|reset|复位|
|submit|提交|
|text|```<input name type="text" value="文本" size="12"(文本框) maxlength="1000"(最大字符数)>文本```|
|select|```<select name="名称" size="数字/设置显示的个数" multipe="设置多选"><option value="给程序看" selected(默认选中）>给用户看的</option> </select>textarea:<textarea name="" cols="设置宽度" rows="设置高度" maxlength="字符长度">内容</textarea>```|

**get和post区别**
- post相对get而言更安全，不添加信息到url
- 通过表单传输，数据量更大

![](/img/Language/HTML/form/d80d30c8-ed7e-40b0-bee9-f1f900fab873.png)
 
