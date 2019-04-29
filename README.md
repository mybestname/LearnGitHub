# Learn GitHub
Learn by practicing

## 写在前面

教程的目的是让零基础小白能学会使用GitHub完成工作任务。
我们将通过该教程学会使用Git完成如下内容：

* 安装下载一个Git
* Fork项目到自己的仓库
* 修改文件
* Push自己的修改文档
* 同步最新版本



### 下载及安装

在使用Git前我们需要先安装 Git。Git 目前支持 Linux/Unix、Solaris、Mac和 Windows 平台上运行。
Git 各平台安装包下载地址为：http://git-scm.com/downloads 。

安装完成后打开终端输入：
```
> git --version
  git version 2.16.2
```
这就说明已经安装成功了。

然后在自己的PC端建个文件夹，打开这个文件夹，进入终端，输入：
```
> git init
```
初始化文件夹，以后的项目都可以放到这个文件夹。


### Fork这个项目

首先你得有自己的git账号，如果没有请点击最右上角的 "Sign Up" 按钮。
有账号的登录自己的账号。

先 Fork 该教程到自己的仓库，如图点击右上角：
![fork](./image/clone_git.png)


复制链接，在终端中输入：
```
> git clone https://github.com/******/LearnGitHub.git 
```
经过一系列的操作后，你就可以在自己的仓库中看到这个项目了。


### 修改本地文件

克隆完这个项目后，打开文件夹就可以看到这个项目的本地文件了，用户编辑器打开 README.md
就可以尽请的添加你想添加的内容了。

接下来你可以在文件夹中新建一个 TEST.md 文件，打开文件，输入：这是我的第一个 Git 提交，保存文件。
切换到终端，输入：
```
> git status
  ...
  modified:   TEST.md
  ...
```

这个命令是查看本地代码库修改了写啥。


### 更新自己的GIT

`git status` 命令是查看本地代码库被修改过得文件，`modified:   TEST.md` 红色表示 `TEST.md` 这个文件被修改了。

现在我们在终端执行：
```
> git add TEST.md
```
这个命令是将`TEST.md`这个被修改的文件添加到本地git代码仓库，`git add .` 表示将所有的修改添加到本地git代码仓库。
完成后，在输入：
```
> git status
```
可以看到`TEST.md`已变成绿色，说明更改添加到本地Git仓库。
继续在终端输入：
```
> git commit -m '第一次提交'
```
`git commit -m '第一次提交'` 命令是将自己的修改做提交处理，`-m` 后面的内容可以自己编写，说明本次提交的目的即可。

commit 完成后，再次 `git status` 你会发现已经看不到 `TEST.md` 文件。

> 提示：如果git提示：Please tell me who you are ，这是因为git提交需要设置你提交使用的用户名，和邮箱。你需要输入：

```
> git config --global user.email '你的注册邮箱'
> git config --global user.name '你的用户名'
```
 
最后我们运行【需联网】：
```
> git push 
```
完成后，在GitHub上就可以看到自己的更新的`TEST.md` 文件了。



### 处理冲突

当同一个文件由多个参与着一起维护时，不可避免的会出现两个参与者同时对一份文档做了不同的修改，这时两个参与者再 `git push` 时会遇到文档冲突问题。

如：A参与者在自己的本地仓库中在 `TEST.md` 文档末尾添加内容。同时B参与者也在自己本地仓库中的 `TEST.md` 文档末尾添加了不同的内容。此时 `TEST.md` 将会有 3 个版本：

* GitHub 上保存原 `TEST.md` 版本
* A参与者的 `TEST.md` 版本
* B参与者的 `TEST.md` 版本

如果A参与先Push自己的版本到 GitHub 上，将原版覆盖后 B 在 Push 自己的 `TEST.md` 版本，A 和 B 提交的版本就会冲突，因为 A 和 B 都是基于 GitHub 上保存的原 `TEST.md` 版本进行修改的，
A 提交时 `TEST.md` 版本已更新，B 还是基于上一版本，B Push的版本就和 A 版本属于冲突版本【都是基于原 `TEST.md` 版本修改的】，这时 B 就需要修改自己的 `TEST.md` ，重新提交。

#### 具体操作

我们先模拟 A 参与者修改 `TEST.md` 文档，操作很简单，在 GitHub 上进入 `TEST.md` 文档：
![fork](./image/eidt.png)
点击铅笔，在线编辑文档，完成后点`commit change`，标题可写成 `A 参与者` ，这个动作相当于执行 `git commit -m 'A 参与者'` 命令。

成功后可以看到 `TEST.md` 已被修改。

现在我们回到本地 `TEST.md` 文档中，在尾部添加`这是 B 参与者添加的内容`，保存，然后运行我们熟悉的4个命令【复习一遍】：
```
> git status
> git add .
> git commit -m 'B 参与者'
> git push
```

我们发现Push失败了，提示：
```$xslt
To https://github.com/zhangyi999/LearnGitHub.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/zhangyi999/LearnGitHub.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

解决方法很简单，首先：
```$xslt
> git pull
```
这个命令的作用是将远程代码更新到本地 Git 代码库。
我们在打开本地`TEST.md` 文件，发现文件已被修改：
```$xslt
这是我的第一个提交。

这是 B 参与者的提交。
```
以下部分便是冲突的部分，我们需要根据情况修改自己代码，更改以后保存，便可以重新提交。
我们将文本改成：
```$xslt
这是我的第一个提交。

我是 A 参与者，我提交了一个版本。

这是 B 参与者的提交。
```

接下来重新 4 步骤：
```
> git status
> git add .
> git commit -m 'merge'
> git push
```
大功告成。
> 注意：我们要养成良好的协作习惯，每次修改前更新下自己的文档，保持文档最新。
```$xslt
> git pull
```
更新本地代码仓库。

### 删除文件
首先通过 `rm -r file` 删除本地文件，在执行 `git rm -r file`，接下来就是我们熟悉的 4 步骤，**push** 以后文件便被删除。

### 提交自己的修改到源码库（Pull Request 即 PR）

一开始，我们是将 zhangyi999/LearnGitHub 的内容 Fork 到自己的仓库，相当于复制了一份给自己。

我们在自己的仓库修改自己的文档内容，并不会影响到源文档内容【即 zhangyi999/LearnGitHub 文档】，这样设计是为了方便我们协作，不至于大家在同一个文档上相互覆盖。

当我们修改完成本地文档后，我们需要将自己的修改发送给原作者【 这里是 zhangyi999 】，原作者决定是否更新到源文档。这里我们就要使用 `Pull Request` 功能。
 
具体操作，进入自己的 LearnGitHub 库页面，点击 `Pull Request`：

![pullrepust](./image/pullrepust.png)

点击`create pull repust`，填写更新理由，即可提交更新需求。



### 更新自己的代码库

你GitHub上的代码库是从 zhangyi999 这个库fork过去，这会导致一个问题就是：当源项目更新后，你fork的分支并不会一起更新，需要自己手动去更新。

接下来我们练习一下通过源码库到本地。

1、增加源分支地址到你项目远程分支列表中(此处是关键)，先得将原来的仓库指定为upstream，命令为：
```
> git remote add upstream https://github.com/zhangyi999/LearnGitHub.git
```
这里的git地址是你 FORK 的源码仓库地址。

2、fetch源分支的新版本到本地
```
> git fetch upstream
```

3、合并两个版本的代码
```
> git merge upstream/master
```
  
4、将合并后的代码push到github上去
```
> git push origin master
```

这个流程主要是为了同步源码库更新，比如长时间没更新代码，就需要在修改本地代码前先同步源码。

