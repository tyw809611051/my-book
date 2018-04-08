**简介：**
Windows Server 2003 Resource Kit Tools是一组为管理员、开发者和高级用户设计的软件工具，包括管理活动目录、组策略、TCP/IP网络、注册表、系统安全、监测等涉及Windows Server 2003 操作系统的其它很多方面的非常规安装的工具组

**下载链接：**
[下载链接](https://www.microsoft.com/en-us/download/details.aspx?id=17657)

**步骤：**
- 下载文件解压后找到instsrv.exe（给系统安装和删除服务），srvany.exe（让程序以服务的方式运行）
- cmd输入 path\instsrv.exe 服务名 path\srvany.exe path为实际位置，成功则返回successfully added
- 运行输入regedit 进入注册表，进入HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services 下找到刚刚注册的服务，在其右击新建一个项，名称为Parameters,新建选中后，在后侧窗口新建一个字符串值名称为Application,将其值设为服务运行程序的全路径 如：D:\\elasticsearch\\bin\\elasticsearch.bat **注意：**用双斜杠隔开
- 运行输入services.msc打开服务管理可以看到
- 删除服务：path\instsrv.exe 服务名 remove