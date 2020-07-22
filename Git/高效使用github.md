## GitHub快捷键

- r          | 快速引用 ，打开issues，你可以选中别人的评论文字，然后按r，这些内容会以引用的形式被复制在文本框中：
  ![](https://user-gold-cdn.xitu.io/2019/5/17/16ac3a271466f609?w=600&h=275&f=gif&s=520522)

- t          | 搜索文件

- s          | 光标定位到搜索窗口

- w          | 选择分支

- `l`         | 键编辑 Issue 列表页的标签。

- `g n`           | Go to Notifications

- `g d`           | Go to Dashboard

- `g c`          |  Go to Code

- `g i`          |  Go to Issues

- `g p`           | Go to Pull Requests

- `g w`           | Go to Wiki

- ?          | 如果要查看所有的快捷键，可以在键盘上按下 ? 

- shift+/          | GitHub快捷键一览表

![](https://user-gold-cdn.xitu.io/2019/5/17/16ac3a32f2c1c83e?w=1636&h=1208&f=png&s=217191)

## 搜索

你是否也像我一样，在GitHub搜索栏，傻傻的输入自己想要检索的内容后按下回车键，然后再在GitHub的下方点击那些分类按钮，再次进行二次筛选呢？

![](https://user-gold-cdn.xitu.io/2019/5/17/16ac3a30a7194b74?w=2394&h=1308&f=png&s=342472)

一般的搜索类功能，都会有**高级检索**的功能，GitHub也不例外，有类似的功能，下面我们就一起学习一下如何高级而又高效的在GitHub中进行搜索吧。

### **awesome + xx ** 搜索

awesome这个单词表示的棒极了一类意思，GitHub上包含了各种swesome系列如果你在GitHub中搜索awesome  + xxx关键词，你就能搜索这个关键词的资源大全，例如：awesome react、awesome java、awesome linux。

你就会发现关于这些东西的学习资料真的是一大堆一大堆的。无论是书籍资源，库资源，还是学习视频、学习笔记，应有尽有。会了这个技能你再也不用到处求学习资源了。

### 关键词搜索

**明确搜索仓库标题、仓库描述、README……**

![](https://user-gold-cdn.xitu.io/2019/5/17/16ac3a520b2ea297?w=2436&h=928&f=png&s=209911)

- **in:name** 关键词          | 查找`仓库名`称包含 关键词 的仓库，可以使用语法

- **in:description** 关键词          |  查找描述包含 关键词 的仓库，可以使用语法

- **in:readme** 关键词          | 都会README文件包含 关键词 的项目
- **in:path 关键词**          | `路径`中包含关键词的代码
- **in:file 关键词**          | 文件中包含关键词的代码
- **in:file,path 关键词**          | 搜索路径中有 关键词 的代码或者文件中有 关键词 的代码

**通过目录结构搜索**

- **path:app/public language:javascript console**           | 在app/public directory目录下搜索console关键字的javascript代码
- **path:cgi-bin language:perl form **           | 搜索cgi-bin`目录`下包含form的perl代码

**通过文件名搜索**

- **filename:.vimrc commands**            |  搜索 `文件名`匹配 .vimrc 并且包含commands的代码

**通过扩展名来搜索**

- **icon size:>200000 extension:css **           |  搜索超过200kb包含icon的css代码

**明确搜索 star、fork 数大于多少的**

- **stars: >**100  关键字          | stars 大于100星的项目

- **stars: 10..20 **关键词          |  stars 在10-20颗星之间的项目

- **fork: >** 数字  关键字          | fork 数量大雨某个数字的项目

- **fork: 10..20 **关键词          |  fork 数量在10-20之间的项目

**明确搜索仓库大小的**

- **size:>=5000** 关键词          | 占用磁盘大于等于5000k的项目。这个数字代表K, 即5000代表着5M

**明确仓库是否还在更新维护**

- **pushed:>2019-01-03** 关键词          | 带有关键词，并且在2019.1.3`后`，还在更新维护的项目
- **created:>2019-01-03** 关键词          | 带有关键词，并且在2019.1.3`前`，还在更新维护的项目

**明确搜索仓库的 LICENSE（许可）**

- **license:apache-2.0** 关键词          | 要找包含关键字的协议是最为宽松的 Apache License 2 的代码，如果是其他协议，就更替apache-2.0为其他

**明确搜索仓库的语言**

- **language**:java  关键词          | 

**明确搜索某个人或组织的仓库**

- **user**:用户名          | 如果用户是个人，则用user:的方法查询
- **org**:组织名          | 如果用户是某个组织，则用org:的方法查询，就可以列出具体org 的仓库

**多个查询之间「空格」分隔**

- **user:json language:java 关键词**          | 搜索用户为json，包含某个关键词的java代码
- **in:path:cgi-bin language:perl form**           | 搜索cgi-bin目录下包含form的perl代码
- **android language:java fork:true**            | 搜索用java写的 android相关的代码并且被fork过

## 通过URL进行筛选和调整

### 去掉有关空白字符的改动

- 在任意 diff 页面的 UR L后加上 `?w=1`，可以去掉那些只是空白字符的改动，使你能更专注于代码改动。

### 调整 Tab 字符所代表的空格数

- 在 diff 或文件的 URL 后面加上 `?ts=4` ，这样当显示 tab 字符的长度时就会是 4 个空格的长度，不再是默认的 8 个空格。 

### 查看用户的全部 Commit 历史

在 Commits 页面 URL 后加上 `?author={user}` 查看用户全部的提交。

```
例如：
https://GitHub.com/rails/rails/commits/master?author=dhh
```

### 分枝

#### 查看分枝

在项目的url后面追加 **/branches**，你会看到一个包含所有未合并的分支的列表。在这里你可以访问分支比较页面或删除某个分支。

例如：https://github.com/{user}/{repo}/branches

![](https://user-gold-cdn.xitu.io/2019/5/17/16ac3a5b89e86ffe?w=2224&h=1342&f=png&s=309690)

#### 比较分支

在项目的url后面追加 **/compare/分支名1...分支2**，则在GitHub上会直接比较分枝1和分枝2这两个分支

```
https://github.com/{user}/{repo}/compare/{range}
```

其中 `{range} = master...patch-1`，例如：

```
https://github.com/{user}/{repo}/compare/master...dev1
```

`{range}` 参数还可以使用下面的形式:

```
https://github.com/{user}/{repo}/compare/master@{1.day.ago}...master
https://github.com/{user}/{repo}/compare/master@{2014-10-04}...master
```

*日期格式 YYYY-MM-DD*

### 整行高亮

在代码文件地址 URL 后加上`#L52`或者单击行号 52 都会将第 52 行代码高亮显示。

多行高亮也可以，比如用`#L53-L60`选择范围，或者按住 `shift` 键，然后再点击选择的两行。

```
https://github.com/{user}/{repo}/blob/master/activemodel/lib/active_model.rb#L53-L60
```



## 其他

[GitHub图标库](<https://octicons.github.com/>)

### GitHub 资源

| 内容          | 链接                            |
| ------------- | ------------------------------- |
| 探索 GitHub   | <https://github.com/explore>    |
| GitHub 博客   | <https://github.com/blog>       |
| GitHub 帮助   | <https://help.github.com/>      |
| GitHub 培训   | <http://training.github.com/>   |
| GitHub 开发者 | <https://developer.github.com/> |

#### GitHub 相关演讲视频

| 内容                                            | 链接                                          |
| ----------------------------------------------- | --------------------------------------------- |
| How GitHub Uses GitHub to Build GitHub          | <https://www.youtube.com/watch?v=qyz3jkOBbQY> |
| Introduction to Git with Scott Chacon of GitHub | <https://www.youtube.com/watch?v=ZDR433b0HJY> |
| How GitHub No Longer Works                      | <https://www.youtube.com/watch?v=gXD1ITW7iZI> |
| Git and GitHub Secrets                          | <https://www.youtube.com/watch?v=Foz9yvMkvlA> |
| More Git and GitHub Secrets                     | <https://www.youtube.com/watch?v=p50xsL-iVgU> |



------

本文摘自

[你真的会使用GitHub吗](<https://segmentfault.com/a/1190000008867338>)

[GitHub秘籍](<https://GitHub.com/tiimgreen/GitHub-cheat-sheet/blob/master/README.zh-cn.md>)