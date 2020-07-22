[TOC]

## Git与Github

介绍Git命令操作，必然要提及Github。

### GitHub介绍

> Github是一个基于git的代码托管平台，主要为开发者提供基于git仓库的版本托管服务，并提供一个web界面。
>
> Github 由Chris Wanstrath, PJ Hyett 与Tom Preston-Werner三位开发者在2008年4月创办。 总部位于美国旧金山。

### Git

> 简单介绍一下Git：
>
> Linux的创始人Linus Torvalds在2015年开发了Git的原型程序。
>
> Linux内核的更新速度在全世界也是首屈一指。
>
> Git 像是把数据看作是对小型文件系统的一组快照。 每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。 为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个 **快照流**。
>
> Git 有三种状态，你的文件可能处于其中之一：已提交（committed）、已修改（modified）和已暂存（staged）。 已提交表示数据已经安全的保存在本地数据库中。 已修改表示修改了文件，但还没保存到数据库中。 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
>
> 基本的 Git 工作流程如下：
>
> 1. 在工作目录中修改文件。
> 2. 暂存文件，将文件的快照放入暂存区域。
> 3. 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。
>
> [Git官方文档](<https://git-scm.com/book/zh/v2>)

### GitHub与Git的关联

- Git：开发者将源代码存入"Git仓库"的资料库中
- GitHub：是在网络上提供Git仓库的一项服务
- GitHub与Git的关联：GitHub上公开的软件源码是由Git进行管理，理解Git是熟练运用GitHub的关键所在

## Git的初始设置

### 查看用户名和邮箱地址

```
$ git config user.name
$ git config user.email
```

### 修改用户名和邮箱地址

```
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@example.com"
```

也可以通过git的配置文件"～/.gitconfig"进行修改

### 提高命令输出的可读性 （git 命令行显示呈现color 高亮）

```
$ git config --global color.ui auto
```

`$ git config --global color.ui auto` 这个命令相当于

```
$ git config --global color.diff auto
$ git config --global color.status auto
$ git config --global color.branch auto
$ git config --global color interactive auto
```

### 查看配置是否生效

```
$ git config --list
```

## 获取Git帮助

若你使用 Git 时需要获取帮助，有三种方法可以找到 Git 命令的使用手册：

```console
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```

例如，要想获得 config 命令的手册，执行

```console
$ git help config
```

## Git的命令操作

### 从Github上clone已有仓库

打开Github，打开需要拷贝的仓库链接，点击右侧按钮：Clone or download，获得一个git地址（例如：git@github.com:user-name/new-repository.git）

```
$ git clone git@github.com:user-name/new-repository.git
Cloning into 'new-repository'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.

$ cd new-repository
```

注意：这里会要求输入GitHub上设置的公开密钥的密码，认证后，仓库便会被clone到仓库名后的目录中，将想要公开的代码提交至这个仓库再push到GitHub的仓库中，代码便会被公开。

### Git基本操作

1. 进行`Git初始化`，会得到一个**.git**目录，这个.git目录里存储管理当前目录内容所需要的仓库数据，又叫**"附属于该仓库的工作树"**：`$ git init`

2. 查看本地Repository与哪些远程仓库建立了链接：`$ git remote -v`

3. 查看当前Git仓库的**状态**和**所在分支**：`$ git status`

4. 美化git status：`$ git status -sb` 

5. 提交代码（如果是add . 则说明是提交的所有改变过的文件，否则需要根据单独的文件名分别上传）：`$ git add .` 

6. **保存仓库的历史记录**（将当前暂存区的文件世纪保存到仓库的历史记录中，以便日后在工作树中复原文件），**记述一行提交信息**：`$ git commit -m "提交信息的概述"` 

7. 如果发现备注不够恰当，要修改上一条提交的备注信息：$ git commit \-\-amend

8. 如果想要**记录更详细的提交信息**，**请不要 -m**，直接使用`$ git commit` ，执行后，VI的编辑模式会自动启动，会看到：

   ```
   # Please enter the commit message for your changes. Lines starting
   # with '#' will be ignored, and an empty message aborts the commit.
   # On branch master
   #
   # Initial commit
   #
   # Changes to be committed:
   # (use "git rm --cached <file>..." to unstage) #
   # new file: README.md
   #
   ```

   在编辑器中记述提交信息的格式如下：

   第一行：用一行文字简述提交的更改内容

   第二行：空行

   第三行以后：记述更改的原因和详细内容

   如图所示：
   ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab144c82855458?w=1092&h=476&f=png&s=266074)

   编辑完成后，退出VI模式，`按esc`／`再打:wq`，保存并退出，然后再通过 $  git log 查看刚刚提交的记录

