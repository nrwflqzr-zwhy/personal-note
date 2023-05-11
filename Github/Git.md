# Git

## 配置 Git

```shell
git --version #查看 git 版本
```

要配置Git，必须定义一些全局变量：`user.name`和 `user.email`。 这两者都是进行提交所必需的。

在 Cloud Shell 中，用以下命令设置你的名称。 将 `<USER_NAME>` 替换为要使用的用户名。

使用此命令创建 `user.email` 配置变量，并将 `<USER_EMAIL>` 替换为你的电子邮件地址：

```shell
git config --global user.name "<USER_NAME>"
git config --global user.email "<USER_EMAIL>"
```

运行以下命令以检查更改是否成功：

```shell
git config --list
```

确认输出包含类似以下示例的两行。 你的用户名和电子邮件地址将与示例中显示的内容不同。

```shell
user.name=User Name
user.email=user-name@contoso.com
```

## 设置Git存储库

Git 的工作方式是：检查特定文件夹内文件的更改。 我们会创建一个文件夹作为“工作树”（项目目录），并将其告知 Git，以便可以开始跟踪更改。 我们将 Git 存储库初始化到该文件夹中来告知 Git 开始跟踪更改。

首先为项目创建一个空文件夹，然后在该文件夹内初始化 Git 存储库。

1.   创建名为“Cats”的文件夹。 此文件夹将为项目目录（也称为“工作树”）。 项目目录是存储所有与项目有关的文件的位置。 在此练习中，它是存储你的网站和创建该网站的文件及其内容的位置。

     ```shell
     mkdir Cats
     ```

2.   使用 `cd` 命令切换到项目目录：

     ```bash
     cd Cats
     ```

3. 现在，初始化新存储库，并将默认分支的名称设置为 `main`：如果你运行的是 Git 版本 2.28.0 或更高版本，请使用以下命令：

     ```bash
     git init --initial-branch=main
     git init -b main
     ```

     对于 Git 的较早版本，请使用以下命令：

     ```bash
     git init
     git checkout -b main
     ```

     运行初始化命令后，应当会看到与以下示例类似的输出：

     ```shell
     Initialized empty Git repository in /home/<user>/Cats/.git/
     
     Switched to a new branch 'main'
     ```

4.   现在使用 `git status` 命令以显示工作树的状态：

     ```shell
     git status
     ```

     Git 用此输出进行响应，这表示 `master` 为当前分支。 （它也是唯一分支。）到目前为止，一切顺利。

     ```shell
     On branch master
     
     No commits yet
     
     nothing to commit (create/copy files and use "git add" to track)
     ```

5.   使用 `ls` 命令以显示工作树的内容：

     ```shell
     ls -a
     ```

     确认目录包含一个名为“.git”的子目录。 （将 `-a` 选项与 `ls` 结合使用非常重要，因为 Linux 通常会隐藏以句点开头的文件和目录名称。）此文件夹为 Git 存储库 - Git 用于存储工作树的元数据和历史记录的目录。

     你通常无需直接对“.git”目录执行任何操作。 在工作树的状态发生更改时，Git 会更新元数据，以跟踪文件中的更改。 此目录无需你执行任何操作，但它对于 Git 非常重要。

## 从Git获取帮助

与大多数命令行工具一样，Git 具有内置的帮助功能，可用于查找命令和关键字。

1.   键入以下命令，获取 Git 相关的操作帮助：

     ```shell
     git --help
     ```

