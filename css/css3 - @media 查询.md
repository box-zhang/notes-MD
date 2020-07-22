# css-@media 查询

随着市面上各种型号的终端产生，做适配类的网站也成了越来越多页面的制作趋势，实现多终端适配时，中必不可少的属性就是css3的@media screen属性，他可以根据浏览器宽度判断并输出不同的长宽值。

## @media是什么？如何使用？

先来了解一下官方对@media的定义吧：

> `@media `查询，你可以针对不同的媒体类型定义不同的样式，并根据不同的媒体类型查询出所对应的应用样式。
>
> @media 可以针对不同的屏幕尺寸设置不同的样式，特别是如果你需要设置设计响应式的页面，@media 是非常有用的。
>
> 当重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面。
>
> 注：媒体查询后即使查询返回false，附有媒体查询的样式表[仍然会下载](http://scottjehl.github.io/CSS-Download-Tests/)到[`<link>`]标签。但是，直到其查询结果变为真，否则其内容将不适用。

@media在 **css3** 中 **语法**（日常推荐写法）：

```css
/* @media在css3中的 语法，css中使用@media属性直接判断媒体类型时 须以@media开头*/
@media mediatype and|not|only (media feature) {
    /* CSS-Code; */
}
/* 或者通过 @import将单独的打印样式引入到css中 */
@import url(xxx.css) mediatype;	
```

 @media在 **css3** 中 **举例**：

```css
/* 当文档宽度小于 300 像素时，修改背景颜色 background-color 为 blue */
@media screen and (max-width: 300px) {
    body { background-color: blue; }
}
/* 当媒体类型为all时，表示所有设备都引入 body { background-color: blue; }*/
@media all {
    body { background-color: blue; }
}
/* 当媒体类型为print时，引入print.css */
@import url(print.css) print;	

/* 要注意的是：使用link标签要比使用@import规则性能更好。 */
```

@media在 **css2** 中**语法**：

```html
<!-- @media在css2中使用时，需要通过html的<link>里的medea属性来判断媒体类型 -->
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">

<!--或-->
<!--提示：如需在一个 style 元素中定义一个以上的媒介类型，请使用逗号分隔的列表（如：media="screen,projection"）。-->
<style type="text/css" media="screen,projection">
    ...
</style>
```

@media在 **css2** 中**举例**：

```html
<!-- 当文档宽度小于 300 像素时，引入样式mystylesheet.css，此种写法为css2的写法 -->
<link rel="stylesheet" media="screen and (max-width: 300px)" href="mystylesheet.css">

<!--当媒体类型为screen或projection时，使用该style里的样式-->
<style type="text/css" media="screen,projection">
    ...
</style>
```

**日常我们使用@media时，推荐css3写法，如遇兼容问题，可通过引入外部文件的方式进行处理（请见下文中介绍的：@media兼容性的考虑）。**

## 媒体类型（Media Type）

> `媒体类型`就是 `描述`设备的一般`类别`，即通过媒体类型`指定不同的样式`。
>
> 除非您使用`not`或`only`逻辑运算符，否则媒体类型是可选的，并且将隐含使用`all`类型。
>
> css3废弃了很多媒体类型，所有主流浏览器都支持 media 属性的` "screen"`、`"print" `以及 `"all"` 值。

- **all：适用于所有设备。**  **`（在 媒体查询 中如果没有明确指定Media Type，那么其默认为all）`**

  ```css
  @media all { ... }	/* @media all的使用方法 */
  ```

- **print：用于打印机和打印预览，设置打印机用字体尺寸等。**

  <sub>显示器(screen)和打印机(printer)是两种差别很大的设备，所以从浏览器里看到的页面，打印出来也许和你看到的样子有很大的差距。</sub>

  <sub>screen一般使用逻辑单位比如px，而打印机则应该使用物理单位比如cm或in。</sub>

- **screen：用于电脑屏幕，平板电脑，智能手机等**

- **speech：应用于屏幕阅读器等发声设备**

## @media 的常用实例

1. **max-with** （最大宽度值，即 <=）

   ```css
   /* 媒体类型小于或等于480px时 */
   @media screen and (max-width:480px){ ... }
   ```

2. **min-with** （最小宽度值，即 >=） 

   ```css
   /* 媒体类型大于或等于960px时 */
   @media screen and (min-width:960px){ ... }
   ```

3. **all** （适用于所有）

   ```css
   /* 在所有媒体类型下，浏览器宽度小于等于500px的时，使用{}里的样式 */
   @media all and (max-width: 500px) { ... } 
   ```

4. **and** （"and"关键词 将多个媒体特性结合在一起） 

   ```css
   /* 媒体类型在480px~960px之间时，使用{}里的样式 */
   @media screen and (min-width:480px) and (max-width:960px){ ... }
   
   ```

5. **Device Width** （设备屏幕的输出宽度，“max-device-width” “min-device-width” 指的是设备的实际分辨率，即可视面积分辨率。）

6. ```html
   <!--iphone.css适用于最大设备宽度为480px的设备中-->
   <link rel="stylesheet" media="screen and (max-device-width:480px)" href="iphone.css" />
   
   ```

7. **not**（“not”关键词 用来排除某种制定的媒体类型） 

   ```css
   /* 在 除打印设备 以及 设备宽度小于1200px下所有设备中，使用{}里的样式 */
   @media not print and (max-width: 1200px){ ... }
   
   ```

8. **only** （only用来指定某种特定的媒体类型，排除不支持媒体查询的浏览器）（媒体类型：Media Type）

   `其实only很多时候是用来对那些不支持 媒体查询 但却支持Media Type的设备隐藏样式表的`。

   - *支持* 媒体特性 的设备，正常调用样式，此时就当only不存在；
   - *不支持* 媒体特性 但又 *支持* Media Type 的设备，这样就会不读样式，因为其先会读取only而不是screen；
   - 不支持* 媒体查询 的浏览器，*不论是否支持*only，样式都不会被采用。  

   ```css
   /*用法*/
   @media only screen and (min-width:480px) and (max-width:960px){ ... }
   
   ```

9. **screen** （与打印样式有关）

   > 上面的代码几次用到了`screen` ，他的意思是在告知设备在*打印页面时*使用[衬线字体](http://baike.baidu.com/link?url=FOnnUbOa6X590ao9mYca7Rgz_z5bLBtmMV0qwimHDZIsaZFTC5vztLLlPvOnzCo5hGU5loIN9zhxJDBBRaQeTa)，在*屏幕上显示时*用无衬线字体。
   >
   > 当你的网站不需要考虑用户打印的样式问题时，可以省略`screen`。

## @media兼容性的考虑

pc端兼容：

![](https://user-gold-cdn.xitu.io/2019/3/5/1694b85356244f52?w=1834&h=398&f=png&s=73468)

移动端兼容：

![](https://user-gold-cdn.xitu.io/2019/3/5/1694b858682dfa81?w=1828&h=396&f=png&s=75929)

### 1、移动设备的兼容考虑（<meta>）

有了CSS的媒体查询这个功能，便有了所谓的响应式（例如bootstrap的响应式布局），那么设置<meta>也就成了必不可少的一部分。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no,shrink-to-fit=no">

```

content属性值如下，这些属性值主要用来处理可视区域。

| 值            | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| width         | 设置layout viewport 的宽度，为一个正整数，或字符串”device-width”（宽度等于当前设备的宽度） |
| initial-scale | 设置页面的**初始**缩放值，为一个数字，可以带小数（默认设置为1.0） |
| minimum-scale | 允许用户的最**小**缩放值，为一个数字，可以带小数（默认设置为1.0） |
| maximum-scale | 允许用户的最**大**缩放值，为一个数字，可以带小数（默认设置为1.0） |
| height        | 设置layout viewport 的高度，这个属性很少使用                 |
| user-scalable | 是否允许用户手动缩放，值为”no”或”yes”，no 代表不允许，yes代表允许（默认设置为no） |
| shrink-to-fit | 网页宽度自适应时，ios9的兼容解决办法                         |

> 下面一行代码可以让网页的宽度自动适应手机屏幕的宽度
>
> ```
> `<meta name=``"viewport"` `content=``"width=device-width,initial-scale=1"``>`
> 
> ```
>
> 但在IOS9中要想起作用，得加上"shrink-to-fit=no"，原因如下：
>
> ```
> `Viewport meta tags using``"width=device-width"` `cause the page to scale down to fit content that overflows the viewport bounds.``You can override ``this` `behavior by adding ``"shrink-to-fit=no"` `to your meta tag as shown below.``The added value will prevent the page from scaling to fit the viewport`
> 
> ```

### 2、低版本浏览器的兼容考虑

```html
<!--
html5shiv.js：解决ie9以下浏览器对html5新增标签的不识别，并导致CSS不起作用的问题。
respond.min.js：让不支持css3 Media Query的浏览器包括IE6-IE8等其他浏览器支持查询。
搜寻网址：https://www.bootcdn.cn/
-->
<!--[if lt IE 9]>
  <script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
  <script src="https://cdn.bootcss.com/html5shiv/r29/html5.min.js"></script>
<![endif]-->

```

### 3、设置IE渲染方式默认为最高(这部分可以选择添加也可以不添加)

IE 处处是陷阱，虽然大多人的IE浏览器版本都升级到了IE9以上，可IE9也并不十分友好，有可能它的文档模式却是IE8，为了防止这种情况，我们需要下面这段代码来让IE的文档模式永远都是最新的：

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge，chrome=1">

```

> chrome=1，这个[Google Chrome Frame（谷歌内嵌浏览器框架GCF）](http://zh.wikipedia.org/wiki/Google_Chrome_Frame)。
>
> 如果有的用户电脑里面装了这个chrome的插件，就可以让电脑里面的IE不管是哪个版本的都可以使用Webkit引擎及V8引擎进行排版及运算。
>
> 如果用户没装这个插件，那这段代码就会让IE以最高的文档模式展现效果。
>
> 也就是说：当浏览器为双核时，默认使用chrome内核。

## 常用的几种屏幕宽度设定

```css
/* 竖屏 */
@media screen and (orientation: portrait) and (max-width: 720px) { ... }

/* 横屏 */
@media screen and (orientation: landscape) { ... }

```



## @media使用要点

1. 使用**min-width**时，**小**的放**上**面，**大**的在**下**面，否则会出现样式覆盖的现象。
2. 使用**max-width**时，**大**的在**上**面，**小**的在**下**面，否则会出现样式覆盖的现象。



## 附：媒体功能

| 值                      | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| aspect-ratio            | 定义输出设备中的页面可见区域宽度与高度的比率                 |
| color                   | 定义输出设备每一组彩色原件的个数。如果不是彩色设备，则值等于0 |
| color-index             | 定义在输出设备的彩色查询表中的条目数。如果没有使用彩色查询表，则值等于0 |
| device-aspect-ratio     | 定义输出设备的屏幕可见宽度与高度的比率。                     |
| device-height           | 定义输出设备的屏幕可见高度。                                 |
| device-width            | 定义输出设备的屏幕可见宽度。                                 |
| grid                    | 用来查询输出设备是否使用栅格或点阵。                         |
| height                  | 定义输出设备中的页面可见区域高度。                           |
| max-aspect-ratio        | 定义输出设备的屏幕可见宽度与高度的最大比率。                 |
| max-color               | 定义输出设备每一组彩色原件的最大个数。                       |
| max-color-index         | 定义在输出设备的彩色查询表中的最大条目数。                   |
| max-device-aspect-ratio | 定义输出设备的屏幕可见宽度与高度的最大比率。                 |
| max-device-height       | 定义输出设备的屏幕可见的最大高度。                           |
| max-device-width        | 定义输出设备的屏幕最大可见宽度。                             |
| max-height              | 定义输出设备中的页面最大可见区域高度。                       |
| max-monochrome          | 定义在一个单色框架缓冲区中每像素包含的最大单色原件个数。     |
| max-resolution          | 定义设备的最大分辨率。                                       |
| max-width               | 定义输出设备中的页面最大可见区域宽度。                       |
| min-aspect-ratio        | 定义输出设备中的页面可见区域宽度与高度的最小比率。           |
| min-color               | 定义输出设备每一组彩色原件的最小个数。                       |
| min-color-index         | 定义在输出设备的彩色查询表中的最小条目数。                   |
| min-device-aspect-ratio | 定义输出设备的屏幕可见宽度与高度的最小比率。                 |
| min-device-width        | 定义输出设备的屏幕最小可见宽度。                             |
| min-device-height       | 定义输出设备的屏幕的最小可见高度。                           |
| min-height              | 定义输出设备中的页面最小可见区域高度。                       |
| min-monochrome          | 定义在一个单色框架缓冲区中每像素包含的最小单色原件个数       |
| min-resolution          | 定义设备的最小分辨率。                                       |
| min-width               | 定义输出设备中的页面最小可见区域宽度。                       |
| monochrome              | 定义在一个单色框架缓冲区中每像素包含的单色原件个数。如果不是单色设备，则值等于0 |
| orientation             | 定义输出设备中的页面可见区域高度是否大于或等于宽度。         |
| resolution              | 定义设备的分辨率。如：96dpi, 300dpi, 118dpcm                 |
| scan                    | 定义电视类设备的扫描工序。                                   |
| width                   | 定义输出设备中的页面可见区域宽度。                           |

## 参考

[@media 媒体类型 print 的使用](https://www.html.cn/archives/4731/)

[CSS3 @media 查询](http://www.runoob.com/cssref/css3-pr-mediaquery.html)