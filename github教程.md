## 本地

```
git init
```

在项目文件夹下打开gitbash，初始化git仓库

```
git status
```

查看文件夹下那些文件是在被跟踪的(主要是代码文件需要被跟踪)，被跟踪标绿的文件才会被提交

```
git add <filename/dir/.>
```

指定哪些文件需要被跟踪，指定单个文件、文件夹或者点表示当前目录下全部文件都可以

```
git commit
```

提交，并编写更新日志

```
git tag <tag number>
```

编辑当前节点的标签，个人习惯写版本号

```
git log
```

查看所有提交

## 远程

```
git remote add origin <ssh/https>
```

让git关联远程仓库，在github新建仓库，复制仓库的ssh或者https连接(国内的https连接貌似不好使，ssh配置百度吧)

```
git push -u origin master
```

推送到github的master分支，-u是指定默认的远端分支，下次再推送就不用再指定origin和master了


