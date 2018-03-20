![](/img/Language/JavaScript/ajax/1.png)

**创建ajax对象**

    **主流浏览器: var xhr  =  new XMLHttpRequest\(\);**

    **IE浏览器:  var xhr = new  ActiveXObject\(“Msxml2.XMLHTTP.6.0”\)**

**ajax对象成员属性：responseText、readyState、**

**onreadystatechange、responseXML\(针对xml文件\)**

**方法：open\(\)、send\(\)、setRequestHeader\(\)**

get请求：

①传递参数位置

②特殊符号和中文处理

encodeURIComponent\(\)

post请求：

①传递参数位置send\(\)

②设置setRequestHeader\(\)方法

③特殊符号处理

④同时可以传递GET参数信息

**Ajax对象的创建：**

主流浏览器通过：new XMLHttpRequest\(\)

```
 非主流（IE低版本的浏览器）new ActiveXObject\('Microsoft.XMLHTTP'\)
```

## **1.创建ajax对象**

### **1.1主流浏览器方式**

火狐、chrome\(google\)、safari\(苹果\)、opera包括IE7以上版本的浏览器

var xhr =new XMLHttpRequest\(\);

### **1.2 IE\(6/7/8\)方式**

var xhr = new ActiveXObject\(“Microsoft.XMLHTTP”\);  //最原始方式

var xhr = new ActiveXObject\(“Msxml2.XMLHTTP”\);    //升级

var xhr = new ActiveXObject\(“Msxml2.XMLHTTP.3.0”\);  //升级

var xhr = new ActiveXObject\(“Msxml2.XMLHTTP.5.0”\);  //升级

var xhr = new ActiveXObject\(“Msxml2.XMLHTTP.6.0”\);  //IE

维护的最高版本

![](/img/Language/JavaScript/ajax/2.png)

ajax常用方法：

![](/img/Language/JavaScript/ajax/3.png "graphic")

ajax常用属性：

![](/img/Language/JavaScript/ajax/4.png "graphic")

### **4.1 get/post两者的不同**

**①给服务器传递数据量**

**   get方式的大小是受限于浏览器，大部分浏览器是2k的限制每个浏览器的限制不一样**

**  chrome就是8K**

**                                          http://网址/index.php?name=tom上述请求通过get方式传递了9个字节的信息**

**                                          1024字节= 1k**

**  post原则没有限制，**

**php.ini对其限制为8M**

**②安全方面，post传递数据较安全**

**③传递数据的形式不一样**

**       get方式在url地址后边以请求字符串形式传递参数**

**       http://网址/index.php?name=tom&age=23&addr=beijing**

**蓝色部分就是请求字符串，就是一些“名值”对，中间使用&符号连接。**

**post方式是把form表单的数据给请求出来以xml形式传递给服务器**

### **ajax之get方式请求**

ajax之get请求需要注意的两个地方：

①在url地址后边以请求字符串\(传递的get参数信息\)形式传递数据。

②对中文、=、&等特殊符号处理对特殊信息的处理在浏览器里通过get参数传递一些特殊符号信息会被误解混淆，例如&=等。为了避免特殊符号被误解产生歧义，需要对其进行编码处理。同时如果传递get参数中文信息，也需要编码处理。

①．在php里边可以函数urlencode\(\)/urldecode\(\)对特殊符号进行编码、反编码处理

②．在javascript里边可以通过encodeURIComponent\(\)对特殊符号等信息进行编码。\(以上红色函数可以把”特殊符号、中文”转变为浏览器可以识别不会混淆的信息。编码后的信息为%号后接两个十六进制数\)编码后的信息可以被正常接收使用，无需反编码。

**具体可以被编码的特殊符号：**

![](/img/Language/JavaScript/ajax/5.png "graphic")

### **ajax之post方式请求**

### ajax之get请求需要注意的四个地方：

①给服务器传递数据需要调用send\(请求字符串数据\)方法

②调用方法setRequestHeader\(\)把传递的数据组织为xml格式\(模仿form表单传递数据\)

③传递的中文信息无需编码，特殊符号像、=等仍需要编码

④该方式请求的同时也可以传递get参数信息，同样使用

$\_GET接收该信息

post方式请求需要把信息组织为请求字符串传递给

send\(\)方法：

**    
**

