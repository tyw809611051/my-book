#### 背景
公司合作的一个项目需要安装一些软件，而金主粑粑却不想操作太复杂。所以需要我们能够将所有需要安装的软件打包，然后傻瓜式安装

#### 方案
采用InstallShield来进行打包操作

#### 流程
**1. 下载** 
网址：https://www.flexera.com/producer/resources/?type=free-trial
这里我下载试用版，选择一款后填写相关信息，他们会发下载链接到你邮箱

问题1
添加ico文件，仍会提示提示 Error -3204: Cannot Extract icon with specified index [x]
解决方案：
ico文件像素不达标，最后选择516x516