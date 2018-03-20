1.

**圆角**

  border-radius,如果正方形，设置为50%或者宽度一半就是圆形

2.渐变

     参数1：渐变开始的方向（bottom/top/left/right）

     参数2：开始位置的颜色、结束位置的颜色


     linear-gradient（）

![](/img/Language/CSS/css3/Image.png)

![](/img/Language/CSS/css3/1.png)

  


**3、动画：平移、缩放、旋转（2d、3d\)**

**  
**

**水平方向移动：**

**     transform : transalateX**

**     transform : transalateY**

**     transform:  translate\(x像素、y像素\)**

**过渡效果**

：

**transition\(过渡的属性、时间\)**

![](/img/Language/CSS/css3/2.png)

linear:匀速、ease：从快到慢

**缩放：**

**     transform:scale\(x轴放大倍数、y轴放大倍数\)**

**旋转：**

**     transform:rotateX\(旋转的度数\)，单位：deg【2D】**

**  
**

**自定义动画：**

**     1.先定义动画：@keyframes 动画名称{}**

**     通常会使用0%作为开始的地方**

**                    100%作为结束的地方**

**  
**

**     2.调用动画：animation：动画名称 参数列表**

![](/img/Language/CSS/css3/2.png)

![](/img/Language/CSS/css3/3.png)

![](/img/Language/CSS/css3/4.png)

