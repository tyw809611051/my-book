1. 配置名字和地址
```
git config --global user.name "xx"
git config --global user.email "xx"
```

2. 配置文件的优先级：
    - etc/gitconfig --system（整个系统用户有效）
    - home/gitconfig --global(当前用户有效）
    - .git/gitconfit --local（当前仓库有效）


3. .git文件夹中的文件：
    - .git/index   暂存区
    - .git/object/*     版本库

4. 初始化git目录
```
git init
```