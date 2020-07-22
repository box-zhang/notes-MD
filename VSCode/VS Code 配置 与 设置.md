# VS Code 配置 与 设置

## 用户设置&&工作空间设置

VS Code提供了两种设置方式： 
- `用户设置`（适合 个人偏好）： 这种方式进行的设置，会应用于该用户打开的所有工程； 

- `工作空间设置`（适合 多人项目时，设置的编码规范）：工作空间是指使用VS Code打开的某个文件夹，在该文件夹下会创建一个名为.vscode的隐藏文件夹，里面包含着**仅适用于当前目录的**VS Code的设置。工作空间的设置会覆盖用户的设置。

  `工作空间设置的文件`保存在当前目录的`.vscode`文件夹下。

##更改默认用户设置与工作空间设置
VS Code的设置文件为`setting.json`。

用户设置的文件保存在如下目录： 
- Window	 %APPDATA%\Code\User\settings.json 
- Mac  	$HOME/Library/Application Support/Code/User/settings.json 
- Linux 	$HOME/.config/Code/User/settings.json

工作空间设置的文件保存在当前目录的.vscode文件夹下。

所以有三种方式更改默认的设置： 
- 使用编辑器直接打开setting.json文件； 
- 点击 VS Code 的 文件 > 首选项 > 设置 ，可以打开设置面板； 
- 在 VS Code 中使用 Ctrl+Shift+P（Mac：cmd+shift+p）打开命令面板，输入Preferences: Open User Settings 或 Preferences: Open Workspace Settings。

## settings.json配置

~~~json
{
  "workbench.iconTheme": "material-icon-theme",
  // VScode主题配置
  "editor.tabSize": 2,
  "editor.lineHeight": 24,
  "editor.renderLineHighlight": "none",
  "editor.renderWhitespace": "none",
  // "editor.fontFamily": "Consolas",
  "editor.fontSize": 14,
  // "editor.cursorStyle": "block",
  // "editor.cursorBlinking": "smooth",
  "editor.renderIndentGuides": true,  // 控制编辑器是否显示缩进参考线。
  "editor.multiCursorModifier": "ctrlCmd", //多光标修改器
  "editor.formatOnSave": true, //保存时候自动格式化，如果同时设置了"files.autoSave": "autoSaveDelay",保存及格式化会失效。files.autoSave配置成别的选项即可。
  "editor.snippetSuggestions": "top",
  "editor.wordWrapColumn": 120,
  "editor.wordWrap": "off", //编辑器换行
  "editor.fontLigatures": true,
  "editor.minimap.enabled": false,  // 开启 vscode 文件路径导航
  "editor.quickSuggestions": {
    "other": true,
    "comments": true,
    "strings": false
  },
  // VScode 文件搜索区域配置
  "search.exclude": {
    "**/dist": true,
    "**/build": true,
    "**/elehukouben": true,
    "**/.git": true,
    "**/.gitignore": true,
    "**/.svn": true,
    "**/.DS_Store": true,
    "**/.idea": true,
    "**/.vscode": false,
    "**/yarn.lock": true,
    "**/tmp": true
  },
  "javascript.suggestionActions.enabled": false,
  "javascript.updateImportsOnFileMove.enabled": "always",
  "javascript.implicitProjectConfig.experimentalDecorators": true,
  "files.autoSave": "onFocusChange",
  // "[javascript]": {
  // "editor.formatOnSave": false,
  // },
  "beautify.language": {
    "js": {
      "type": ["javascript", "json"],
      "filename": [".jshintrc", ".jsbeautifyrc"]
      // "ext": ["js", "json"]
      // ^^ to set extensions to be beautified using the javascript beautifier
    },
    "css": ["css", "scss"],
    "html": ["htm", "html"]
  },
  "explorer.confirmDelete": false,
  "terminal.integrated.fontSize": 14,
  // "terminal.integrated.shell.windows": "C:\\windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
  // "Consolas, 'Courier New', monospace",
  // "terminal.integrated.fontFamily": "Consolas, 'Courier New', monospace",
  "terminal.integrated.cursorStyle": "underline",
  "workbench.startupEditor": "newUntitledFile",
  "workbench.colorCustomizations": {
    "terminal.foreground": "#5b874b",
    "tab.activeBackground": "#282c34",
    "activityBar.background": "#282c34",
    "sideBar.background": "#282c34"
  },
  "emmet.triggerExpansionOnTab": true, // 配置emmet是否启用tab展开缩写
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },
  //vue设置
  "vetur.format.defaultFormatter.html": "js-beautify-html",   //.vue文件template格式化支持，并使用js-beautify-html插件
  "vetur.format.defaultFormatterOptions": {   //js-beautify-html格式化配置，属性强制换行
    "js-beautify-html": {
      "wrap_attributes": "force-aligned"
    },
    "prettier": {   //vetur的格式化样式定制
      "printWidth": 100,
      "wrapAttributes": false,
      "sortAttributes": false
    }
  },
  "files.associations": { //根据文件后缀名定义vue文件类型
    "*.vue": "vue"
  },
  //eslint语法检查设置
  "eslint.enable": true,
  "eslint.autoFixOnSave": true, // 文件保存时，是否自动根据eslint进行格式化，自动修复错误
  "eslint.validate": [  //配置 ESLint 检查的文件类型
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact",
    {
      "language": "vue",
      "autoFix": true // 保存文件时，自动格式化
    },
    {
      "language": "html",
      "autoFix": true // 保存文件时，自动格式化
    }
  ],
  //prettier格式化设置
  "prettier.eslintIntegration": true, //开启 eslint 支持
  "prettier.singleQuote": true, //使用单引号
  "prettier.semi": false, //结尾不加分号
  "prettier.requireConfig": true,

  //VS Code 单独针对某种语言的设置，会覆盖外面定义的的公共设置
  "[typescript]": {
    "editor.formatOnPaste": true
  },
  "[markdown]": {
    "editor.wordWrap": "on",
    "editor.renderWhitespace": "all",
    "editor.acceptSuggestionOnEnter": "off"
  },

  //生成文件注释
  "docthis.authorName": "boxZhang",
  "workbench.colorTheme": "Material Theme"
}

~~~

## 其他设置

### 1. CPU100%

　　有时，vscode会出现CPU利用率100%的情况，两个rg.exe占用了全部的CPU。解决办法如下

　　文件>首选项>设置, 搜索设置 "search.followSymlinks" ：false；