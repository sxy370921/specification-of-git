# fetch和pull的区别

## 1. git fetch：相当于是从远程获取最新版本到本地，但不会自动 merge 



```
`git fetch origin master``git log -p master origin``/master``git merge origin``/master`
```

以上命令的含义：

首先从远程的 origin 的 master 主分支下载最新的版本到 origin/master 分支上

然后比较本地的 master 分支和 origin/master 分支的差别

最后进行合并

上述过程其实可以用以下更清晰的方式来进行：

```
`git fetch origin master:tmp``git ``diff` `tmp``git merge tmp`
```

从远程获取最新的版本到本地的 tmp 分支上，之后再进行 比较、合并

## 2. git pull：相当于是从远程获取最新版本并 merge 到本地 



```
`git pull origin master`
```

上述命令其实相当于 `git fetch + git merge`，

> 在实际使用中，git fetch 更安全一些，因为在 merge 前，我们可以查看更新情况，然后再决定是否合并。