9. 查看提交信息：`$ git log`

10. 美化git log：`$ git log --all --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative`

   - 只显示第一行提交信息：`$ git log  \-\-pretty=short`
   - 只显示指定目录、文件的日志：`$ git log 某文件名`
   - 显示文件的改动，会对比文件的前后差别：`$ git log -p`
   - 显示具体文件的改动，会对比文件的前后差别：`$ git log -p 文件名` 


     ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab1463d13973e5?w=766&h=486&f=png&s=49880)查看文件的操作日志（可以看到操作版本的哈希值）：`$ git reflog`

11. 查看更改前后的差别（查看工作树、暂存区、最新提交之间的差别）：`$ git diff`

    其中：

    - "+"，表示新添加的行
    - "-"号，表示被删除的行

12. 查看工作树和最新提交的差别（养成好习惯，git commit之前先执行git diff HEAD）：`$ git diff HEAD`

13. 提交代码：`$ git push`

14. 通过master分支提交到远程：`$ git push -u origin "master"`

15. 查看所在分枝：`$ git`

16. 切换分枝：`$ git checkout \-\-master`'

17. 查看当前路径：$ pwd

### VI编辑模式命令

此处我们简单了解一下VI的几个命令，后面将会详细介绍VI环境的四种模式。

1. 进入插入模式（INSERT）：
   - `a 光标之后插入／ A 行尾插入`
   - `i 光标之前插入／ I 行首插入`
   - `o 下一行插入 ／O 上一行插入`
2. 进入命令模式（Command）：`：`
3. 保存文件并退出：`连按两次大写Z`
4. 保存不退出：`:w`
5. 系统退出VI，进入到shell模式：`:q`
6. 保存并退出：`:wq`
7. 不保存，强制退出：`:q!`

### Git分支操作

> 当进行多个并行作业时，我们会用到分枝。在这类并行开发的过程中，往往同时存在多个最新的代码状态。
>
> 不同分支中，可以同时进行完全不同的作业，等该分支的作业完成之后再与master分支合并。
> ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab1466c73d3659?w=766&h=486&f=png&s=49880)
> ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab1467f250dfe8?w=760&h=688&f=png&s=60081)

分支又分为：

- 特性分支Topic（完成特定任务的分支）
- 主干分支master

#### 分支相关命令：

1. 查看本地分支（带星号的为当前分支）：`$ git branch`

2. 查看远程仓库+本地仓库的分支信息：`$ git branch -a`

3. 创建并切换分枝：`$ git checkout -b 分支名`

4. 创建分枝：`$ git branch 分支名` 

5. 切换分枝：`$ git checkout 分支名` 

6. 切换回上一个分支：`$ git checkout -`

7. 合并分支：切换回master分支，`$ git merge  \-\-no-ff 需要合并的分支名`

   合并分支，需要各个分支先在各分支的领域里提交代码至远程仓库，而后由master分支对各个分支提交的内容进行合并。

8. 合并某分支到当前分支：`$ git merge <name>`

9. 显示合并到当前分支的分支列表：`$ git branch --merged`

10. 显示所有还没有合并到当前分支的分支列表：`$ git branch --no-merged`

11. 删除分枝：$ git branch -d <name>

12. 强制删除分枝：$ git branch -D <name>

13. **以图表形式查看分支**（可以看到各分支的合并状态，清楚明了）：`$ git log \-\-graph`

14. 回溯历史版本：`$ git reset`

15. 回溯到某个指定状态：$ git reset \-\-hard 哈希值

16. `查看当前仓库的操作日志（从日志中找到哈希值）`：`$ git reflog`

17. **消除冲突：**

    例如：

    > \# Git教程   
    >
    > <<<<<<< HEAD 
    >
    > 	- feature-A 
    >
    > \=\=\=\=\=\=\=
    > 	 \- fix-B 
    >
    > \>>>>>>> fix-B 

    =\=\=\=\=\=\=**以上**的部分是当前HEAD的内容，**以下**的部分是要合并的 fix-B 分支中的内容。

    实际开发过程中，往往需要删除其中之一，所以在处理时，需要仔细分析冲突部分再修改。

    解决冲突后，执行 \$ git add 与 \$ git commit 命令。

