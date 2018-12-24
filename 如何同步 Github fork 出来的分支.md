# 如何同步 Github fork 出来的分支

发表于 2015-10-12   |   分类于 [github ](https://jinlong.github.io/categories/github/)  |  

原先一直有个疑惑， Github fork 出来的项目，我已经做了部分修改，由于某些原因，无法提交 Pull Request，可是想把原项目的最近更新代码合并进来怎么办？google 了一下才茅塞顿开，年纪大了，这里记录一下吧。

两种方式：

1. 项目 fetch 到本地，通过命令行的方式 merge
2. 懒人方法，只用 Github ，不用命令行



# 项目 fetch 到本地，通过命令行的方式 merge

提示：跟上游仓库同步代码之前，必须配置过 remote，[指向上游仓库](https://help.github.com/articles/configuring-a-remote-for-a-fork/) 。

```
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

1. 打开命令行工具

2. 切换当前工作路径至你的本地工程

3. 从上游仓库获取到分支，及相关的提交信息，它们将被保存在本地的 `upstream/master` 分支

   ```
   git fetch upstream
   # remote: Counting objects: 75, done.
   # remote: Compressing objects: 100% (53/53), done.
   # remote: Total 62 (delta 27), reused 44 (delta 9)
   # Unpacking objects: 100% (62/62), done.
   # From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
   #  * [new branch]      master     -> upstream/master
   ```

4. 切换到本地的 `master` 分支

   ```
   git checkout master
   # Switched to branch 'master'
   ```

5. 把 `upstream/master` 分支合并到本地的 `master` 分支，本地的 `master` 分支便跟上游仓库保持同步了，并且没有丢失你本地的修改。

   ```
   git merge upstream/master
   # Updating a422352..5fdff0f
   # Fast-forward
   #  README                    |    9 -------
   #  README.md                 |    7 ++++++
   #  2 files changed, 7 insertions(+), 9 deletions(-)
   #  delete mode 100644 README
   #  create mode 100644 README.md
   ```

提示：同步后的代码仅仅是保存在本地仓库，记得 `push` 到 Github 哟。

# 懒人方法，只用 github ，不用命令行

盗几张[知乎的图](http://www.zhihu.com/question/20393785)，见图知意。

[![步骤1](https://jinlong.github.io/image/sync-a-fork/1.jpg)](https://jinlong.github.io/image/sync-a-fork/1.jpg)
[![步骤2](https://jinlong.github.io/image/sync-a-fork/2.jpg)](https://jinlong.github.io/image/sync-a-fork/2.jpg)
[![步骤3](https://jinlong.github.io/image/sync-a-fork/3.jpg)](https://jinlong.github.io/image/sync-a-fork/3.jpg)
[![步骤4](https://jinlong.github.io/image/sync-a-fork/4.jpg)](https://jinlong.github.io/image/sync-a-fork/4.jpg)
这一页往下面拉:
[![步骤5](https://jinlong.github.io/image/sync-a-fork/5.jpg)](https://jinlong.github.io/image/sync-a-fork/5.jpg)

# 参考资料：

- 《[Github 上怎样把新 commits 使用在自己的 fork 上？](http://www.zhihu.com/question/20393785)》
- 《[更新從Github上fork出來的repository (或是同步兩個不同server端的repository)](https://www.peterdavehello.org/2014/02/update_forked_repository/)》
- 《[Syncing a fork](https://help.github.com/articles/syncing-a-fork/)》