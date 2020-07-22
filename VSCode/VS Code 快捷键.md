[TOC]

## VSCode快捷键

**1、注释**：

　　a) 单行注释：[ctrl+k,ctrl+c] 或 ctrl+/

　　b) 取消单行注释：[ctrl+k,ctrl+u] (按下ctrl不放，再按k + u)

　　c) 多行注释：[alt+shift+A]

　　d) 多行注释：/**

**2**、**移动行**：alt+up/down

**3、显示**/**隐藏左侧目录栏**  ctrl + b

**4**、**复制当前行**：shift + alt +up/down

**5**、**删除当前行**：shift + ctrl + k

**6**、**控制台终端显示与隐藏**：ctrl + ~

**7、查找文件/安装vs code** **插件地址**：ctrl + p

**8**、**代码格式化**：shift + alt +f

**9、新建一个窗口** : ctrl + shift + n

**10、行增加缩进:**  ctrl + [

**11、行减少缩进:**  ctrl + ]

**12、裁剪尾随空格(去掉一行的末尾那些没用的空格)** : ctrl + shift + x

**13、字体放大**/**缩小:**  ctrl + ( + 或 - )

**14、拆分编辑器 :**  ctrl + 1/2/3

**15、切换窗口** :  ctrl + shift + left/right

**16、关闭编辑器窗口** :  ctrl + w

**17、关闭所有窗口 :**  ctrl + k + w

**18、切换全屏 :**   F11

**19、自动换行** :  alt + z

**20、显示git**  :   ctrl + shift + g

**21、全局查找文件：**ctrl + shift + f

**22、显示相关插件的命令(如：git log)**：ctrl + shift + p

**23、选中文字**：shift + left / right / up / down

**24、折叠代码**： ctrl + k + 0-9 (0是完全折叠)

**25、展开代码**： ctrl + k + j (完全展开代码)

**26、删除行** ： ctrl + shift + k 

**27、快速切换主题**：ctrl + k / ctrl + t

**28、快速回到顶部** ： ctrl + home

**29、快速回到底部** : ctrl + end

**30、格式化选定代码** ：ctrl + k / ctrl +f

**31、选中代码 ：** shift + 鼠标左键

**32、多行同时添加内容（光标） ：**ctrl + alt + up/down

**33、全局替换：**ctrl + shift + h

**34、当前文件替换：**ctrl + h

**35、打开最近打开的文件：**ctrl + r

**36、打开新的命令窗：**ctrl + shift + c



##VSCode插件

### HTML／CSS

1. HTML Hint   |    html代码检测

2. HTML Snippets    |    H5代码片段以及提示

3. HTML CSS Support    |    让 html 标签上写class 智能提示当前项目所支持的样式的名字

4. Atuo Rename Tag    |    修改 html 标签，自动帮你完成尾部闭合标签的同步修改

5. css peek    |    可以追踪至样式表中 CSS 类和 ids 定义的地方。

   使用：鼠标在html中经过样式／cmd+点击样式／出现样式框进行查阅和更改

6. HTML Boilerplate    |    为 HTML 新文件重新编写头部和正文标签

   **使用：**输入 html，并按 Tab 键

7. color info    |    提供你在 CSS 中使用颜色的相关信息。你只需在颜色上悬停光标，就可以预览色块中色彩模型的（HEX、 RGB、HSL 和 CMYK）相关信息了。

8. Icon Fonts    |    能够在项目中添加图标字体的插件。该插件支持超过 20 个热门的图标集，包括了 Font Awesome、Ionicons、Glyphicons 和 Material Design Icons。

9. **language-stylus**     |    CSS预处理器styl后缀文件的识别扩展

### JS

1. jQuery Code Snippets    |    jQuery代码片段以及提示

2. Document this    |    js 的注释模板 （注意：最新版的vscode已经原生支持）

   使用：Ctrl+Alt+D` and again `Ctrl+Alt+D

3. fileheader    |    顶部注释模板，可定义作者、时间等信息，并会自动更新最后修改时间

4. Quokka    |  Quokka 是一个调试工具插件，能够根据你正在编写的代码提供实时反馈。

   **使用**：先shift+cmd+p （ctrl+shift+p）输入 quokka 选择 new javascript 就行了  

5. Faker    |    JavaScript 库 – Faker，能够帮你快速的插入用例数据。Faker 可以随机生成姓名、地址、图像、电话号码，或者经典的乱数假文段落，并且每个类别还包含了各种子类别，你可以根据自身的需求来使用这些数据。

### 综合

1. Path Intellisense    |    自动路劲补全，默认不带这个功能的。

2. Eslint    |    ESlint 接管原生 js 提示，可以自定制提示规则。语法检查。

3. Project Manager    |    在多个项目之前快速切换的工具

4. beautify    |    格式化代码的工具

5. Prettier    |    代码格式化程序。如果你还想使用 ESLint，那么还有个 Prettier – Eslint 插件，你可不要错过咯

   使用：默认快捷键是**alt + shift + f**

6. filesize    |    在底部状态栏显示当前文件大小，点击后还可以看到详细创建、修改时间

7. Minify    |    用于压缩合并 JavaScript 和 CSS 文件的应用程。

8. Open-In-Browser    |    提供直接在浏览器中打开文件的内置界面。

   使用：鼠标放在想要在浏览器打开的文件上／右键／open in default browser

9. Code Spell Checker    |    代码拼写检查

10. TODO Height    |    标注功能，如你写到某一部分的代码时，其中部分的功能需要稍后再来实现，这是就可以在对应的代码处添加一个 TODO 类型的注释。

   使用：`TODO: ` `FIXME:`

11. **markdownlint**     |    书写md文件的预览插件

### 服务

1. Npm Intellisense    |    require 时的包提示，（最新版的vscode已经集成此功能）
2. **Code Runner**    |      node，python等代码不必开命令行即可运行

### Git

- **Git History**     |    git提交历史
- **GitLens**     |    在代码中显示每一行代码的提交历史

### 框架

- **React Native Tools**     |    添加对 React Native项目的支持，快速书写es6以及jsx
- **Vetur**     |    添加对.vue后缀文件的快速书写支持。
- **Vue 2 Snippets**     |    快速新建vue页面（参考我另一篇文章）

### 调试

1. Debugger for Chrome    |    让 vscode 映射 chrome 的 debug功能，静态页面都可以用 vscode 来打断点调试。
2. 

### 

### SERVICE