#### 更改提交的操作：

1. 修改已经提交了的备注信息（此处需要懂一些vim的相关命令常识）：`\$ git commit \-\-amend`

   执行 git commit \-\-amend 后，编辑器会启动，按`esc` 再按 `i` ，进入insert插入模式，修改好后，再点击`esc`，打`:x`，保存并退出。

   修改并保存退出后，执行`$ git log \-\-graph`命令，查看日志中的内容是否修改成功

2. **压缩提交历史：$ git rebase -i** 

   > 很多我们提交了例如 拼写错误等内容的修改，对于整个项目版本追溯的意义并不大，我们并不希望在历史记录中看到这类提交，因此可以选择使用合并历史提交记录的方式，将此记录与上一次有意义的提交记录合并为一次完美的提交
   >
   > 例如：git rebase -i HEAD-2
   >
   > 实际，git rebase -i HEAD-2 的作用是选定当前分支中包含HEAD在内的2个最新历史记录为对象，打开编辑器，进行备注信息的修改，修改完后保存并退出编辑器，再通过git log \-\-graph查看，会发现，哈希值已经不是原来的了。

3. 合并git add 和 git commit 这两个命令：`$ git commit -am '备注内容'`

4. 对比修改文件：`$ git diff`

#### 远程仓库的操作：

1. `添加远程仓库到本地`（执行git remote add后，git会自动将git@github.com:/…远程仓库的名称设置为origin（标识符））：

   ```
   $ git remote add origin git@github.com:user/new-repository.git
   ```

2. 推送至远程仓库：`$ git push -u origin master`

   > -u 参数可以在推送的同时，将origin仓库的master分支设置为本地仓库当前分支的upstream（上游）。
   >
   > 添加了这个参数，将来运行git pull命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从roigin的master分支获取内容，省去了另外添加参数的麻烦。

3. 推送master意外的分支：

   ```
   先切换到其他分支
   $ git checkout -b 分支名
   再从意境切换到的分支上进行推送
   $ git push -u origin 分支名
   ```

4. 获取远程仓库：`$ git clone git@github.com:...`

5. 查看当前分支信息（本地和远程origin）：$ git branch -a

   > -a 参数可以同时显示本地仓库和远程仓库的分支信息

6. 获取远程仓库的feature-D分支：$ git checkout -b feature-D origin/feature-D

7. 获取最新的远程仓库分支：$ git pull origin feature-D

## vi/vim的介绍及相关命令

vi/vim的介绍及相关命令请参考我的另一篇文章：[vim 小总结](<https://juejin.im/post/5cdb71675188252035420ce4>)

## Git资源及参考书籍

### Git 资源

| Title                                     | Link                                                      |
| ----------------------------------------- | --------------------------------------------------------- |
| Official Git Site                         | <http://git-scm.com/>                                     |
| Official Git Video Tutorials              | <http://git-scm.com/videos>                               |
| Code School Try Git                       | <http://try.github.com/>                                  |
| Introductory Reference & Tutorial for Git | <http://gitref.org/>                                      |
| Official Git Tutorial                     | <http://git-scm.com/docs/gittutorial>                     |
| Everyday Git                              | <http://git-scm.com/docs/everyday>                        |
| Git Immersion                             | <http://gitimmersion.com/>                                |
| Git for Computer Scientists               | <http://eagain.net/articles/git-for-computer-scientists/> |
| Git Magic                                 | <http://www-cs-students.stanford.edu/~blynn/gitmagic/>    |
| GitHub Training Kit                       | <http://training.github.com/kit>                          |
| Git Visualization Playground              | <http://onlywei.github.io/explain-git-with-d3/#freeplay>  |

#### Git 参考书籍

| Title                               | Link                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| Pragmatic Version Control Using Git | <http://www.pragprog.com/titles/tsgit/pragmatic-version-control-using-git> |
| Pro Git                             | <http://git-scm.com/book>                                    |
| Git Internals Pluralsight           | <https://github.com/pluralsight/git-internals-pdf>           |
| Git in the Trenches                 | <http://cbx33.github.com/gitt/>                              |
| Version Control with Git            | <http://www.amazon.com/Version-Control-Git-collaborative-development/dp/1449316387> |
| Pragmatic Guide to Git              | <http://www.pragprog.com/titles/pg_git/pragmatic-guide-to-git> |
| Git: Version Control for Everyone   | <http://www.packtpub.com/git-version-control-for-everyone/book> |



