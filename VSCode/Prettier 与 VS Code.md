# Prettier 与 VSCode

> [Prettier ](https://prettier.io/)是一个代码格式化工具，（支持大部分前端语言的处理，包括JavaScript、Flow、TypeScript、CSS、SCSS、Less、JSX、Vue、GraphQL、JSON、Markdown等的样式格式化）。它会删除代码里的原始样式，并根据其样式规则重新格式化代码，确保输出的代码风格一致。

##为什么要使用prettier格式化工具 

在多人项目中，大家每个人都有自己的代码习惯：运算符前后空格、大括号位置、行尾分号、缩进规则、代码块间空行等。。。风格的不一致，会导致一个项目中不同人接收过的模块有不同的代码格式，导致阅读、维护的困难。

以前，我们在格式化代码时，总是配置各种 ** link（css lint、html lint、javascript lint），减少大家输出不一致的风格代码，因此需要研究各种语言的配置，有了prettier，我们可以把多种语言的格式化集中在

## 与 ESLint 的差异

这是最常见的问题之一，简明的回答是 ESLint 只是一个代码质量工具 (确保没有未使用的变量、没有全局变量，等等)。`而 Prettier 只关心格式化`文件 (最大长度、混合标签和空格、引用样式等)，并不具有lint检查语法等能力。你可以将 ESLint 和 Prettier 结合起来使用，以获得双赢的组合。

## 安装Prettier

- 全局安装
  `npm install --global prettier`
- 局部安装
  `npm install --save-dev --save-exact prettier`

##如何自定义配置 Prettier

Prettier提供了一套默认的配置，那么如何修改配置项符合我们自己的代码规范呢，有三种方法可以做到

1. .prettierrc 文件（在项目中）

   ~~~javascript
   {
       "printWidth": 100,
       "parser": "flow"
   }
   ~~~

2. prettier.config.js 文件

   ~~~javascript
   module.exports = {
       tabWidth: 2,	// tab缩进大小,默认为2
       useTabs: true,	// 使用tab缩进，默认false
       semi: false,	// 句末加分号, 默认true
       singleQuote: true,	// 使用单引号, 默认false(在jsx中配置无效, 默认都是双引号)
   
       TrailingCooma: "none",	// 行尾逗号,默认none,可选 none|es5|all。（es5 包括es5中的数组、对象，all 包括函数对象等所有可选）
   
       bracketSpacing: true,	// 对象&数组是否追加空格 默认true。true: { foo: bar }	false: {foo: bar}
       // JSX标签闭合位置 默认false
       // false: <div
       //          className=""
       //          style={{}}
       //       >
       // true: <div
       //          className=""
       //          style={{}} >
       jsxBracketSameLine：false,
   
       arrowParens: 'always',	// 箭头函数参数括号 默认avoid 可选 avoid| always。（avoid 能省略括号的时候就省略 例如x => x。always 总是有括号。）
   }
   ~~~

3. package.json 中配置prettier属性

   ~~~javascript
   "scripts": {
      "precommit": "lint-staged",
      "lint-staged": {
       "*.{ts,js,css,json}": [
          "prettier --write", 
          "git add"
        ]
     }
   }
   ~~~

注意：

- VSCode中，需要安装 `Vetur`、`ESLint`、`Prettier - Code formatter`这三个插件，安装完重启下，防止插件不生效。

- 另外这里有个坑，VSCode中， `Beautify`插件会占用格式化代码的快捷键，因此会和`prettier`产生冲突，所以直接禁用掉。

- 一些全局配置可以在 VSCode 的setting中进行设置：点击文件->首选项->设置，在右侧用户设置添加。

  实际项目使用当中比较推荐用配置文件`.prettierrc`的方式进行针对性的配置，方便团队协作使用。 配置文件的选项可以参考官网：[prettier.io/docs/en/con…](https://link.juejin.im/?target=https%3A%2F%2Fprettier.io%2Fdocs%2Fen%2Fconfiguration.html)

  ```javascript
  {
    "editor.formatOnSave": true,	//自动保存，注意：如果同时设置了"files.autoSave": "autoSaveDelay",保存及格式化会失效。files.autoSave配置成别的选项即可。例如："files.autoSave": "onFocusChange"
    "prettier.eslintIntegration": true, //开启 eslint 支持
    "prettier.singleQuote": true, //使用单引号
    "prettier.semi": false, //结尾不加分号
    "prettier.requireConfig": true,
  }
  ```

- 如果项目配置了`.editorConfig`文件，在配置了`"editor.formatOnSave": true`后，如果项目成员没有安装 Prettier 插件，保存时就会读取`.editorConfig`文件，同样可以格式化代码。启用 Prettier 插件后，`.editorConfig`的配置就会失效，读取`.prettierrc` 文件的配置 

## Prettier 格式化快捷键

默认prettier快捷键是`alt + shift + f`（mac：cmd + shift + f）

## 使用prettier时遇到的问题

1. 在VSCode中，进行编辑react文件时，用prettier格式化，会出现格式错乱问题

   解决：修改VSCode下方的文件格式为javascript react格式（对比如下图）![image-20190318154130267](../../Library/Application Support/typora-user-images/image-20190318154130267.png)![image-20190318154158500](../../Library/Application Support/typora-user-images/image-20190318154158500.png)













