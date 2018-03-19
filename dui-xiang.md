### 数组对象
**1.1 length属性，获得数组元素的个数**

![](/img/Language/JavaScript/object/1.png)

**1.2	concat合并数组，生成一个新的数组**
```
var arr = ['热火队','马刺队','勇士队']
var arr2 = ['皇马队','巴萨队','国足队']

var arr3 = arr.concat(arr2);
```

**1.3	join，将数组的元素连接起来，生成字符串**
```
var arr = ['热火队','马刺队','勇士队']

arr.join(',')
```

**1.4	push、pop；shift、unshift**

**1.5	reverse,颠倒数组的顺序**

**1.6	slice，截取数组的元素**

**1.7	splice，删除数组的元素**
```
参数1：开始的索引位置
参数2：删除的元素个数
参数3：如果有该参数就表示使用该参数代替删除的元素
```

**1.8	toString，将数组转换成字符串**

**1.9	sort，数组排序**

默认会按照数组元素每个数字的第一位进行比较

### 字符串对象
![](/img/Language/JavaScript/object/e478336d-6919-45bb-8ec6-19bf8de6544f.png)

### 数学对象
![](/img/Language/JavaScript/object/a7739c3d-3bc8-4b48-bf61-5aba0242a9d2.png)


### DOM对象

**4.1	DOM介绍**
> Document：文档，指的就是整个html文档
Object：对象
Model：模型（模子，通过不同形状的模子，可以造出不同形状的蛋糕）

文档对象模型，在JavaScript中，也是一个模子


![](/img/Language/JavaScript/object/61.png)


**说明：**
- 当我们在浏览器端打开一个html文档的时候，JavaScript就已经将html文档中的标签转换成了一个一个的节点对象了
- DOM将html标签转换成对象之后，原来标签里面的属性，也会被转换成JavaScript对象的属性

- JavaScript的DOM模型，将html文档的标签转换成一个一个的节点之后，在内存中进行维护，转换之后的对象之间不是孤立存在的，而是有一定的关联

![](/img/Language/JavaScript/object/62.png)

**4.2	查找DOM节点方式**
- 通过id属性查找节点对象
![](/img/Language/JavaScript/object/63.png)

- 通过标签的名字找到该对象
![](/img/Language/JavaScript/object/64.png)

- 通过name属性查找节点对象
![](/img/Language/JavaScript/object/65.png)

- 通过class属性名查找节点对象
> 注意：该方法，是HTML5新增的方法，版本比较新的浏览器都支持，版本低的浏览器不支持，手机浏览器都支持
![](/img/Language/JavaScript/object/66.png)

- 通配符 * 

我们在设置css样式的时候，通常会使用 * 代表所有的标签
![](/img/Language/JavaScript/object/67.png)

![](/img/Language/JavaScript/object/68.png)


**4.3	DOM节点操作**

- 操作属性
    - 对象.属性名 = 属性值
    - dom对象.setAttribute : 设置属性
    - dom对象.getAttribute：获得属性值
    - dom对象.removeAttribute：删除属性值

![](/img/Language/JavaScript/object/69.png)

- 操作内容
    - innerText：只操作标签内的文字内容
    - innerHTML：可以操作标签内的子标签
![](/img/Language/JavaScript/object/70.png)


- 操作样式
> 说明：如果css样式是多个单词的合成词（font-size、margin-top、background-color等），需要采用小驼峰法的形式（fontSize、marginTop）

![](/img/Language/JavaScript/object/71.png)


**4.4	DOM节点添加、删除**
- 新建节点对象
```
document.createElement()
```

- 确定节点位置
```
父节点.appendChild() 
父节点.insertBefore() 
```

- 删除节点：父节点.removeChild(子节点)
![](/img/Language/JavaScript/object/72.png)


**4.5	DOM节点类型**

Dom文档对象模型将html文件里面的标签，转换成javascript的对象之后，我们将这些对象分类总结:

- 标签节点（元素节点）
- 属性节点
- 文本节点
    - 通过nodeName属性获得节点的名称
    - 通过nodeType属性获得节点的类型

![](/img/Language/JavaScript/object/73.png)

**4.6	DOM节点关系**

- 父子关系：childNodes、parentNode

- 兄弟姐妹关系：nextSibling(弟弟节点)、previousSibling(哥哥节点)


### BOM对象

**5.1	BOM对象介绍**
B:Browser，浏览器
O: Object，对象
M: Model，模型
```
history，历史记录：前进、后退、刷新（掌握）
该对象提供了如下方法，操作历史记录：
go(1)，前进一步
go(-1)，后退一步
go(0)，刷新本页面
forward()	前进一步
back()		后退一步
```
![](/img/Language/JavaScript/object/74.png)

location，地址栏相关：（掌握）
该对象提供了href属性，该属性指定跳转到哪个url地址中去
例如：从location.html页面，跳转到百度去

screen，屏幕对象，用来获得屏幕分辨率的宽度、高度（了解）
width
height
availWidth：可用的宽度
availHeight：可用的高度


### window对象

**6.1 window对象介绍**
window对象，是所有对象的顶层对象，包括DOM、BOM对象等都是window对象的子对象
![](/img/Language/JavaScript/object/75.png)

Window对象除了以上的子对象之外，还提供了很多常用的方法，例如：
alert()方法就是window对象的方法
confirm()方法，确认框
![](/img/Language/JavaScript/object/76.png)

```
prompt()，弹出输入框

setInterval()
计时器（类似于定时炸弹，一旦开启之后，每隔一定的时间执行函数）
注意：因为每开启一次计时器，就会在内存中运行一次，如果用户点击了多次，我们需要关闭多次，我们通常在开启定时器之前，先将之前的计时器关闭

setTimeout()
setInterval和setTimeout的区别是什么？
setInterval是间隔执行，每间隔一定时间就执行函数
setTimeout是延迟执行，延迟一定时间之后执行一次

clearTimeout，清除延迟执行
注意：由于延迟执行，是多长时间之后执行一次，删除时也是删除执定的延迟执行

```

### 事件