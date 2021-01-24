# GitHub学习笔记

## 目录

[toc]

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

## 二、开始使用git

### 2.1 基本操作

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
```

6）查看更改前后的差别：`git diff`

查看工作树，暂存区，最新提交之间的差别。