#### 1. 需要了解
![](/img/Language/ReactJS/introduce/introduce.png)

#### 2. 介绍
- facebook出品
- 是一个采用声明式，高效而且灵活的用来构建用户界面的框架
- 简单的表述任意时间点你的应用应该是什么样子的，React将会自动的管理UI界面更新当数据发生变化的时候
- React不是一个MVC框架
- React不使用模板

#### 3. 比较分析

和其他一些js框架相比，React怎样，比如Backbone、Angular等。

- React不是一个MVC框架，它是构建易于可重复调用的web组件，侧重于UI, 也就是view层
- 其次React是单向的从数据到视图的渲染，非双向数据绑定
- 不直接操作DOM对象，而是通过虚拟DOM通过diff算法以最小的步骤作用到真实的DOM上。
- 不便于直接操作DOM，大多数时间只是对 virtual DOM 进行编程