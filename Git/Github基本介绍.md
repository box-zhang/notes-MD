[TOC]

## 什么是SVN／Git／Github

在介绍Github之前，我们一起了解一下SVN、Git、Github这三个概念、分别的责任以及相关联的区别。

### SVN

> SVN（Subversion）是集中式管理的版本控制器。
>
> SVN只有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。
>
> 集中式版本控制系统最大的问题就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟。
> ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab149f4b570882?w=1394&h=960&f=png&s=191517)

### Git

> Git是分布式管理的版本控制器。
>
> 简单介绍一下Git：
>
> Linux的创始人Linus Torvalds在2015年开发了Git的原型程序。Linux内核的更新速度在全世界也是首屈一指。
>
> Git 像是把数据看作是对小型文件系统的一组快照。 每次你提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。 为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个 **快照流**。
>
> Git每一个终端都是一个仓库，客户端并不只提取最新版本的文件快照，而是把原始的代码仓库完整地镜像下来。每一次的提取操作，实际上都是一次对代码仓库的完整备份。
>
> Git 有三种状态，你的文件可能处于其中之一：已提交（committed）、已修改（modified）和已暂存（staged）。 已提交表示数据已经安全的保存在本地数据库中。 已修改表示修改了文件，但还没保存到数据库中。 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
>
> 基本的 Git 工作流程如下：
>
> 1. 在工作目录中修改文件。
> 2. 暂存文件，将文件的快照放入暂存区域。
> 3. 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。
>
> 分布式版本控制系统通常也有一台充当``“中央服务器”``的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。
>
> [Git官方文档](<https://git-scm.com/book/zh/v2>)
> ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab14a80792d40a?w=1110&h=1276&f=png&s=213552)

### Github

> Github是一个基于Git的代码托管平台，主要为开发者提供基于Git仓库的版本托管服务，并提供一个web界面。
>
> Github的付费用户可以建私人仓库，免费用户只能使用公共仓库，也就是代码要公开。
>
> Github 由Chris Wanstrath, PJ Hyett 与Tom Preston-Werner三位开发者在2008年4月创办。 总部位于美国旧金山。
>
> GitHub最大的特征："面向人"。
>
> - GitHub 与以往的仓库管理服务最大的不同，就在于它以人为中心，以往的仓库托管都是以项目为中心，每个项目就是一个信息封闭的世界。

------

### SVN与Git的区别

版本管理系统分为Subversion这种集中型和Git这种分散型。

- Git是分布式的，而SVN是集中式的
- Git没有一个全局版本号，而SVN有
- Git把内容按元数据方式存储，而SVN是按文件
- Git下载下来后，在OffLine状态下可以看到所有的Log，SVN不可以。
- 版本库（repository)：SVN只能有一个指定中央版本库。当这个中央版本库有问题时，所有工作成员都一起瘫痪直到版本库维修完毕或者新的版本库设立完成。而 Git可以有无限个版本库。或者，更正确的说法，每一个Git都是一个版本库，区别是它们是否拥有活跃目录（Git Working Tree）。如果主要版本库发生了什么事，工作成员仍然可以在自己的本地版本库（local repository）提交，等待主要版本库恢复即可。工作成员也可以提交到其他的版本库。
- 提交（Commit）上的不同：在SVN，当你提交时，它将直接记录到中央版本库。当发现提交的内容存在严重问题时，已经无法阻止事情的发生了。如果网路中断，则无法提交。而Git的提交完全属于本地版本库的活动。只需push到主要版本库即可，相当于在执行“同步”（Sync）。

### GitHub与Git的区别

- Git：开发者将源代码存入“Git仓库”的资料库中
- GitHub：是在网络上提供“Git仓库”的一项服务
- GitHub与Git的关联：GitHub上公开的软件源码是由Git进行管理，理解Git是熟练运用GitHub的关键所在

## GitHub使用前的准备

### 1. 创建账户

### 2. 设置头像

### 3.设置SSH Key

> GitHub上，连接已有仓库时的认证，是通过使用SSH的公开密钥认证方式进行的。

- `创建SSH Key：`

```
$ ssh-keygen -t rsa -C "【此处填写创建github时的邮箱，例如your_email@example.com】" 
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):【此处按回车键】
Enter passphrase (empty for no passphrase): 【此处输入密码】
Enter same passphrase again:【此处再次输入密码】
```