2.   此命令显示以下输出：

     ```shell
     usage: git [--version] [--help] [-C <path>] [-c name=value]
            [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
            [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
            [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
            <command> [<args>]
     
     These are common Git commands used in various situations:
     
     start a working area (see also: git help tutorial)
        clone      Clone a repository into a new directory
        init       Create an empty Git repository or reinitialize an existing one
     
     work on the current change (see also: git help everyday)
        add        Add file contents to the index
        mv         Move or rename a file, a directory, or a symlink
        reset      Reset current HEAD to the specified state
        rm         Remove files from the working tree and from the index
     
     examine the history and state (see also: git help revisions)
        bisect     Use binary search to find the commit that introduced a bug
        grep       Print lines matching a pattern
        log        Show commit logs
        show       Show various types of objects
        status     Show the working tree status
     
     grow, mark and tweak your common history
        branch     List, create, or delete branches
        checkout   Switch branches or restore working tree files
        commit     Record changes to the repository
        diff       Show changes between commits, commit and working tree, etc
        merge      Join two or more development histories together
        rebase     Forward-port local commits to the updated upstream head
        tag        Create, list, delete or verify a tag object signed with GPG
     
     collaborate (see also: git help workflows)
        fetch      Download objects and refs from another repository
        pull       Fetch from and integrate with another repository or a local branch
        push       Update remote refs along with associated objects
     
     'git help -a' and 'git help -g' list available subcommands and some
     concept guides. See 'git help <command>' or 'git help <concept>'
     to read about a specific subcommand or concept.
     ```

     

# 基本 Git 命令

Git 的工作方式是记住对文件所做的更改，就像它对文件系统拍摄快照一样。

我们将介绍一些基本命令，用于开始跟踪存储库中的文件。 然后，你将保存 Git 的第一个“快照”以进行比较。

## git status

首先是最常用的 Git 命令 `git status`。 你在前面的练习中已使用过一次，目的是查看是否已正确初始化 Git 存储库。

`git status` 显示工作树的状态（以及暂存区域的状态 - 后文会对此详细介绍）。 利用它可查看 Git 当前正在跟踪哪些更改，以便决定是否指示 Git 再拍摄一个快照。

## git add

`git add` 命令用于指示 Git 开始跟踪某些文件中的更改。

此操作的技术术语是“暂存”这些更改。 你将使用 `git add` 来暂存更改以准备提交。 已添加但尚未提交的文件中的所有更改都存储在“暂存区域”中。

## git commit

暂存要提交的某些更改后，可以通过调用 `git commit` 命令将工作保存到快照。

“提交”是动词也是名词。 在“提交到计划”或“将更改提交到数据库”中，“提交”的含义本质上是相同的。作为动词，提交更改意味着将文件、目录或其他内容的副本作为新版本放置到存储库中。 作为名词，提交是一小部分数据，它为所提交的更改提供了唯一标识。保存在提交中的数据包括作者姓名和电子邮件地址、日期、有关所执行操作（以及原因）的注释、可选数字签名和先前提交的唯一标识符。

## git log

使用 `git log` 命令，可查看先前提交的相关信息。 每个提交都附加有一条消息（提交消息），`git log` 命令输出有关最新提交的信息，如其时间戳、作者和提交消息。 此命令有助于跟踪你执行的操作和已保存的更改。

## git help

尽管你已使用过 `git help` 命令，但还是应该提醒你。 利用此命令，可以轻松获取到目前为止已了解的所有命令的相关信息和其他命令信息。

请注意，每个命令均附带自己的帮助页。 可以通过键入 `git <command> --help` 找到这些帮助页。 例如，`git commit --help` 会调出一个页面，其中包含有关 `git commit` 命令及其使用方法的详细信息。

## 总结

恭喜！ 在本模块中，你已了解使用 Git 的基础知识。

你已了解：

-   版本控制系统 (VCS) 的概述
-   重要的 Git 术语。
-   Git 与 GitHub 之间的区别。
-   如何配置 Git。
-   一些基本 Git 命令。

你目前所掌握的 Git 相关知识已足够你针对基本项目自行使用版本控制。 版本控制的强大功能只有在与其他开发人员协作时才能明显显现。 有关与他人协作使用 Git 的详情，请查看本学习路径中的其他模块！

### 资源

如果要深入了解，请参阅以下资源：

-   运行 `git help tutorial` 和 `git help tutorial-2` 命令。
-   访问[每日 Git](https://git-scm.com/docs/everyday) 网站或使用 `git help everyday` 命令。
-   参阅 [Git 和 GitHub 学习资源](https://help.github.com/en/articles/git-and-github-learning-resources)。
-   观看 [Git 介绍回顾](https://www.youtube.com/watch?v=9uGS1ak_FGg%3Fazure-portal%3Dtrue)视频。
-   查看 [Git 官方网站](https://git-scm.com/)的[文档部分](https://git-scm.com/doc)。
