# Git更新远程仓库代码到本地 

当我们在多台电脑上开发一个项目的时候，需要经常修改提交内容并在另一台电脑上更新远程最新的代码，今天看了一下如何从远程代码仓库获取更新到本地，总结了一下网上的文章，采用如下的方式比较简单。

 

## 方法一

### 查看远程分支

使用如下命令可以查看远程仓库（我这里有一个origin仓库）

```
$ git remote -v

origin  git@github.com:username``/Animations``.git (fetch)``origin  git@github.com:username``/Animations``.git (push)`
```

 

### 从远程获取最新版本到本地

使用如下命令可以在本地新建一个temp分支，并将远程origin仓库的master分支代码下载到本地temp分支

```
$ git fetch origin master:temp

remote: Counting objects: 18, ``done``.``remote: Compressing objects: 100% (6``/6``), ``done``.``remote: Total 11 (delta 3), reused 0 (delta 0)``Unpacking objects: 100% (11``/11``), ``done``.``From github.com:username``/Animations`` ``* [new branch]      master     -> temp``   ``c07bdc7..40f902d  master     -> origin``/master`
```

 

### 比较本地仓库与下载的temp分支

使用如下命令来比较本地代码与刚刚从远程下载下来的代码的区别：

```
$ git diff temp

diff --git a/README.md b/README.md``deleted file mode ``100644``index 76699ed..``0000000``--- a/README.md``+++ /dev/``null``@@ -``1``,``6` `+``0``,``0` `@@``-Animations``-==========``-``。。。`
```

 

### 合并temp分支到本地的master分支

对比区别之后，如果觉得没有问题，可以使用如下命令进行代码合并：

```
$ git merge temp

Updating c07bdc7..40f902d``Fast-forward`` ``README.md                                                  | 6 ++++++`` ``src``/cn/exercise/animations/MainActivity``.java | 4 ++--`` ``2 files changed, 8 insertions(+), 2 deletions(-)`` ``create mode 100644 README.md`
```

 

### 删除temp分支

如果temp分支不想要保留，可以使用如下命令删除该分支：

```
$ git branch -d temp

Deleted branch temp (was 40f902d).`
```

如果该分支的代码之前没有merge到本地，那么删除该分支会报错，可以使用git branch -D temp强制删除该分支。

## 方法二

git pull的作用是，从远程库中获取某个分支的更新，再与本地指定的分支进行自动merge。完整格式是：

```

$ git pull <远程库名> <远程分支名>:<本地分支名>
```

比如，取回远程库中的develop分支，与本地的develop分支进行merge，要写成：

```
git pull origin develop:develop
```

如果是要与本地当前分支merge，则冒号后面的<本地分支名>可以不写。

```
git pull origin develop
```

通常，git会将本地库分支与远程分支之间建立一种追踪关系。比如，在git clone的时候，所有本地分支默认与远程库的同名分支建立追踪关系。也就是说，本地的master分支自动追踪origin/master分支。因此，如果当前处于本地develop分支上，并且本地develop分支与远程的develop分支有追踪关系，那么远程的分支名可以省略：

```
git pull origin
```

其实，git pull 命令等同于先做了git fetch ，再做了git merge。即：

```
git fetch origin develop
git checkout develop
git merge origin/develop
```

或者

```
git fetch origin master:tmp
git diff tmp 
git merge tmp
git branch -d tmp
```

好多人不建议使用git pull，喜欢自己merge，以便万一自动merge出错的时候可以解决冲突