- 输入密码后，会出现如下结果，其中 `id_rsa文件是私有密钥， id_rsa.pub是公开密钥` 

```
Your identification has been saved in /Users/your_user_directory/.ssh/id_rsa. 
Your public key has been saved in /Users/your_user_directory/.ssh/id_rsa.pub. 
The key fingerprint is:
fingerprint  your_email@example.com 
The key's randomart image is:
 +--[ RSA 2048]----+ 
 | .+ + | 
 | =oO. |
 【略】
```

### 4. 添加公开密钥

在GitHub中添加公开密钥，今后就可以用私有密钥进行认证了。

- 打开GitHub／头像／settings／SSH and GPG Keys／New SSH Key
  ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab14c81b2e4fc5?w=1584&h=722&f=png&s=251328)

`New SSH Key`后，会要求输入Title和Key：

- Title中请输入适当的密钥名称

- Key部分请粘贴 **id_rsa.pub 公开密钥** 文件里的内容，其中获取 **id_rsa.pub 公开密钥**的方式如下：

  ```
  $ cat ~/.ssh/id_rsa.pub
  ```

  会得到以下形式的内容：
  ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab14e99b536281?w=1528&h=260&f=png&s=376746)

- 添加成功后，创建账户时，该邮箱会接到一封"公共密钥添加完成"的邮件。

### 5. 添加私人密钥

只有公开密钥添加完成后，才可添加私人密钥，通过私人密钥与GitHub进行认证和通信。

```
$ ssh -T git@github.com
The authenticity of host 'github.com (207.97.227.239)' can't be established. RSA key fingerprint is fingerprint  .
Are you sure you want to continue connecting (yes/no)?   yes
```

得到以下结果，即为成功：

```
Hi hirocastest! You've successfully authenticated, but GitHub does not provide shell access.
```

### 6. 使用社区功能

Follow  

Watch

## 创建仓库 new repository

### 创建一个公开仓库

右上角的➕／New repository

填写如下内容

- Repository name：填写仓库名称

- Description：填写仓库说明

- Public、Private：公开仓库Public内所有内容会被公开，选择Private则为创建非公开仓库，用户可以设置访问权限，但需要收费。

- Initialize this repository with a README：用README文件初始化仓库，打上勾以后，让用户可以立刻clone这个仓库。如果想向GitHub添加手中已有的Git仓库，建议不要勾选，直接手动push。

- Add .gitignore：

  > Add .gitignore这个下拉菜单很方便，通过它可以在舒适化时，自动生成Add .gitignore文件（这个文件用来描述Git仓库中不需要管理的文件与目录）。
  >
  > 这个设定会帮我们把不需要在Git仓库中进行版本管理的文件记录在Add .gitignore文件中，省去了每次根据框架进行设置的麻烦。

- Add a license：

  > Add a license菜单可以选择要添加的许可协议文件。如果这个仓库中包含的代码已经确定了许可协议，那么请在这里进行选择。

都填充和选择完后，点击Create repository，完成仓库的创建。

### 链接仓库

- 新建仓库的链接：https://github.com/用户名/仓库名
- README.md：初始化时就已经生成，一般用来描述本仓库所包含软件的概要、使用流程、许可协议等信息。
- GitHub Flavored Markdown：GitHub上的文档都可以用Markdown语法编写，而GitHub Flavored Markdown是GitHub在Markdown语法的基础上扩充而来的。

### 公开代码

- clone已有仓库

  打开需要拷贝的仓库链接，点击右侧按钮：Clone or download，获得一个git地址（例如：git@github.com:user-name/new-repository.git）

  ```
  $ git clone git@github.com:user-name/new-repository.git
  Cloning into 'new-repository'...
  remote: Enumerating objects: 3, done.
  remote: Counting objects: 100% (3/3), done.
  remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
  Receiving objects: 100% (3/3), done.
  
  $ cd new-repository
  ```

  ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab14f62a94068c?w=1112&h=562&f=png&s=92353)

  注意：这里会要求输入GitHub上设置的公开密钥的密码，认证后，仓库便会被clone到仓库名后的目录中，将想要公开的代码提交至这个仓库再push到GitHub的仓库中，代码便会被公开。

- 几个常用的`git命令`如下：

  1. 创建文件夹：`$ mkdir 文件夹名字`
  2. 进入文件夹：`$ cd 文件夹名字`

