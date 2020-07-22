## 邮箱内嵌页面-表格高度均衡一致问题解决办法

> 由于邮件不支持javascript，link，flash、iframe以及一些特殊的标签，所以在表格行、列有变化的时候，表格高度也要随即调整，在页面尾部我添加了个计算表格高度的脚本，会通过控制台进行输出，因此编辑该页面的时候，需要查看console控制台来获取高度，并进行表格高度的添加。此表格一共分为三栏，上、左、右，3大板块，我们分别进行填充和获取。

具体做法如下：

- **步骤一：**

  打开页面到编辑器中，分别搜索 name="jobTop"、 name="jobLeft"和 name="jobRight"，会看到有很多个相同的标签在页面中。那么编辑规则是，每一个板块的`职位栏`所对应的`<td>`标签内都添加对应的name值，也就是` name="jobTop"、 name="jobLeft"和 name="jobRight"`。

  注意哦：<u>仅仅在职位栏的<td>标签内添加name标签，地区和部门所对应的<td>内不添加</u>。

  如图所示：

  ![image-20200616131444628](../../../Library/Application Support/typora-user-images/image-20200616131444628.png)



- **步骤二：**

  打开页面到浏览器中，点击键盘F12调出控制台/点击Console，会看到3行输出内容，分别是表格的上、左、右三大板块的职位总数和所需要的表格高度。

  如图所示：![image-20200616131825341](../../../Library/Application Support/typora-user-images/image-20200616131825341.png)



- **步骤三：**

  复制三个高度值，将所获得的像素值分别填入对应的<table>标签内，例如：320像素，对应 id="jobTop" 的 table，搜索 id="jobTop" 并在后面追加 height="360" 即可，以此类推，需要把 id="jobTop" 、 id="jobLeft" 、 id="jobRight" 三个表格都添加上对应的height值。

  如图所示：![image-20200616132344397](../../../Library/Application Support/typora-user-images/image-20200616132344397.png)

     ![image-20200616132640544](../../../Library/Application Support/typora-user-images/image-20200616132640544.png)

  ![image-20200616132535666](../../../Library/Application Support/typora-user-images/image-20200616132535666.png)



## 表格下方出现横切线问题

这个我多加了一个高度的输出项，如果再遇到刚才那种问题，是表格的总高度太高了，但是内容填充的高度比表格规定高度小导致的，所以你把我算出的这个值填在id=“box” 这个位置就行了。

同上面方法一致：打开页面到浏览器，点击键盘F12调出控制台/点击Console，会看到3行输出内容后面多了一行，这个就是整个页面的高度值，替换到id="box"的height里面即可。

![2641593764460_.pic_hd](../../../Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/f1d7c9cba3fdd495fa859a2d718b8a55/Message/MessageTemp/c79e1466888544e8f5aa2827d60a958f/Image/2641593764460_.pic_hd.jpg)

![2651593764509_.pic](../../../Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/2.0b4.0.9/f1d7c9cba3fdd495fa859a2d718b8a55/Message/MessageTemp/c79e1466888544e8f5aa2827d60a958f/Image/2651593764509_.pic.jpg)