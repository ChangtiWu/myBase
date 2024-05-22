# Git

## 基本操作

**拉取远端最新仓库**

```cmd
git pull origin 分支
```



## 本地仓库修改后同步到远程仓库

### 添加文件&修改文件内容

本地直接新建文件&修改文件内容，正常add>commit>push即可。

```cmd
git add 新文件名
git commit –m "add"
git push origin 分支
```

### 删除文件

不能在本地直接删除！否则远程仓库后上原文件没有变化！应该在git bush中输入命令：

```cmd
git rm 文件名
git commit –m "delete"
git push origin 分支
```

若删除文件夹，第一行改成：

```cmd
git rm -r 文件夹名
```

删除文件夹时，文件夹不能为空，否则不能找到文件夹从而无法删除。

### 修改文件名称

不能在本地直接修改！否则上传远程仓库后会新增该文件，而原文件没有变化！应该在git bush中输入命令：

```cmd
git mv 旧文件名 新文件名
git commit –m "rename"
git push origin 分支
```

第一行也可以写成

```cmd
git mv --force 旧文件名 新文件名
```

## 拉取远程仓库

### 强制拉取并覆盖本地文件

```cmd
#需要将这些更新取回本地，这时就要用到git fetch命令
git fetch --all
#撤销本地、暂存区、版本库（用远程服务器的origin/master替换本地）
git reset --hard origin/master
#git pull 来从远程仓库拉取同步代码
git pull origin master
```



> 参考资料：
>
> 1. https://juejin.cn/post/7029615515492433957
