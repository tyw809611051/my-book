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
** 7.1 事件介绍**
Javascript中的事件 和 显示生活中事件，有点类似
现实生活中，交通事件、政治事件等等，现实生活中发生这些事之后，我们采用相应的处理
在javascript中，事件指的是用户 和 网页之间发生一些交互的行为、动作（鼠标点击、键盘敲击、手指触摸等），为了用户体验更好，会针对用户的这些行为提供对应处理方案

**7.2  事件分类**
```
鼠标事件：用户拿着鼠标和网页进行交互
- click()  			鼠标单击
- dblclick()			鼠标双击
- mouseover() 		鼠标移入事件
- mouseout()  		鼠标移出事件
- mousemove()		鼠标移动事件
- mousedown()		鼠标按下事件
- mouseup()  		鼠标按键被松开事件
- scroll           	滚动事件（body）

键盘事件：用户通过键盘的按键和网页进行交互
- keydown		键盘按下
- keyup			键盘抬起
触摸事件：用户拿着手指和网页进行交互（手机网页）
- touchstart
- touchmove
touchend
表单事件
- submit		用户提交表单时事件
- select   	文本框的文本被选中
- focus		获得焦点事件
- blur		失去焦点事件
- change		内容改变事件
页面加载完毕事件
- load			页面加载完毕
```

**7.3	监视事件**
> 我们要时刻监视某个元素、标签，监视用户的这些行为是否发生，一旦发生了，我们要做相应的处理

- 直接在html标签上，通过on监视
![](/img/Language/JavaScript/object/77.png)

- 通过javascript监视用户的行为
![](/img/Language/JavaScript/object/78.png)

- 绑定事件监听器
![](/img/Language/JavaScript/object/79.png)

- 通过attachEvent给IE8以下的浏览器监视事件
![](/img/Language/JavaScript/object/80.png)


**7.4 事件捕获、事件冒泡**
当采用事件捕获时，参数3位true的时候，先执行父元素的事件，再执行自己身上的事件
![](/img/Language/JavaScript/object/81.png)

把参数3设置为false，不捕获，采用事件冒泡（就像水里的水泡一样，从水底冒出来），对于事件来说，就是先执行自己身上的函数，再执行父元素身上的函数
![](/img/Language/JavaScript/object/82.png)

**7.5	阻止事件冒泡**
由于我们点击一个元素时，应该是先执行自己身上的事件对应的函数，所以我们通常都是设置为false，外面的元素（父元素身上的事件不应该受影响），所以我们需要设置阻止事件冒泡

主流浏览器是通过事件对象的stopPropogation方法阻止
IE8及以下版本的浏览器采用事件对象的cancelBubble属性 = true阻止

事件对象怎么获得呢？
通常当事件（监视的用户的行为）发生时，会自动产生事件对象，并且会自动传递到事件触发的函数中。通过事件对象可以获得事件发生时，事件主体（鼠标、键盘、手指等）在什么位置等等
![](/img/Language/JavaScript/object/83.png)
![](/img/Language/JavaScript/object/84.png)


**7.6	事件分类演示**
- dblclick: 鼠标双击事件（连续点击两次鼠标）
![](/img/Language/JavaScript/object/85.png)

- mouseover鼠标移入,mouseout鼠标移出
```
mousemove 	鼠标移动事件
鼠标移动时，获得鼠标当前的坐标,也是通过事件对象获得
clientX：距离客户端X轴的距离
clientY
pageX：距离页面的位置，包括滚动条卷去的距离
pageY

mousedown	鼠标按下
mouseup		鼠标抬起

通过鼠标按下行为，我们可以获得用户是左击、还是右击鼠标
通过事件对象的button属性获得，如果属性值为0表示左击、2是右击、1按下的是滑轮

```
![](/img/Language/JavaScript/object/87.png)

scroll：滑轮滚动事件
说明：由于滑轮滚动时，控制的是body在滚动，所以我们应该监视body
![](/img/Language/JavaScript/object/88.png)


keydown键盘按下
keyup键盘抬起
说明：通常我们通过键盘按下、抬起事件，获得用户按下的是哪个键
因为键盘上的每一个按键，都对应一个ascii码，通过事件对象的keyCode属性获得，再根据按键码做相应的判断

![](/img/Language/JavaScript/object/89.png)

在键盘事件中，除了keyCode属性之外，事件对象还提供了如下3个属性：
ctrlKey，只有当用户按下ctrl键的时候，该属性的值才为true
altKey，只有当用户按下alt键的时候，该属性的值才为true
shiftKey，只有当用户按下shift键的时候，该属性的值才为true


解决按下enter键时，默认会自动回车换行，这个回车换行的功能是计算机自带的功能，如何阻止计算机默认的功能呢？
通过事件对象的preventDefault方法设置
![](/img/Language/JavaScript/object/90.png)

**表单事件**

submit		监视用户提交表单的行为
说明：通常在表单提交事件中，使用return true/false 提交或者阻止表单提交
例如：onsubmit=”return false”表示阻止表单提交
![](/img/Language/JavaScript/object/91.png)

但是这个地方我们不能固定死，而应该根据判断返回true 或 false
	我们通常在表单提交事件发生时，验证表单项的内容，如果合法允许提交






