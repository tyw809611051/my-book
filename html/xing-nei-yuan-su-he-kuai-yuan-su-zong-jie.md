块元素(block element)   

* div – 常用块级主要标签   
* dl – 定义列表     
* form – 交互表单   
* h1-h6 – 标题   
* hr – 水平分隔线   
* ol ,ul- 排序表单 ，非排序列表   
* p – 段落 
* pre – 格式化文本
* table – 表格
  * blockquote – 块引用  
行元素(inline element)   不能设置宽，高和text-align

  * a – 锚点   
* br – 换行    
* em – 强调   
* i – 斜体   
* img – 图片   
* input – 输入框   
* label – 表格标签   
* q – 短引用   
* select – 项目选择   
* span – 常用内联容器，定义文本内区块   
* sub – 下标   
* sup – 上标   
* textarea – 多行文本输入框   
* var – 定义变量    

1.块级标签可以设置宽高(width、height)和text-align;

行标签由内容撑开，不能设置宽高和text-align;

 

需要注意：行标签<img>、<textarea>、单独使用的<select>(读者不必了解，没有实际应用场景)和<input>系列标签可以设置宽高;

并且<textarea>可以设置text-align，<input>系列标签除了type为checkbox、radio、file、hideen的标签不可以设置text-align，其他标签都可以(内容默认是垂直居中)。

 
2.所有标签都可以设置左右margin;
块级标签可以设置上下margin;

行内标签不可以设置上下margin;

 

需要注意：行标签<img>、<textarea>、单独使用的<select>、<input>系列标签可以设置上下margin并有效果。

 

3.所有标签都可以设置左右padding；

块级标签可以设置上下padding；

行内标签不可以设置上下padding；

 

需要注意：

a.<input>type为checkbox、radio属性标签不能设置上下、左右padding。

b.行标签<img>、<textarea>、单独使用的<select>、<input>系列标签可以设置上下padding;

c.特别要注意<img>可以设置上下、左右padding，但是图片不会像背景一样填充padding，详见以上测试效果；

d.<input>type为reset、button、submit标签可以设置上下、左右padding，但是其padding会包含在元素本身的width和height中，为了避免这类不可控的情况，我们一般不会在此类<input>标签中设置padding，或者我们一般会用其他标签模拟实现<input>标签的功能，但能够更好的控制其样式。

 

4.块标签和行内标签在任何情况下都可以设置border属性，并有相应的效果。

说明：块标签<br>标签和行标签<input type="hidden">标签不需考虑设置属性，因为其在页面中没有效果。

 

二、所有标签转换为块级标签
 

1.所有标签都可以设置宽高和text-align；

相关注意事项同默认情况一样。

 

2.所有标签都可以设置上下、左右margin；

 

3.所有标签都可以设置上下、左右padding；

相关注意事项同默认情况一样。

 

三、所有标签转换为行内标签

 
1.所有标签表现为行标签属性，不能设置宽高和text-align，由内容撑开。
相关注意事项同默认情况一样。
 

2.所有标签可以设置左右margin，不能设置上下margin。

相关注意事项同默认情况一样。

 

3.所有标签都可以设置左右padding，不能设置上下padding。

相关注意事项同默认情况一样。


