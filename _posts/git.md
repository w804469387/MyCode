---
title: GIt? Lv.1 和 Lv.99 只差这一步

date: 2021-11-10

author: Samuel
img: https://samuel-1308214755.cos.ap-shanghai.myqcloud.com/img/git.png
top: true
hide: false

cover: true

coverImg:

password:

toc: true

mathjax: false

summary: 众所周知git是一个代码管理仓库，那么他有那些奇淫巧技呢

categories: Git

tags:
  - Git
---

刚入行第一次接触 <b>Git</b> 的时候,只知道他是一个非常强大的代码管理工具，经过几年的捶打，总结一下吧，

---
### 提交错误到仓库的时候


###### 如果你在使用过程中，误操作或者是提交了一个 bug 到仓库了，这个时候可以使用

```bash
$ git reflog
```

你将看到你在 git 上提交的所有改动记录被列了出来，而且囊括了所有的分支，和已被删除的 commit 哦.
每一条记录都有一个类似 HEAD@{index} 的索引编号
找到在犯错前的那个提交记录的索引号，
然后执行

```bash
$ git reset HEAD@{index}
```

### 提交后悔的时候

###### 当你已经提交了 commit 后，才想起来还有一个地方没有修改，这咋整？？

//千万别直接对公共的 commit 上进行修改，否则会让你知道什么社会

首先，添加下当前已改动的代码：

```bash
$ git add .
//或者你可以添加指定的文件
```

然后，运行下面这条命令，它就会把你刚刚添加的代码合并到最后一次提交上了：

```bash
$ git commit --amend
```

什么，你又觉得上次提交的不够好看，想改一下？
ok。可以，。（真事的....)
还是上面提到过的那条代码，运行一下，就可以重新写你想写的了

```bash
$ git commit --amend
```

接下来放大招了：

如果 不小心把新分支的代码提交到主分支上了
别慌，稳住
首先我们先创建一个新的分支

```bash
$ git branch some-new-branch-name
```

然后把刚才的提交从主分支中移除：

```
$ git reset HEAD~ --hard
```

要注意的是，这个操作只能回到最后一条操作上面，
什么？？？
如果你已跑到其它提交记录上怎么办？
没关系，你可以用 git reset HEAD@{number} 再跑回来。
然后在切回到新的分支上面

```
$ git checkout some-new-branch-name
```

概述
### 提交错误的时候

###### 如果代码提交到错误的分支上了

首先撤销这次提交，但保留变更代码：

```
git reset HEAD~ --soft
git stash
```

在切到正确的那个分支去

```
git checkout name-of-the-correct-branch
git stash pop
git add . # 或者你可以添加指定的文件
git commit -m "your message here";
```

现在 你的改动就在正确的分支上啦

### 想看diff的时候

###### 我想用 diff 命令看下改动内容，但啥都没看到?!

如果对文件做了改动，但是通过 diff 命令却看不到，
那很可能是你执行过 add 命令将文件改动添加到了 暂存区 了。你需要添加下面这个参数。

```
git diff --staged
```

此时，你会发现又可以看到了

### 已经麻了的时候

###### 如果你的分支已经乱成一锅粥了，

ok,直接删除当前本地文件

```js
cd ..
sudo rm -r <yougitName>
git clone ...//你的仓库地址
cd yougit
```

参考 [Git 的基本操作](https://www.runoob.com/git/git-basic-operations.html)
