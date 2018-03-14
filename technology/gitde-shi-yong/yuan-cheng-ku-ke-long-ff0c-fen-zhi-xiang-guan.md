1.从github上克隆自己/别人的信息
```
git clone git@gitHub.com:帐号/文件.git （-b 本地仓库）
```

2.查看分支
```
git branch
```

3.创建+切换分支
```
git checkout -b <分支名>
```

4.合并xx分支到当前分支
```
git merge <xx>
```

5.删除分支
```
git branch -d <xx>
```

6.以图形显示分支合并的情况
```
git log -graph --pretty=online --abbrev-commit
```

7.合并时生成新的提交
```
git merge --no-ff -m "说明" dev
```

8.丢弃没有被合并的分支
```
git branch -D <name>
```
