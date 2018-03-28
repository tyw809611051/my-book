#### 进程
语法

```
TASKLIST [/S system [/U username [/P [password]]]] [/M [module] | /SVC | /V] [/FI filter]
[/FO format] [/NH]
```
|选项|描述|
|---|---|
|/S system|指定要连接的远程系统|
|/U [domain]user |- 指定命令应在其下执行的用户上下文。|
|/P [password]| - 指定给定用户上下文的密码。 提示输入，如果省略。|
|/M [module] |- 列出当前使用给定的exe / dll名称的所有任务。 如果未指定模块名称，则显示所有已加载的模块。|
|/SVC |- 显示每个进程中托管的服务。|
|/V |- 显示详细的任务信息。|
|/FI filter| - 显示一组符合过滤器指定条件的任务。|
|/FO format| - 指定输出格式。 有效值:TABLE，LIST，CSV。|
|/NH |- 指定“列标题”不应显示在输出中。 仅适用于TABLE和CSV格式。|
```
tasklist /fi "memusage gt 40000"
#获取内存大于40MB的进程
```

**杀死/终止一个进程**
语法
```
TASKKILL [/S system [/U username [/P [password]]]] { [/FI filter] 
[/PID processid | /IM imagename] } [/T] [/F]
```
|选项|描述|
|---|---|
|/S system| - 指定要连接的远程系统|
|/U [domain]user| - 指定命令应在其下执行的用户上下文。|
|/P [password]| - 指定给定用户上下文的密码。 提示输入，如果省略。|
|/FI FilterName| - 应用过滤器来选择一组任务，允许使用*通配符。|
|/PID processID |- 指定要终止的进程的PID。使用TaskList来获取PID。|
|/IM ImageName| - 指定要终止的进程的映像名称。 通配符*可用于指定所有任务或图像名称。|
|/T |- 终止指定的进程以及由其启动的任何子进程。|
|/F |- 指定强制终止进程。|

```
taskkill /f /im notepad.exe
#杀死(终止)打开的记事本任务。
taskill /pid 9901
一个ID为9901的进程。
```

**启动一个新的过程**
语法
```
START "title" [/D path] [options] "command" [parameters]
```
|选项|描述|
|---|---|
|title| - CMD窗口标题栏的文本(必需)|
|path |- 起始目录。|
|command |- 命令，批处理文件或可执行程序运行。|
|parameters |- 传递给命令的参数。|
|/MIN| - 启动窗口最小化。|
|/MAX |- 启动窗口最大化。|
|/LOW| - 使用IDLE优先级。|
|/NORMAL| - 使用NORMAL优先级。|
|/ABOVENORMAL| - 使用ABOVENORMAL优先级。|
|/BELOWNORMAL |- 使用BELOWNORMAL优先级。|
|/HIGH |- 使用HIGH优先级。|
|/REALTIME |- 使用REALTIME优先级。|

示例
```
START "Test Batch Script" /Min test.bat
#在新窗口中运行批处理脚本test.bat。 窗口将以最小化模式启动，并且指定标题为:“Test Batch Script”
START "" "C:\Program Files\Microsoft Office\Winword.exe" "D:\test\TESTA.txt"
#在另一个进程中运行Microsoft Word，然后在MS Word中打开文件TESTA.txt
```