## Git的命令操作

### Git基本操作

本地仓库链接Github远程仓库时，内容上的推送和拉取，必要通过git操作命令来完成。

[请查看我的另一篇关于git基本操作的文章](<https://juejin.im/post/5cd967326fb9a031ee3c3272>)

## GitHub提供的主要功能

### GitHub快捷键 shift+/

打开GitHub快捷键一览表的方式：shift+/
![](https://user-gold-cdn.xitu.io/2019/5/13/16ab1501ec72196b?w=2042&h=1098&f=png&s=242047)



1. **Git仓库**

   > 我们可以免费建立任意个GitHub提供的Git仓库（但是如果需要创建私有仓库，则需要花钱）。

2. **Organization 组织、团体**

   > 一般我们只用个人账户就够了，如果是公司，建议使用Organization账户（要花钱），优点是可以统一管理账户和全县。

   如果只是用公开仓库，是可以免费创建Organization账户的。

3. **Issue**

   > Issue功能，是将一个任务或问题分配给一个Issue进行追踪和管理的功能。
   >
   > 管理issue的系统称为BTS（Bug Tracking System，BUG跟踪系统）。
   >
   > 遇到以下情况时，可使用Issue功能：
   >
   > - 发现软件的bug并报告
   > - 有事想向作者询问、探讨
   > - 事先列出今后准备实施的任务

   > 每个功能更改或修正都对应一个Issue，讨论或修正都以这个Issue为中心进行，发布一个Issue，就类似发布了一个话题，大家都可以围绕这个话题进行讨论。只要查看Issue，就能知道所有和这个更改相关的内容，以此进行管理。
   >
   > 如果别人对你的项目发起了一个Issue，你会通过邮件收到提醒前去查阅即可。

4. **Wiki**

   > wiki功能，任何人都能随时对一篇文章进行更改并保存，因此可以多人共同完成一篇文章。
   >
   > 常用此功能来编写开发文档或手册。
   >
   > wiki页也是作为Git仓库进行管理的，可以记录各个修改版本。

5. **Pull Request**

   > 开发者向GitHub的仓库推送更改或功能添加后，可以通过Pull Request功能向别人的仓库提出申请，请求对方合并。是GitHub的核心功能。
   >
   > GitHub提供了对Pull Request和源代码前后差别进行讨论的功能，可以让程序员更高效的交流。
   >
   > 在Pull Request页面能够查看当前处于Open状态的Pull Request。
   >
   > 如果你想要以.diff或者.patch格式文件的形式来处理Pull Reques，可以在URL末尾添加.diff或.patch，例如：
   >
   > https://github.com/userName/requestName/pull/28.diff
   >
   > https://github.com/userName/requestName/pull/28.patch

   

## GitHub界面基本介绍

### 顶部工具栏

![](https://user-gold-cdn.xitu.io/2019/5/13/16ab150cc0d185db?w=2530&h=136&f=png&s=42959)

#### 1. LOGO

#### 2. Search 搜索窗口

> 除了 Trending ，还有一种最主动的获取开源项目的方式，那就是 GitHub 的 Search 功能。

#### 3. Pull requests 发起请求

> Pull requests 是指开发者在本地对源代码进行更改后，向GitHub中托管的Git仓库请求合并的功能。
>
> 功能：
>
> 1. 开发者可以在Pull requests上通过评论进行交流，例如："我试着做了这样一个新功能，可以合并一下吗"等。
>
> Pull requests 这个功能，开发者可以轻松更改源代码，并公开细节，然后向仓库提交合并请求，仓库的创建者选择性的对其进行合并。
>
> 2. Pull requests 可以查看源代码的前后差别

#### 4. Issues 事物卡片

> 任务管理和 BUG 报告可以通过 Issue 进行交互。
>
> - 在团队协作中，每个 issue 可以代表一个任务，Product Owner 为每一个人的每一项任务创建一个issue，由组员自行管理关于自己的issue
> - 每一个issue被分配有不同的标签，分为：
>   - new tasks
>   - user story
>   - working on
>   - waiting for checking
>   - pass checking
>   - pass tests
>   - task completed
>
> 每名成员动态调整标签，组长检查所有带有waiting for checking的标签，完成检查后标记为pass checking. 通过测试后标记为pass tests
>
> - 在project中建立一个新项目，通过看板管理所有的issues，组员动态拖动关于自己的issues，组长定期查看。
>
> 如果你是项目的维护者，github还支持你如下的操作：
>
> - 将一个issue分配给参与者
> - 为一个issue打上标签
> - 将一个issue添加到项目的看板
> - 为一个issue关联到某个里程碑 
>
> github还支持您为仓库中或者是pull request中的特定代码行添加issue 

#### 5. Marketplace 集市

向开发者提供工具改进和定制工作流，是一个购买和发现应用的市场。

- [LogRocket](https://github.com/marketplace/logrocket) 可以让您重播问题，就像在自己的浏览器中发生的那样。 LogRocket不是猜测为什么发生错误或向用户询问屏幕截图和日志，而是为您提供了用户看到的视频记录，以及控制台日志，网络请求和应用程序状态，以便您可以快速找出出错的内容。 

#### 6. Explore 优秀项目集中在此

> Explore GitHub 会把所有近期有活跃的项目呈现给大家，是没有经过筛选的，按照默认排序。
>
> 例如：
>
> - **Trending，潮流热门趋势**的意思。这页里有一些热门的开源项目，GitHub就通过这个页面，做了筛选功能，是大家主动获取一些开源项目最好的途径，可以选择[当天热门]、[一周内热门]、[一月内热门]。也可以通过语言分类来查找想要学习的编程语言，例如你想看最近热门的ios项目，可以选择Objective-C语言
>
> 浩如烟海的库中，如何知道哪些语言有哪些优秀的库，有哪些优秀的开发者，github官方贴心出品，这里[Trending repositories on GitHub today · GitHub](https://github.com/trending) 并且一天固定时间更新一波。

#### 7. 铃铛🔔 Notifications

铃铛旁边蓝色的点提示用户是否有新的通知。（默认设置中，用户在GitHub收到通知会同时发送到该账户的注册邮箱）

#### 8. 加号➕ Create a new...

创建新的Git仓库，或Organization，向Organization添加成员、小组、仓库，为仓库添加Issue或collaborator等操作的残带都聚集在这里。

#### 9. 头像

用户设置（个人信息、安全管理、付费方案等）

### 仓库（Repository）的功能介绍

> Repository，仓库，存放自己或别人创建的开源项目，也就是如果你想要在Github上创建一个开源项目用来存放代码，必须创建一个Repository，如果你的开源项目多了，你就会拥有多个Repositories

![](https://user-gold-cdn.xitu.io/2019/5/13/16ab1516adbe42ae?w=2294&h=1194&f=png&s=280499)

#### 1. 用户名／仓库名

#### 2. Watch／Star／Fork

> watch:
>
> watch翻译过来可以称之为观察，点击watch可以看到如下的列表。
>
> 如果Watch了某仓库，今后该仓库的更新信息会显示在用户的公开活动中，用户可以追踪仓库的内容。
>
> 默认每一个用户都是处于Unwatch的状态，当你选择Watching，表示你以后会关注这个项目的所有动态，以后只要这个项目发生变动，如被别人提交了pull request、被别人发起了issue或者issue里面有新的讨论等等情况，你都会在自己的个人通知中心，收到一条通知消息，如果你设置了个人邮箱，那么你的邮箱也可能收到相应的邮件。
>
> 所以，`watch要谨慎使用，不然你的邮箱会被垃圾邮件占满`。如果你不想接受这些通知，那么点击 Not Watching 即可。
>
> 另外这里有一篇文章讲 [如何正确接收 GitHub 的消息邮件](https://github.com/cssmagic/blog/issues/49)，很不错的一篇文章，推荐大家看看。

> star：
>
> Star 表示给这个仓库加星的人数，数量越高，代表该仓库越受关注。star更像是书签，可以在user里面的Your stars中查看到自己标记了的star仓库列表。
>
> 相比朋友圈的点赞，github 里面会有一个列表，专门收集了你所有 star 过的项目，点击 github 个人头像，可以看到 your star的条目，点击就可以查看你 star 过的所有项目了。
>
> 不过，在你的 star 列表很容易出现这样的问题。就是你可能 star 成百上千个项目怎么办？
>
> 这时，如果 github 可以提供一个分类功能该多好，就像微博网页版的收藏，你在`收藏的时候可以设置 tag`，这样设置的好处是，以后再次查找项目时，可以根据归类查找，但是不知道 github 的产品经理是怎么想的。
>

> **fork：**
>
> GitHub中Fork 即是 **服务端的代码仓库克隆**（即 新克隆出来的代码仓库在远程服务端），包含了原来的仓库（即upstream repository，上游仓库）所有内容，如分支、Tag、提交。
>
> 这样有了一个你**自己的**可以自由提交的远程仓库，然后可以通过的 **Pull Request** 把你的提交**贡献回** 原仓库。而对于原仓库Owner来说，鼓励别人Fork自己的仓库，通过Pull Request 给自己的仓库**做贡献**，也能提高了自己仓库的**知名度**。
>
> 当选择 fork，相当于你自己有了一份原项目的拷贝，当然这个拷贝只是针对当时的项目文件，如果后续原项目文件发生改变，你必须通过其他的方式去同步。
>
> fork后面的数字代表该仓库被Fork到各用户仓库的次数，数越大，表示参与这个仓库开发的人越多。
>
> 一般来说，我们不需要使用 fork 这个功能，除非有一些项目，可能存在 bug 或者可以继续优化的地方，`你想帮助原项目作者去完善这个项目，那么你可以 fork 一份项目下来，然后自己对这个项目进行修改完善，当你觉得项目没问题了，你就可以尝试发起 pull request给原项目作者了，然后就静静等待他的 merge。`
>
> 我看到很多人**错误的在使用 fork**。很多人把 fork 当成了收藏一样的功能，每次看到一个好的项目就先 fork，因为这样，就可以我的 repository(仓库)列表下查看 fork 的项目了。其实完全可以使用 star 来达到这个目的。
>
> fork区别于clone：
>
> 1. Fork他的仓库：这是GitHub操作，这个操作会复制Joe的仓库（包括文件，提交历史，issues，和其余一些东西）。复制后的仓库在你自己的GitHub帐号下。目前，你本地计算机对这个仓库没有任何操作。
> 2. Clone你的仓库：这是Git操作。使用该操作让你发送"请给我发一份我仓库的复制文件"的命令给GitHub。现在这个仓库就会存储在你本地计算机上。做一些 bug fix。
>
> 相关文章：
>
> <https://linux.cn/article-4292-1-rss.html>
>
> [forking工作流](<https://github.com/oldratlee/translations/blob/master/git-workflows-and-tutorials/workflow-forking.md>)
>
> 

#### 3.Code：

> 显示仓库的文件列表，仓库名下方是该仓库的简单说明和URL。

#### 4.Issues：

> 用于bug报告、功能添加、方向性讨论等，将这些以Issue形式进行管理。Pull Requests时也会创建Issue。旁边显示的数字是当前处于Open状态的Issue数。

#### 5.Pull requests：

> Pull Request 是用户修改代码后向对方仓库发送采纳请求的功能，是`GitHub的核心功能`。代码的更改和讨论都在这里进行，旁边的数字表示尚未关闭的Pull Request的数量。
>
> - Conversation
>
> 在Conversation标签页中，可以查看与当前Pull Request相关的所有评论，以及提交历史。
>
> 小功能：想要引用别人的评论，可以选中当前评论，按R键，被选择的部分会自动以评论语法写入评论文本框。
>
> ![](https://user-gold-cdn.xitu.io/2019/5/13/16ab151dca3ce9e6?w=812&h=528&f=png&s=118878)
>
> - Commits
>
> Pull Request里面的commits标签页中，按时间顺序显示了与当前Puss Request相关的提交。标签上的数字为提交的次数。
>
> - Checks
> - Files Changed 
>
> Files Changed标签页中，可以查看当前Pull Request更改的文件内容以及前后差别。数字表示新建及被更改的文件数。
>
> 相关文章：
>
> [pull request 操作](<https://blog.csdn.net/qq_33429968/article/details/62219783>)
>
> [pull reqesut 的整个流程](https://www.zhihu.com/question/21682976)

#### 6.Projects

> GitHub的项目管理模式

#### 7.Wiki：

> wiki 是一种比HTML语法更简单的页面描述功能。常用于记录开发者之间应该共享的信息活着软件文档。
>
> 所有人都可以对文章进行修改，所以比较适合多人共同编写文章的情况。很适合用来针对更新频率较高的软件进行文档等信息方面的汇总。

#### 8.Insights

![](https://user-gold-cdn.xitu.io/2019/5/13/16ab15262ccd7c11?w=2234&h=966&f=png&s=186140)

> 洞察：
> Pulse：体现该仓库软件开发活跃度的功能。该仓库中的软件是 无人问津，还是在火热的开发之中，从这里可以一目了然。
> Graphs：以图表形式显示该仓库的各项指标。让用户轻松了解该仓库的活动倾向。
>
> - Pulse：体现该仓库软件开发活跃度的功能，近期该仓库创建了多少Pull Request 或 Issue，有多少人参与了这个仓库的开发等，都在这里一目了然
>   - Active Pull Requests：通过特定期间内活动过的Pull Request数量
>   - Active Issues：特定期间内活动过的issue数
>   - commits：commits显示与提交相关的信息
>     - 编写过代码的人数 
>     - 提交的次数
>     - default branch 中修改过的文件数
>     - default branch 中添加／删除的行数 
> - Contributors：每个用户在相应的日期中发送提交、添加代码、删除代码的大致数量。能够了解到该仓库的代码主要由哪些人编写。
> - Traffic：
> - Commits：显示一年内每周收到的提交的大致数量。
> - Code Frequency：显示了该仓库中代码行数的增／删量。
> - Dependence graph：
> - Network：以图表形式显示包括克隆仓库在内的所有分支的提交。从图上可以直观的看出每个人做了多少工作。
> - Forks：

#### 9.Settings

> 更改当前仓库的设置，用户必须拥有更改设置的权限才能看到这个菜单。

#### 10.Create new file

> 可以在当前仓库的路径下新建文件。新建文件作为一个新的提交记录在Fork出的分支中。
> 如果用户对该仓库拥有足够权限，该项则显示为Create a new file，用户可以直接在当前路径下新建文件。

#### 11.Upload files

> 上传文件到GitHub的仓库。

#### 12.Find File

> 可以查看当前分支的文件。

#### 13.Clone or download

> 以SSH协议／HTTPS协议下载该仓库；
>
> Open in Desktop 启动GitHub客户端 并进行下载；
>
> 通过浏览器等下载仓库的ZIP包

#### 14.项目相关信息

- a、 commits

  commits 查看当前分支的提交历史。左侧数字表示提交数。

- b、 branches

  branches 查看仓库的分支列表。数字表示当前拥有的分支数。

- c、 releases

  releases 显示仓库的标签（Tag）列表，可以将标签加入时的文件以归档（.zip、tar.gz）形式下载到本地。

  软件在版本升级时，一般都会打标签，如果需要特定版本的文件，从这里寻找。

- d、environment

- e、contributors

  显示对该仓库进行过提交的程序员名单。

  如果你对该仓库发送过Pull Request并且被采纳，那么在这里就能找到自己的名字。数字表示程序员人数。

- f、branch

  显示当前分支的名称，从这里可以切换仓库内分枝，查看其他分支的文件。

- g、new pull request

- h、files

  files里面可以查看当前分支的文件，以及READEME文件。

### 文件的相关操作

点开文件后，会显示文件的内容，同时也会显示一些作用于文件的菜单。

#### Raw

直接在浏览器中显示该文件的内容。

#### Blame

按行显示最新提交的信息。打开以后，左侧为commit时候的提交备注，右侧为当次提交时修改的内容。

#### History

查看该文件的历史记录

#### 本地查看／编辑／删除

#### 通过部分名称搜索文件

> 进入仓库页面后，按下键盘t键，然后输入要找的目录货文件的部分名称，筛选器会在仓库的目录和文件中进行筛选。

#### 查看差别的方法 ：在URL的仓库名后加 /compare/条件

1. 查看分支间的差别

   例如：要查看master和patch-1这两个分支之间的差别，可以在URL末尾这样写：

   https://github.com/user/project/compare/`master...patch-1`

2. 查看与几天前的差别

   例如：要查看master分枝在最近7天内的差别，可以在URL末尾这样写：

   https://github.com/user/project/compare/`master@{7.day.ago}...master`

3. 查看与指定日期之间的差别

   例如：要查看master分枝2019年1月1日与现在的区别，可以在URL末尾这样写：

   https://github.com/user/project/compare/`master@{2019-01-01}...master`

## 高效使用Github

### Github快捷键

