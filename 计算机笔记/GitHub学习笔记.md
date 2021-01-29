# GitHub学习笔记

## 目录

[toc]

---

## 一、准备工作

### 1.1 安装Git

​	在`https://git-scm.com/`上下载安装包后傻瓜式安装。

### 1.2 初始化Git

​	初始化用户

```shell
git config --global user.name "your name"
git config --global user.email "your email"
```

​	提高输出可读性

```shell
git config --global color.ui.auto
```

### 1.3 准备GitHub

 1. 注册账户。

 2. 设置SSH Key

    ```shell
    $ ssh-keygen -t rsa -C "your email"
    Generating public/private rsa key pair.
    Enter file in which to save the key (C:\Users\26411/.ssh/id_rsa):（直接回车）
    Created directory 'C:\Users\26411/.ssh'.
    Enter passphrase (empty for no passphrase):（输入密码）
    Enter same passphrase again:（确认密码）
    ```
    
    我的记录:
    
        ```shell
        Your identification has been saved in C:\Users\26411/.ssh/id_rsa.
        Your public key has been saved in C:\Users\26411/.ssh/id_rsa.pub.
        The key fingerprint is:
        SHA256:kv+6+oOJJ76kPeEisovTztXx4Rw/FqOP+AHl/hUcfGM 2641105219@qq.com
        The key's randomart image is:
        +---[RSA 2048]----+
        |                 |
        |           .     |
        |        .   o E  |
        |       +   . + . |
        |      = S o o    |
        |    .. X = o .   |
        | . .oo.oO + .    |
        |=.o== +..B o     |
        |=*+o+=o+*++      |
        +----[SHA256]-----+
        ```
    
3. 添加公开密钥

   选择Setting，进入SSH and GPG keys

   点击new SSH keys，将`C:\Users\26411\.ssh\id_rsa.pub`中的公钥复制过去
   
   之后就可以使用私钥与GitHub进行通讯
   
   ```shell
   $ ssh -T git@github.com
   ```

---

## 二、开始使用git

### 2.1 基本操作

​		这里介绍了一下最常用的git仓库管理指令。

1）初始化仓库：`git init`

使用后会产生`.git`文件夹，可以认为其为附属于该仓库的文件夹

2）查看仓库状态：`git status`

3）向缓存区内添加文件：`git add`

将文件放入**缓存区**等待commit

4）保存历史记录：`git commit`

将文件保存到仓库的历史记录之中，有几种拓展使用方法

```shell
加入单行信息：git commit -m "commit information"

提交详细记录:git commit
之后会打开编辑器，自动等待提交信息
格式：第一行文字简单记叙内容，第二行为空行，第三行记录更改的原因和详细信息

修改并且直接提交
$ git commit -am "commit information"
```

5）查看提交日志：`git log`

拓展用法：

```shell
只显示一行信息
$ git log --pretty=short

只显示指定目录的日志
$ git log ~

显示文件的改动
$ git log -p ~

以图标的形式来查看
$git log --graph
```

6）查看更改前后的差别：`git diff`

查看工作树，暂存区，最新提交之间的差别。

增加的行有+表示，减少的行用-表示

### 2.2 分支的操作

​		在我们进行并行作业的时候，往往存在多个最新状态，我们可以创建新的分支，等完成后再与master主分支进行合并。

1）显示分支一览表：`git branch`

2）创建、切换分支：`git checkout -b`

​	详细用法：

```shell
只切换到分支A
$ git checkout A

可以使用-来代表上一个分支

创建并进入分支A
$ git checkout -b A
或者执行两条
$ git branch A
$ git checkout A
```

之后的活动都将在分支A下进行，称之为：**培育分支**

​	**特性（Topic）分支**：集中实现单一特性，除此之外不再进行其他操作。

​	**主干分支**：master分支，代码都为开发完全，可以随时给别人查看。

3）合并分支：`git merge`

```shell
在主分支mmaster下操作

为了在历史记录上记录下本次的合并，我们需要加上 --no-ff
$git merge --no-ff A

A分支就会合并到主分支中
```

### 2.3 更改提交的操作

1）回溯历史版本：`git reset`

git的一个特征就是可以灵活的**操作历史版本**。

```shell
让仓库，暂存区以及当前的工作树都回到某一个版本
$ git reset --hard

```

2）推进历史版本

```shell
查看全部日志文件
$ git reflog

推进到返回之前的版本
$ git reset --hard (哈希值只要输入四位以上就可以定位)
```

3）修改提交记录:`git commit --amend`

4）压缩历史：`git rebase -i`

```shell
使用
$ git rebase -i HEAD~2
表示更改了最新的两次记录
```

### 2.4 远程仓库的操作

1）在GitHub上创建远程仓库（记得别勾选initialize this ……）

2）添加远程仓库：`git remote add`

```shell
在GitHub上创建的仓库路径为："git@github.com:用户名/仓库名"
```

3）推送到远程仓库：`git push`

```shell
$ git push -u(使得被推送的仓库成为本仓库的上游仓库，可以pull)
```

4）获取远程仓库：`git clone`

5）获取最新的远程仓库分支：`git pull`

---

## 三、GitHub的使用

