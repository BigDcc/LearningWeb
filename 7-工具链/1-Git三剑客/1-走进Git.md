[TOC]

## 1 Git入门与设置

### 1.1 Git简介

- `Git`的主要作用是在开发过程中利用版本控制的思想管理代码的版本迭代；
- 通常的版本控制工具分为集中式版本控制工具（`SVN`）和分布式版本控制工具（`Git`）,集中式版本控制工具，容易在服务器脱机或者损坏的情况下，出现单点故障，严重时导致数据丢失。而分布时的版本控制工具避免了单点故障出现的严重后果；
- `Linus`利用`C`语言开发了`Git`工具，`Git`已成为当前最著名的版本控制工具，`Git`相关的命令与`Linux`命令兼容；
- `Git`可以对任何类型的文件进行版本控制，但是通常用来管理源代码，也就是纯文本的内容，图片等内容通常只能感知数据大小的变化；
- 通常我们使用`Git`提供的命令行去管理仓库，而非基于命令行的`GUI`程序；
- 通常我们在使用`Git`版本控制的时候，利用集中式的思想，建立一个主仓，而在本地库进行开发，主仓又叫做远程库，在局域网环境下通常使用`GitLab`托管代码，在外网环境下通常使用`GitHub`或者码云进行托管。

> - [Git官方网站](https://git-scm.com)
> - **版本控制**是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统
> - **分布式版本控制系统**把代码仓库完整地镜像下来，包括完整的历史记录，分布在每一个使用节点之上
> - Git 把数据看作是对小型文件系统的一系列快照，实际操作中是在操作快照流，所以他的速度很快

### 1.2 安装Git与初始配置

#### 1.2.1 安装Git

安装`Git`的方式有很多，通常分为以下几类：

- 软件包安装
  - 绿色解压安装
  - 包管理工具安装
  - 下载安装包安装
- 源码安装

`Git`支持全平台，不同平台的安装详情可以查看，[Git安装指导](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)， 这里介绍在`ubuntu`下使用`apt`如何安装`Git`。

1. 使用`Ubuntu`中的包管理软件`apt`进行安装。

```shell
sudo apt install git-all
```

2. 检验`Git`是否安装成功。

```shell
git --version  # 查看git版本
```

#### 1.2.2 签名设置

签名的初始化和仓库工作树的初始化，是不分前后顺序的。先建立哪一个都可以。但是必须保证这两个都进行了相关操作，再开启我们的`Git`之旅，因为`Git`默认不允许不带签名去提交变更。

通常签名有三种作用域范围， 它们的优先级依次升高。

- 系统级（System）
- 用户级（Global）
- 仓库级（Local）

最常使用的设置，就是用户级和仓库级。

##### 1.2.2.1 用户级设置

```shell
# 进行用户级配置

git config --global user.name "用户名"
git config --global user.email "邮箱"

# 查看当前用户配置列表

 git config --global --list

 # 配置文件存放位置

 ~/.gitconfig
```

##### 1.2.2.2 仓库签名设置

```shell
# 进行仓库级设置，由于优先级较高，会覆盖global和System的设置

git config user.name "用户名"
git config user.email "邮箱"

# 查看当前仓库配置列表

git config --list

# 配置文件存放位置

your_project_name/.git/config  # 配置文件存放位置在当前仓库中
```

> 这里值得注意的是，设置的姓名和邮箱地址，会用在`Git`的提交日志中，由于在`GitHub`上公开仓库时，这里的姓名和邮箱地址也会随着提交日志一同被公开，所以请不要使用不便公开的隐私信息。

#### 1.2.3 获取帮助

```shell
git help command  # 获得全面的帮助信息
git command -h  # 获得command命令参数的快速参考
```

#### 1.2.4 配置Git

##### 1.2.4.1 配置命令

`Git`提供了配置工具`git config`，来设置 `Git` 外观和行为，这些设置项通常保存在以下的文件当中：

- `/etc/gitconfig`  # 针对系统
- `~/.gitconfig`  # 针对当前用户
- `./.git/config`  # 针对当前仓库

`Git`配置文件采用的是`INI`文件格式， 通过`git config`命令来读写配置属性

```shell
# 可使用命令快速编辑配置文件

git config -e <作用域名参数>  # 不写作用域名时，默认本地仓库

# 读取配置文件中的属性值 => git config <section>.<key>

git config alias.st # 读取alias章节中的st属性指代的值

# 修改配置文件中的属性值 => git config alias.st

git config alias.st log # 使用st指代log
```
低级别的配置文件会覆盖高级别的配置文件，既我们常说的就近原则，就像我们前面设置的签名，如果同时设置了用户签名和仓库签名，那git在管理文件的时候优先使用当前仓库的配置文件。

##### 1.2.4.2 配置vim为默认编辑器

`Git`在日常的使用当中会调用编辑器进行一些相关的操作，如提交时编写详细的编辑信息，这时我们可以为它指定一个我们熟悉的编辑器，如下所示（指定vim）

```shell
git config --global core.editor vim
```

`windows`中可以使用`notepad++`来作为默认编辑器

```powershell
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

##### 1.2.4.3 设置别名

跟`linux`中别名相同，可以给`git`也设置别名，简化长命令

```shell
sudo git config --system alias.st status  # 通常给系统级设置方便一点
```

##### 1.2.4.4 提高可读性

在`Git`命令输出中开启颜色显示，可提高命令行可读性

```shell
git config --global color.ui true  # 关闭使用false
```

### 1.3 初始化Git仓库

通常有两种获取 `Git` 项目仓库的方式：

1. 将尚未进行版本控制的本地目录转换为 `Git` 仓库；
2. 从其它服务器 克隆 一个已存在的 `Git` 仓库；

#### 1.3.1 初始化自己的仓库

将已有项目纳入`Git`管理或者新建一个`Git`项目，需要使用`git init`命令。

```shell
# 1. 初始化一个git项目
git init your_project_name  # 在当前目录下生成一个your_project_name文件夹即生成了一个空的git项目

l$ ls -alh your_project_name  # 查看初始仓的目录结构
total 8.0K
drwxr-xr-x 1 30678 197609 0  2月  4 21:27 ./
drwxr-xr-x 1 30678 197609 0  2月  4 21:27 ../
drwxr-xr-x 1 30678 197609 0  2月  4 21:27 .git/

# 2. 将已有项目纳入git管理

cd your_project_name
git init  # 同样会生成.git文件夹
```

#### 1.3.2 克隆他人仓库

初始化一个仓库的另一种方式就是克隆一个别人的仓库，克隆操作支持多种协议，它可以将远程仓库的数据全部拉取到本地，包括`.git`文件夹，这样我们在获取数据的同时，也就获取到了一个`Git`仓库，以下演示从`GitHub`上通过`https`协议获取一个远程仓库。

```shell
git clone https://github.com/BigDcc/learningNotes.git  # 获取名为learningNotes的仓库
```

克隆时也可以为仓库指定名称，语法如下：

```shell
git clone https://github.com/BigDcc/learningNotes.git  demo # 获取名为learningNotes的仓库,并将learningNotes改为demo
```

### 1.4 Git软件结构

#### 1.4.1 四种状态和三个阶段

##### 1.4.1.1 三个阶段

`Git` 项目拥有三个阶段：工作区、暂存区以及 版本库。

```shell
$ tree -L 2 -a learning_git/

learning_git/
└── .git
    ├── HEAD
    ├── branches
    ├── config
    ├── description
    ├── hooks
    ├── info
    ├── objects
    └── refs

6 directories, 3 files
```

`.git`目录就是**Git版本库**（又叫仓库，`repository`）

`.git`版本库所在的目录根，被称为**工作区**，如  `learning_git`， `Git`的相关操作命令需要在工作区执行。

在工作区中进行代码编写，最后由版本库管理，其中要经过一个叫做暂存区的地方。暂存区本质是一个文件`.git/index`，保存了下次将要提交的文件列表信息，一般在 `Git` 仓库目录中。 按照 `Git` 的术语叫做“索引”，不过一般说法还是叫“暂存区”。

当项目下首次管理了某些文件时，`index`文件就会被创建，生成暂存区。

```shell
~/learning_git$ touch README.md
~/learning_git$ git add README.md
~/learning_git$ tree -L 2 -a

.
├── .git
│   ├── HEAD
│   ├── branches
│   ├── config
│   ├── description
│   ├── hooks
│   ├── index  # 生成了暂存区文件
│   ├── info
│   ├── objects
│   └── refs
└── README.md

6 directories, 5 files
```

三个阶段的相互关系为：

![Git三个阶段的相互关系](./res/001.jpg)

##### 1.4.1.2 四种状态

`Git`中文件通常有两种状态，既已跟踪文件和未跟踪文件，而已跟踪文件又可以分为三种状态，如下所示：

- 未跟踪文件
- 已跟踪文件
<<<<<<< HEAD
  - 已提交：已提交表示数据已经安全地保存在本地数据库中
  - 已修改：表示修改了文件，但还没保存到数据库中
  - 已暂存：表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中

这些状态又分别对应了git的三种区域，如下所示：
=======
  - 已提交：已提交表示数据已经安全地保存在版本库中
  - 已修改未暂存：表示修改了文件，但还没保存到版本库中
  - 已暂存：表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中
>>>>>>> 502455a... add markdown note

文件在`Git`中时刻处于这四种状态：

![Git结构](./res/002.png)

##### 1.4.1.3 使用Git命令的注意事项

在开始使用`Git`去管理项目时应当注意`Git`中相关的操作命令应该在工作目录下执行，因为当在`Git`工作区的某个子目录下执行操作的时候，会在工作区目录中依次向上递归查找`.git`目录，找不到`.git`目录时会产生报错。

比如在版本库下执行命令时就会提示错误。

```shell
~/learning_git/.git$ git status

fatal: this operation must be run in a work tree  # 错误信息
```

##### 1.4.1.4 提交版本库

**跟踪或者暂存文件**

- 使用命令 `git add` 开始跟踪一个文件，`git add` 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件；
- 是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等；

- 如刚才把`README.md`文件设为跟踪文件；

**提交文件**

- 提交暂存区文件到版本库可以使用 `git commit`命令；

- 可以在 `commit` 命令后添加 `-m` 选项，将提交信息与命令放在同一行，省略m参数的时候，git会使用默认编辑器打开一个文件，用于记录本次的提交信息，如果不对文件内容进行更改，直接退出，则认为放弃本次提交；

- 只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤；

```shell
# 现在我们将README.md文件提交到版本库
~/learning_git/.git$ git commit -m "init project and add READM"
```

#### 1.4.2 状态查看

##### 1.4.2.1 状态查看

整个的命令操作流程是基于`Git`的三个阶段的，文件在这三个阶段中分别有四种状态，`Git`通过`git status`命令显示工作目录和暂存区的状态。使用此命令能看到那些修改被暂存到了, 哪些没有, 哪些文件没有被`Git tracked`到。`git status`不显示已经`commit`到项目历史中去的信息。看项目历史的信息要使用`git log`。

```shell
# 创建项目时首次查看

~/learning_git$ git status

On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
        
# 提交README.md文件后再次查看
~/learning_git$ git status

On branch master
nothing to commit, working tree clean

# 此时向文件中添加新内容再次查看

~/learning_git$ echo "1" > README.md
~/learning_git$ git status

On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

> 通过`git status -uno`可以只列出所有已经被git管理的且被修改但没提交的文件。

##### 1.4.2.2 简洁模式

使用`git status -s` 命令或 `git status --short` 命令；

```shell
~/learning_git$ git status -s

 M README.md
```

- 新添加的未跟踪文件前面有 `??` 标记，
- 新添加到暂存区中的文件前面有 `A` 标记
- 修改过的文件前面有 `M` 标记
- 输出中有两栏，左栏指明了暂存区的状态，右栏指明了工作区的状态

#### 1.4.3 不纳入版本管理

一般我们总会有些文件无需纳入 `Git` 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以创建一个名为`.gitignore` 的文件，列出要忽略的文件的模式。

文件 `.gitignore` 的格式规范如下：

- 所有空行或者以 # 开头的行都会被 Git 忽略；
- 可以使用标准的 glob 模式匹配，它会递归地应用在整个工作区中；
- 匹配模式可以以（/）开头防止递归；
- 匹配模式可以以（/）结尾指定目录；
- 要忽略指定模式以外的文件或目录，可以在模式前加上叹号（!）取反；

```shell
# 忽略所有的 .a 文件
*.a

# 但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
!lib.a

# 只忽略当前目录下的 TODO 文件，而不忽略 subdir/TODO
/TODO

# 忽略任何目录下名为 build 的文件夹
build/

# 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
doc/*.txt

# 忽略 doc/ 目录及其所有子目录下的 .pdf 文件
doc/**/*.pdf
```

> 一个仓库可能只有根目录下有一个 .gitignore 文件，它递归地应用到整个仓库中。 然而，子目录下也可以有额外的 .gitignore 文件。子目录中的 .gitignore 文件中的规则只作用于它所在的目录中。

继续拿创建的学习项目进行举例，后续文档的命令默认在工作区的根下执行，将省略文件夹标识。

```shell
touch .gitignore

git status -s

# ------------------
 M README.md
?? .gitignore
# -------------------

echo ".*" > .gitignore
git status -s

# ---------------------
 M README.md  # 此时文件在工作区中修改，暂未提交到暂存区
# ---------------------
```

#### 1.4.4 文件对比

通过`git status`命令可以查看文件的实时状态，而通过 `git diff`命令， 可以实时的对比文件内容的实时变化。

```shell
git diff README.md

# -----------------------------------------
diff --git a/README.md b/README.md
index e69de29..d00491f 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+1
# ------------------------------------------

## 此时发现diff其实对比的是暂存区快照和工作区的差异

git add README.md
git status -s

# -------------------------------------------
M  README.md
# -------------------------------------------

git diff README.md

# -------------------------------------------
暂存区快照此时和工作区文件无差异，所以对比结果空
# -------------------------------------------

echo "2" >> README.md
git status -s

# -------------------------------------------
MM README.md
# -------------------------------------------

git diff README.md

# ---------------------------------------------
diff --git a/README.md b/README.md
index d00491f..1191247 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 1
+2
# ---------------------------------------------
```

此时本地文件包含1和2，暂存区文件包含1，版本库文件为空，可以用 `git diff --staged` （`cached`与`staged`等价）命令， 比对已暂存文件与最后一次提交的文件差异。

```shell
git diff --cached  README.md

# ------------------------------------------------
diff --git a/README.md b/README.md
index e69de29..d00491f 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+1
# ------------------------------------------------
```

在本书中，我们使用 git diff 来分析文件差异。 但是你也可以使用图形化的工具或外部 diff 工具来比较差异。 可以使用 git difftool 命令来调用 emerge 或 vimdiff 等软件（包括商业软件）输出 diff 的分析结果。 使用 git difftool --tool-help 命令来看你的系统支持哪些 Git Diff 插件。

#### 1.4.5 日志查看

`git log`命令在不传入任何参数的默认情况下，会按时间先后顺序列出所有的提交，最近的更新排在最上面。这个命令会列出每个提交的 `SHA-1` 校验和、作者的名字和电子邮件地址、提交时间以及提交说明。

```shell
git log

# ---------------------------------------------------
commit 385a7cee4e268102e12829d6b32f6156bc2d144a (HEAD -> master)
Author: achui <102549XXXX@qq.com>
Date:   Fri Feb 12 16:07:44 2021 +0800

    init project and add READM
# ---------------------------------------------------
```

使用选项` -p` 或 `--patch`会显示每次提交所引入的差异。



git log --oneline

git log -n4 # 查看最近的两次

git log -n2 --oneline  # 配合使用

git log --all

git log --all --graph

--stat 选项在每次提交的下面列出所有被修改过的文件、有多少文件被修改了以及被修改过的文件的哪些行被移除或是添加了。 在每次提交的最后还有一个总结


`Git`

非常有用的选项是 --pretty。 这个选项可以使用不同于默认格式的方式展示提交历史。 这个选项有一些内建的子选项供你使用。 比如 oneline 会将每个提交放在一行显示，在浏览大量的提交时非常有用。 另外还有 short，full 和 fuller 选项，它们展示信息的格式基本一致，但是详尽程度不一：





当 oneline 或 format 与另一个 log 选项 --graph 结合使用时尤其有用。 这个选项添加了一些 ASCII 字符串来形象地展示你的分支、合并历史：

git log -1 --pretty=raw



commit e695606fc5e31b2ff9038a48a3d363f4c21a3d86：这是本次提交的唯一标识。
·tree f58da9a820e3fd9d84ab2ca2f1b467ac265038f9：这是本次提交所对应的目录树。
·parent a0c641e92b10d8bcca1ed1bf84ca80340fdefee6：这是本地提交的父提交（上一次提交）。



| 序号 | 选项            | 说明                                                         |
| :--: | :-------------- | ------------------------------------------------------------ |
|  1   | `-p`            | 按补丁格式显示每个提交引入的差异                             |
|  2   | `--stat`        | 显示每次提交的文件修改统计信息                               |
|  3   | --shortstat     | 只显示 --stat 中最后的行数修改添加移除统计                   |
|  4   | --name-only     | 仅在提交信息后显示已修改的文件清单                           |
|  5   | --name-status   | 显示新增、修改、删除的文件清单                               |
|  6   | --abbrev-commit | 仅显示 SHA-1 校验和所有 40 个字符中的前几个字符              |
|  7   | --relative-date | 使用较短的相对时间而不是完整格式显示日期（比如“2 weeks ago”  |
|  8   | --graph         | 在日志旁以 ASCII 图形显示分支与合并历史                      |
|  9   | --pretty        | 使用其他格式显示历史提交信息。可用的选项包括 oneline、short、full、fuller 和 format（用来定义自己的格式） |

### 1.5 基本操作

#### 1.5.1 移除文件

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。 可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。

如果要删除之前修改过或已经放到暂存区的文件，则必须使用强制删除选项 `-f`（译注：即 force 的首字母）。

#### 1.6.6 移动文件

不像其它的 VCS 系统，Git 并不显式跟踪文件移动操作。 如果在 Git 中重命名了某个文件，仓库中存储的元数据并不会体现出这是一次改名操作。 不过 Git 非常聪明，它会推断出究竟发生了什么，至于具体是如何做到的，我们稍后再谈。

既然如此，当你看到 Git 的 `mv` 命令时一定会困惑不已。

##### 在当前工作区搜索内容

```shell
git grep "需要搜索的内容"
```



使用 git reset HEAD <file>... 来取消暂存。

## 2 Git基础操作

### 2.1 一个完整的git提交流程

`git add`命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。主要作用是将未跟踪的文件变为已跟踪文件，并提交缓存区，以及将当前修改的文件提交到缓存区。





git cat-file

`gitk`图形界面操作



git cat-file

#### 文件重命名

```shell
git mv source_file target_file
```

#### 版本历史查看

## 3 分支

使用分支意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。`Git`中操作分支速度非常快。



在创建初始化`Git`仓库的时候，`Git`会给我们默认建立一个分支`master`我们可以把他理解为主分支。一般的分支我们用`feature`为开头来进行命名，`bug`分支我们可以用`fix`开头来命名。所以这里就涉及到了分支如何分， 如何切换，如何合并，如何解决冲突等问题。



分支创建

```shell
git branch branch_name

git branch learning_git  # 创建学习git的分支
```

切换分支

```shell
git checkout branch_name
```



通常我们会在创建一个新分支后立即切换过去，这可以用 `git checkout -b <newbranchname>` 一条命令搞定





<<<<<<< HEAD

## 0 前言
=======
## 3 远程仓库管理

远程仓库是指托管在因特网或其他网络中的你的项目的版本库， 当然也可以托管在本机中，这里的远程指的是别处的意思。

较常使用的远程库：

- GitHub
- GitLab
- 码云

运行 `git remote` 命令。 它会列出你指定的每一个远程服务器的简写。 如果你已经克隆了自己的仓库，那么至少应该能看到 origin ——这是 Git 给你克隆的仓库服务器的默认名字：





就如刚才所见，从远程仓库中获得数据

这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。







##### 1.2.2.3 不带签名提交

`Git`默认不允许进行不带签名的提交， 但是可以使用参数开启允许`--allow-empty`，一把不建议这样做

```shell
# 1. 首先取消签名设置（这里假设没有设置仓库级签名）

git config --unset --global user.name
git config --unset --global user.email

# 2. 运行提交
 git commit -a -m "这是一次不带签名的提交"

# --------git提示无法进行提交
*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got '30678@DESKTOP-1IGKUKR.(none)')
# ---------------------------------------------------

# 3. 使用参数允许提交
 git commit --allow-empty -a -m "这是一次不带签名的提交"
```

### 编辑

·commit e695606fc5e31b2ff9038a48a3d363f4c21a3d86：这是本次提交的唯一标识。
·tree f58da9a820e3fd9d84ab2ca2f1b467ac265038f9：这是本次提交所对应的目录树。
·parent a0c641e92b10d8bcca1ed1bf84ca80340fdefee6：这是本地提交的父提交（上一次提交）。

`git cat-file`命令用于显示对象ID属于哪一种类型
>>>>>>> 502455a... add markdown note
