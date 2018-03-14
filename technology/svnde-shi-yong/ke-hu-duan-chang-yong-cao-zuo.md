**svn import**
```
svn import Contacts 服务器端地址 -m "说明”
```

**svn co(checkout)**
1.检出工作拷贝到  ~/svn/workcopy
```
svn co 地址链接 ~/svn/workcopy
```

**svn up(update)**
更新工作副本到最新
```
svn ~/svn/workcopy
or
cd ~/svn/workcopy
svn up
更新到指定版本
svn up ~/svn/workcopy -r 100
```

**svn st(status)**
```
local@loacl:~/svn/workcopy$ svn st
 M ~/svn/workcopy/xxx.c  表明文件已经有修改
 ？ ~/svn/workcopy/xxx.c 表明文件没有受版本控制
 ！ ~/svn/workcopy/xxx.c 表示文件丢失 
 ````

**svn log**
```
svn log    查看所有版本的log信息
svn log -r 5    查看某一版本的log信息
svn log -r 5:19 查看某区间一系列的版本的log信息
查看log的详细信息加上-V选项
```

**svn diff**
作用
1.检查本地修改
2.比较工作拷贝与版本库
3.比较版本库与版本库
l.不带参数 svn diff ~/svn/workcopy 比较你的工作文件与缓存的.svn的原始拷贝
ll.带--revision -r参数 svn diff -r 3/2:3 ~/svn/workcopy 与指定版本比较/比较2个版本
```
svn list
svn list 地址      查看版本库的文件列表
svn list ~/svn/workcopy     查看本地工作目录列表

svn info
svn info ~/svn/workcopy 查看本地副本信息
svn info 服务器地址  查看服务器端的版本信息

svn add
cd ~/svn/workcopy
svn add Phone/ --no-ignore
svn add xxx.c
(注意：添加目录时，加上--no-ignore,否则可能会缺少文件，比如*.o）
$ svn add auto_sync_android.log 
A        auto_sync_android.log

svn delete
svn del Phone/

svn revert
svn revert ~/svn/workcopy/Phone/ -R 取消本地修改

svn commit
svn commit ~/svn/workcopy/packages/apps/Phone -m "log信息"
```