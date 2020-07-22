# CSS3

###font-smoothing

功能：css3中用于设置字体的抗锯齿或者光滑度的属性

语法：font-smoothing: subpixel-antialiased	|	none	|	antialiased

- subpixel-antialiased  是浏览器默认属性
- none 用于小像素的文本
- antialiased 反锯齿

----

### transform:translate3d(0,0,0) 

transform:translate3d(x,y,z);定义x轴，y轴，z轴的位置

建议用3d，而不是2d，因为3d的变化可以开启移动端GPU硬件的加速

---

###backface-visibility

功能：定义氮元素不面向屏幕时，是否可见

语法：backface-visibility: visible	|	hidden;

- visiblie 背面是可见的
- hidden 背面是不可见的

------

###三角形

~~~css
// 三角形
.triangle:after {
  content: "";
 	width:0;
  height:0;
  overflow:hidden;
  border: 20px solid transparent;
  border-bottom-color: #821134;
}
~~~



------

### 超过两行显示省略号

~~~css
// 超过两行显示省略号
text-overflow: -o-ellipsis-lastline;
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
~~~

另有回答是通过jquery来实现的，下载Jquery插件：jQuery ellipsis plugin
调用方法：

~~~javascript
$(document).ready(function() {
　　$('.ellipsis').ellipsis();
}
~~~

-----



