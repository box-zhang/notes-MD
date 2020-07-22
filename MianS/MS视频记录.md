[toc]

## 准备

1. 职位描述（JD）分析（判断自己的能力是否可以胜任，以及自己需要做的准备）

   - 去看他们的招聘公告

   - PC/H5的前端开发：PC端和移动端的技术栈是不一样的

   - 调试接口：mock数据是最基本的技能

   - 组件库的建立：对原生js/css的理解、之前是否有前端组件库的编写经验、是否通读过其他的UI组件库

   - 系统的优化与重构：可以回答对现在公司的系统的优化和重构的技术和步骤

   

   任职要求：

   - 面向对象的编程方法、组件化的编程（真正的组件化思想是离不开面向对象的）

   - 一定要准备一个项目的架构分析和模式：目录结构、复用性、模块化、自动化测试等
   - 笔试的回答要让代码体现易读、易维护、高质量、高效率
   - 体现出自己学习能力和追求新知的欲望，能说出一些即可
   - 准备一些技术博客的知识点
   - 熟悉web构建工具，Grunt、Gulp，能够自己搭建前端构建环境（重点看一下gulp，然后看一下grunt和gulp的构建区别，告诉人家你为什么要用gulp而忽略grunt）

   - 动画相关的技术：canvas、svg、transition（css3）、animation（css3）、css3哪些属性可以做cup加速的

   - ES6是js的最新标准

   - 对可用性、可访问性等相关知识有实际的了解和实践，如何捕获js异常（例如js的资源加载的错误、js运行异常的捕获）

     

2. 业务分析或实战模拟

   有时候理论知识丰富，但是实战经验单薄，会导致

   - 如何提升网站性能：DNS预解析
   - 图标字体制作
   - jquery处理大片dom片段，要借助于模版引擎：hanldlebars、template
   - vue写页面的时候，template直接塞页面就可以了，可以直接渲染
   - jquery的：事件委托、事件代理、延迟的方法、ajax

   

3. 技术栈准备

   每个公司的技术栈使用不同，有的用vue，有的用react等等

   - jquery的源码：核心架构
   - vueJS、react、anuglar，MVVM框架（vue1源码还是比较简洁的，vue2涉及到了很多ssr方面的东西以及静态语法类型检查的东西，读起来不太容易）
   - nodeJS：如果不会就不要写在简历里面
   - sass、less是预编译语言，gulp、grunt是打包工具，npm，webpack（必看）

4. 自我介绍

   - 简历：姓名、年龄、手机、邮箱、籍贯，不用写自我介绍，画蛇添足，简历里面的内容一定要有回答的准备
   - 学历：
   - 工作经历：时间-公司-岗位-职责-技术栈-业绩
   - 开源项目、github和说明

   自我陈述：

   - 把握面试的沟通方向
   - 豁达、自信的适度发挥



## DOM事件

### DOM事件的级别（DOM定义标准的一个级别）

1. DOM 0: element.onclick = function(){}

2. DOM 2: element.addEventListener('click',  function(){}, false); 

   DOM2中，最后的false还是ture，其实是指定了这个响应函数是冒泡还是捕获

   没有DOM1，是因为DOM1标准没有涉及事件相关的改变

3. DOM 3: element.addEventListener('keyup',  function(){}, false)

   DOM3中，添加了很多事件类型，例如：鼠标事件、键盘事件等等

### DOM事件模型

- 冒泡：从下往上，从当前元素也就是目标元素往上。element.addEventListener('click',  function(){}, false); 
- 捕获：从上往下。element.addEventListener('click',  function(){}, true); 

### DOM事件流

事件流：就是浏览器在为当前页面与用户做交互的过程中，比如我点击了点击鼠标左键，这个左键怎么传到页面上的

事件流的完整阶段：事件通过捕获到达目标元素，这个是捕获的过程。再从目标元素上传到window对象，也就是冒泡的过程

![image-20200616135331612](../../../Library/Application Support/typora-user-images/image-20200616135331612.png)

![image-20200616135937279](../../../Library/Application Support/typora-user-images/image-20200616135937279.png)

### DOM事件捕获的具体流程

![image-20200616140424266](../../../Library/Application Support/typora-user-images/image-20200616140424266.png)

### Event对象的常见应用

enevt是dom事响应中中非常重要的一个对象，例如想要拿到用户到底集中的是哪个键，想要拿到这种类似的所有东西基本都是从event对象获取到的。

- event.preventDefault()    阻止默认事件，例如：a标签，给a标签绑定了一个click事件，那么在响应函数中，如果设置了preventDefault() ，就阻止了链接一个默认跳转的行为。
- event.stopPropagation()    阻止冒泡，有时候业务不需要冒泡，例如子元素有一个点击，父元素有一个点击事件，想让子元素单击时候做一件事情，父元素单击时候做一件事情，如果不阻止冒泡，单击了子元素范围的时候，按照冒泡规则，父元素也会随之被响应。
- event.stopImmediatePropagation()    比如一个按钮绑定了两个click事件，第一个响应是a事件，第二个响应是b事件，我想通过优先级的方式，先响应a，再响应b，想在a点击的时候，不要再执行b，如果在a的响应函数中中加入这样一个方法，就会阻止b事件的执行
- event.currentTarget    面试经常考察，currentTarget表示当前所绑定的事件。
- event.target    面试经常考察，一个for循环给一个dom注册了n个事件，问要怎么优化。其实就是为了让你用事件代理，把所有的子元素的事件代理转移到父元素上，只绑定一次click事件就可以了。然后做响应的时候，就要判断是哪个子元素做的点击，那么怎么获取这个被点击的元素呢，这时候就需要target上场了。target表示当前被点击的元素

### 自定义事件（或者叫模拟事件 new Event()）

自定义事件的使用场景：现在有一个按钮，不是一个常规的click按钮，想自己增加一个事件，在别的地方触发这个事件，而不是用回调的方式处理，这时候就需要自定义事件。

通过document.dispatchEvent(eve);来触发执行这个事件

![image-20200616162939507](../../../Library/Application Support/typora-user-images/image-20200616162939507.png)



## HTTP协议类

### HTTP协议的主要特点

1. 简单快速：访问什么输入url就可以了
2. 灵活：在每个http头部协议，都会有一个数据类型，通过一个http协议就可以完成不同数据类型的一个传输
3. 无连接：我连接一次，就会自己断开
4. 无状态：客户端与服务端是两种身份，但从http协议上是没有办法区分你的身份的

### HTTP报文的组成部分

1. 请求报文：
   - 请求行：http方法（get/post），页面地址，http协议，版本
   - 请求头：key value值
   - 空行：
   - 请求体：数据部分
2. 响应报文：
   - 状态行：http方法（get/post），页面地址，http协议，版本
   - 响应头：key value值
   - 空行
   - 响应体：数据部分

### HTTP方法

1. get——获取资源
2. post——传输资源
3. put——更新资源
4. delete——删除资源
5. head——获得报文首部

### POST和GET的区别

1. 传送方式：baiget通过地址栏传输，post通过报文传输。

2. 传送长度：get参数有长度限制（受限于url长度），而post无限制

3. GET和POST还有一个重大区别，简单的说：GET产生一个TCP数据包；POST产生两个TCP数据包

   长的说：对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；
   而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。
   也就是说，GET只需要汽车跑一趟就把货送到了，而POST得跑两趟，第一趟，先去和服务器打个招呼“嗨，我等下要送一批货来，你们打开门迎接我”，然后再回头把货送过去。

4. √ GET在浏览器回退时是无害的，而POST会再次提交请求。
5. GET产生的URL地址可以被Bookmark，而POST不可以。
6. √ GET请求会被浏览器主动缓存，而POST不会，除非手动设置。
7. GET请求只能进行url编码，而POST支持多种编码方式。
8. √ GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
9. √ GET请求在URL中传送的参数是有长度限制的，而POST么有。如果get请求中url中的参数很长，会被浏览器截断，导致数据传输不全
10. 对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
11. √ GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
12. √ GET参数通过URL传递，POST放在Request body中。

### HTTP状态码

1. 1xx：指示信息——表示请求已接收，急需处理
   - 100：[客户端](https://baike.baidu.com/item/客户端)应当继续发送请求。
   - 101：服务器已经理解了客户端的请求，并将通过Upgrade 消息头通知客户端采用不同的协议来完成这个请求。
   - 102：由WebDAV（RFC 2518）扩展的状态码，代表处理将被继续执行。
2. 2xx：成功——表示请求已经被成功接收
   - 200：请求成功
   - 206：客户发送了一个带有range头的get请求，服务器完成了它。一般情况，当你发送一个video或者redio的很大的视频或音频文件给服务器时，他会返回206
3. 3xx：重定向——要完成请求必须进行更进一步的操作
   - 301：所有的请求页面已经转移到新的url，永久重定向
   - 302：所有请求页面已经临时转移到了新的url，临时重定向
   - 304：客户端有缓冲的文档并发出了一个条件性的请求，服务器告诉客户，原来缓冲的文档还可以继续使用。
4. 4xx：客户端错误——请求有语法错误或请求无法实现
   - 403：被请求资源禁止被访问
   - 404：请求资源不存在
5. 5xx：服务器错误——服务器未能实现合法的请求
   - 500：服务器错误
   - 503：服务器宕机，过载

### HTTP协议持久连接

http协议采用“请求-应答”模式，并且http支持持久连接。

当使用普通模式时，每个请求/应答客户和服务器都要新建立一个连接，完成之后立即断开连接（http协议本身是无连接的协议）

当使用Keep-Alive模式（又称持久连接、连接重用）时，Keep-Alive功能使客户端到服务器端的连接持续有效，当出现对服务器的后记请求时，Keep-Alive功能避免了建立或者重新建立连接。

###HTTP协议管线化

管线化机制通过持久连接完成，仅http/1.1支持此技术

get和head请求可以进行管线化，而post则有所限制

由于服务端问题，开启管线化并不会为性能做出很大的贡献，而且很多服务端和代理程序对管线化的支持并不好，所以现在浏览器默认并未开启管线化

![image-20200616172310059](../../../Library/Application Support/typora-user-images/image-20200616172310059.png)

## 原型链

  ### 创建对象的几种方法

~~~javascript
//字面量方法
var o1 = {name: 'o1'};   //字面量的时候，会默认这个对象的原型链指向object
var o2 = new Object({name:'o2'});		//new Object，new一个Object构造函数

//new方法，显示的构造函数来创建对象
var M = function(name){this.name=name}
var o3 = new M('o3');

//Object.create 方法创建
var P={name:"P"};
var o4 = Object.create(P);

~~~

### 原型、构造函数、实例、原型链

[原型链](https://juejin.im/post/5c765cdce51d453f4142d25a)

构造函数可以通过new 这个构造函数，生成一个实例。

任何函数都可以当作构造函数，只要被new，就会变成构造函数。

所有函数都有prototype属性，这是声明这个函数的时候，js引擎会自动给这个函数加上的这个属性，这个属性会初始化一个空对象，也就是原型对象。

原型对象中，怎么来区分是被哪一个构造函数所引用呢。原型对象中会有一个构造器constructor，他会告诉我们谁是自己的的构造函数。

 ① `__proto__`和`constructor`属性是`对象所独有`的；（原型对象、实例对象、函数对象，万物皆对象）

 ② `prototype`属性是`函数所独有`的。

![image-20200616193712721](../../../Library/Application Support/typora-user-images/image-20200616193712721.png)

原型链：

把一个实例对象，往上找构造这个实例相关联的对象（构造函数），然后再往上找创造这个实例对象的对象的关联对象，以此类推，一直到object.prototype，那么这时候，这个链条就断了。

也就是说，object.prototype这个属性是整个原型链的顶端，到这里终止，那么原型链是通过什么实现向上找的这个过程呢？就是通过prototype和\_ \_proto\_ \_这个属性实现的。

~~~javascript
//new方法，显示的构造函数来创建对象
var M = function(name){this.name=name}
var o3 = new M('o3');

M.prototype===o3.__proto__;	//true ｜ o3的__proto__和M的prototype 完全一致，说明M是o3的构造函数
Function.prototype === M.__proto__;	//true｜ M的__proto__和Function的prototype 完全一致，说明Function是M的构造函数，M自身也是一个实例对象，可以往上追溯自己的构造函数
M.prototype.__proto__===Object.prototype;	//true
~~~

原型链的应用场景：

原型对象和原型链之间到底是起了一个什么样的作用呢？

如果我的构造函数中多了很多属性和方法，那么是不是我的实例就可以共用这个东西，当多个实例要共同都拥有一个方法的时候，不可能所有的实例都拷贝一份构造函数，那么这个时候就要考虑将共用的方法加到一个共同的东西上，这个共同的东西就是原型对象。

~~~javascript
//new方法，显示的构造函数来创建对象
var M = function(name){this.name=name}
var o3 = new M('o3');

//通过原型链增加共用的方法
M.prototype.say = function(){
  console.log("say hi")
}

var o5 = new M("o5");

//打印
console.log(o3.say,o3.name);	//say hi,o3
console.log(o5.say,o5.name);	//say hi,o5

~~~

### instanceof的原理

instanceof的原理就是来判断，实例对象的\_ \_proto\_ \_和构造函数的prototype是不是同一个引用，如果是就反回true，不是就返回false

怎么用呢？

~~~javascript

//new方法，显示的构造函数来创建对象
var M = function(name){this.name=name}
var o3 = new M('o3');

o3 instanceof M；	//true
o3 instanceof Object;	//true，也就是只要是在这个原型链上的构造函数，都会被认为是o3的一个构造函数，面试中很容易错
M.prototype.__proto__===Object.prototype;	//true
o3.__proto__.constructor==M;	//true

~~~

![image-20200616215204384](../../../Library/Application Support/typora-user-images/image-20200616215204384.png)

###  new运算符

new的工作原理（例如new一个构造函数foo，从而创建新实例）

1. new运算符 先创建了一个新的空对象，此时实例对象还没有生成，这个空对象是继承构造函数的原型对象，也就是从这个空对象，指向了原型对象。也就是此时原型链已经被关联上一部分了。
2. 第二步时候，构造函数 foo 被执行。执行时候，相应的船参会被传入，同时上下文（this）会被指定为这个新实例，也就是this 相关联。如果没有参数的时候，new foo等同于new foo()，只能用再不传递任何参数的情况。
3. 如果构造函数返回了一个“对象”，那么这个对象会取代整个new出来的结果。如果构造函数没有返回对象，那么new出来的结果为步骤1创建的对象。 

~~~javascript
//new工作原理，模拟new运算符
var new2 = function(func){
  //第一步，创建一个新对象，空对象要关联构造函数的执行对象func.prototype
  var o = Object.create(func.prototype);
  //第二步，执行构造函数，指针指向
  var k = func.call(o);
  //第三部，判断转移完的是不是对象类型
  if(typeof k ==='object'){
    return k;
  }else {
    return o;
  }
}
var M = function(name){this.name=name}
//使用new2
var o6 =new2(M);

o6.__proto__ === M.prototype	//true
~~~



![image-20200616220221898](../../../Library/Application Support/typora-user-images/image-20200616220221898.png)



## call 和 apply

ECMAScript 规范给`所有函数`都定义了`call` 与 `apply` 两个方法，它们的应用非常广泛，作用也是一模一样，只是`传参形式有区别`而已，并且他们的**目的**都是为了`改变this的指向`。

**注意：**

call()方法的作用和 apply() 方法类似

- 第一个参数都是 **在 fun 函数运行时指定的`this`值**

区别就是，第二个参数（或call中的第二个以及第二个以后的参数）：

- `call()`方法接受的是**参数列表**（把参数按顺序穿进调用call的方法里） ：func.call(`this`, arg1, arg2);
- `apply()`方法接受的是**一个参数数组**（把参数放在数组里统一传到调用call的方法里）：func.apply(`this`, [arg1, arg2])

---

总结call、apply、bind：

1. apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；

2. apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；

3. apply 、 call 、bind 三者都可以利用后续参数传参；

4. bind 返回值是对应的函数，便于稍后调用

5. apply 、call 则是立即调用 

   ~~~javascript
   var obj = {
       name: 'boxZhang'
   }
   function func() {
      return this.name;
   }
   console.log(func.bind(obj)());  //boxZhang 多了个括号，因为bind()要返回一个原函数的拷贝
   console.log(func.call(obj));    //boxZhang，func的this指向的是obj
   console.log(func.apply(obj));   //boxZhang，func的this指向的是obj
   
   // 三个输出的都是boxZhang，但是注意看使用 bind() 方法的，他后面多了对括号。
   // 也就是说，区别是，bind 方法不会立即执行，而是回调执行的时候，使用 bind() 方法。bind()的返回值是一个函数。
   // 而 apply和call 则会立即执行函数。
   
   ~~~



## 面向对象

###类与实例

类的声明

~~~javascript
/**
*	类的声明
*/
function Animal() {
	this.name="name"
}

/**
* ES6中 class的声明
*/
class Animal2{
  constructor(){
    this.name = name;
  }
}

~~~

生成实例

~~~javascript
/**
* 事例化
*/
console.log(new Animal(),new Animal2())
~~~



###类与继承

继承的实质是原型链。

如何实现继承

- **方法一**：

~~~javascript
/**
* 通过构造函数实现继承
*/
function Parent1(){
  this.name="parent1"
}
function Child1(){
  Parent1.call(this);	//将父级构造函数的this指向子构造函数的实例上去，所以父级所有的属性在子级里面也有
  this.type="child1"
}
console.log(new Child1());	//任何函数都有prototype属性，只有当是构造函数的时候才能起到他的作用

/**
* 通过构造函数实现继承  看一下缺点
*/
function Parent1(){
  this.name="parent1"
}
Parent。prototype.say=function(){}	//这样的话，Child1是无法继承say属性的。
function Child1(){
  Parent1.call(this);	//如果父类的属性都在构造函数里面的话，那没有问题，完全可以实现继承。但是如果父类的原型对象还有方法的话，那么子类是拿不到该方法的
  this.type="child1"
}
console.log(new Child1(),new Child1().say());	//会提示.say is not a function
~~~

通过构造函数实现继承：

1. 原理是：原型对象的属性可以经由对象实例访问
2. 缺点是：但是如果父类的原型对象还有别的方法的话，那么子类是拿不到该方法的

- **方法二：**

~~~javascript
/**
* 通过原型实现继承
*/

function Parent2(){
  this.name="parent2"
  this.play = [1,2,3]
}
function Child2 (){
  this.type="child2"
}
Child2.prototype = new Parent2();

console.log(new Child2(), new Child2().name);	//new Child2().name 是parent2
console.log(new Child2().__proto__);	//引用的是Parent2的实例。Child2().__proto__.name 也是parent2

/**
* 看一下缺点
*/
var s1 = new Child2();
var s2 = new Child2();
console.log(s1.play,s2.play);	//[1,2,3] [1,2,3]

s1.play.push(4);
console.log(s1.play,s2.play);	//[1,2,3,4] [1,2,3,4]	发现改了第一个实例的属性，第二个实例也跟着改变了，因为play这个属性是建立在Child2这个函数的原型链上的，原型链中的原型对象，他们是共用的，即s1.__proto__ === s2.__proto__ 是true

~~~

通过原型链实现继承：

1. 原理是：通过把一个对象放在另一个对象的原型链上，实现this的改变
2. 缺点是：如果新建实例时，只要一个实例的原型链上的属性有变化，另一个实例就会跟着变

- **方法三：**

组合的方式（写面向对象时候最通用的方式）

~~~javascript
/**
* 通过组合的方式实现继承，结合优点，弥补不足
*/
function Parent3(){
  this.name="parent3";
  this.play= [1,2,3];
}
function Child3 (){
  Parent3.call(this);	//构造函数的继承的那种写法
  this.type="child3"
}
Child3.prototype = new Parent3();

var s3 = new Child3();
var s4 = new Child3();

s3.play.push(4);

console.log(s3.play,s4.play);	//[1,2,3,4] [1,2,3]

/**
* 组合继承的优化1
*/
function Parent4(){
  this.name="parent4";
  this.play= [1,2,3];
}
function Child4 (){
  Parent4.call(this);	//构造函数的继承的那种写法
  this.type="child4"
}
Child4.prototype = Parent4().prototype;

var s5 = new Child4 ();
var s6 = new Child4 ();

s5.play.push(4);
console.log(s5.play,s6.play);	//[1,2,3,4] [1,2,3]

console.log(s5 instanceof Child4,s6.instanceof Child4);	
console.log(s5.constructor);	


/**
* 组合继承的优化2
*/
function Parent5(){
  this.name="parent5";
  this.play= [1,2,3];
}
function Child5 (){
  Parent5.call(this);	//构造函数的继承的那种写法
  this.type="child5"
}
Child5.prototype = Object.create(Parent5.prototype);	//__proto__
Child5.prototype.constructor = Child5;

var s7= new Child5();
console.log(s7 instanceof Child5, s7 instanceof Parent5);
console.log(s7.constructor);

~~~

## 通信类

###同源策略及限制

>  同源策略限制 从一个源加载的文档或脚本如何与来自另一个源的资源进行交互。
>
> 这是一个用于隔离潜在恶意文件的关键安全机制。
>
> 一个源包含：协议、域名、端口，必须要这三个都一致，才能叫做同源

不同源的限制有：

- Cookie、LocalStorage和IndexDB无法读取
- DOM无法获得
- AJAX请求不能发送

###前后端如何通信（为了考察知识面是不是宽）

1. Ajax
2. WebSocket
3. CORS

###如何创建Ajax

1. XMLHttpRequest对象的工作流程是怎样的
2. 兼容性处理
3. 事件的触发条件
4. 事件的触发顺序

### 跨域通信的几种方式

1. JSONP

   JSONP的原理和实现方式；就是利用script的异步加载来实现的 

2. Hash（url地址后面#后的东西，hash的改变是不刷新页面的）

3. postMessage

4. WebSocket（不受同源策略限制）

5. CORS（支持跨域通信的AJAX）

## 安全类

1. CSRF

   - 基本概念、缩写：跨站请求伪造，英文：Cross-site request forgery

   - 攻击原理

     - 网站中某个接口存在这种漏洞
     - 用户在这个网站确实登录过
     - 例如（图）一个用户，是网站A的注册用户，通过身份认证登陆这个网站，网站A核查这个身份是不是正确的，如果正确，就下发cookie，这个cookie会保存在用户的浏览器中，这就完成了一次身份认证的过程。下面用户有访问了网站B，这个网站B在下发页面的时候会存在一个引诱点击，这个点击往往会是个链接，指向网站A的一个api接口，如果用户禁不住诱惑点击了的话，就会访问到网站A。

     ![image-20200706154750785](../../../Library/Application Support/typora-user-images/image-20200706154750785.png)

   - 防御措施

     - 添加token验证：在访问一个借口的时候，浏览器只是自动的生成了一个cookie，但是没有手动上传一个token。这个token，是你注册成功后，或者访问这个网站后，服务器会自动的在本地存储一个token，如果访问各种接口时候，没有带这个token，他就不会帮你通过验证，如果你点击了某个引入链接，这个链接只会帮你携带cookie，不会自动携带token，所以就避免了那个攻击。
     - referer验证：referer指的是页面来源，服务器判断这个页面来的是不是我这个站点下面的页面，如果是，就执行这个动作，如果不是，就拦截。
     - 隐藏令牌：和token有点像，只不过放在http head头中，不会放在链接上，这样就会做的比较隐蔽，只是使用方式上有一些差别，本质没什么区别。

2. XSS
   - 基本概念：跨域脚本攻击
   - [攻击原理](http://www.imooc.com/learn/812)：http://www.imooc.com/learn/812
   - [防御措施](http://www.imooc.com/learn/812)：http://www.imooc.com/learn/812

CSRF和XSS区别：

XSS是向页面注入js去运行，在js函数体里面去做他想做的事。

CSRF是利用你本身的漏洞，去帮你自动执行那些借口，而且CSRF是依赖于你要接触的那个网站

## 算法类

1. 排序

   - [快速排序](https://segmentfault.com/a/1190000009426421)：https://segmentfault.com/a/1190000009426421
   - [选择排序](https://segmentfault.com/a/1190000009366805)：https://segmentfault.com/a/1190000009366805
   - [希尔排序](https://segmentfault.com/a/1190000009461832)：https://segmentfault.com/a/1190000009461832

   ![image-20200706181546096](../../../Library/Application Support/typora-user-images/image-20200706181546096.png)

2. 堆栈、队列、链表

   - [堆栈](https://juejin.im/entry/58759e79128fe1006b48cdfd)：https://juejin.im/entry/58759e79128fe1006b48cdfd
   - [队列](https://juejin.im/entry/58759e79128fe1006b48cdfd)：https://juejin.im/entry/58759e79128fe1006b48cdfd
   - [链表](https://juejin.im/entry/58759e79128fe1006b48cdfd)：https://juejin.im/entry/58759e79128fe1006b48cdfd

3. 递归

   - [递归](https://segmentfault.com/a/1190000009857470)：https://segmentfault.com/a/1190000009857470 

4. 波兰式和逆波兰式

   - 理论：https://www.cnblogs.com/chenying99/p/3675876.html
   - 源码：https://github.com/Tairraos/rpn.js/blob/master/rpn.js

## 渲染机制

1. 什么是doctype及作用

   DTD（document type definition 文档类型定义）是一系列的语法规则，用来定义XML或（X）HTML的文件类型。浏览器会用它来判断文档类型，决定使用何种协议来解析，以及切换浏览器模式。

   定义：DOCTYPE是用来声明文档类型和DTD规范的，一个主要的用途便是文件的合法性验证。如果文件代码不合法，那么浏览器解析时便会出一些差错。也就是DOCTYPE用来直接告诉浏览器，使用的是DTD规范

   4.0 的DOCTYPE有传统模式和严格模式

2. 浏览器的渲染过程

   先把html和css转成html tree和css tree，结合形成render  tree，然后通过layout，精确的计算出各个div等元素需要画在的浏览器的位置，最后是painting，在浏览器中画图，最后形成display，一个完整的页面图。

   - 生成dom树
   - 生成render树
   - 执行reflow（在render树的基础上计算页面真实显示dom的位置）
   - 执行repaint（为真实显示的dom绘制不影响dom位置的样式，如设置dom的color等）

3. 重排Reflow

   定义：DOM结构中的各个元素都有自己的盒子（模型），这些都需要浏览器根据各种样式来计算并根据计算结果将元素放到它该出现的位置，这个过程称之为reflow。也就是当页面发生的某些变化影响了布局，需要倒回去重新渲染，该过程称为reflow（重排/回流）。

   **触发Reflow：**

   - 增加、删除、修改DOM结点时，会导致Feflow或Repaint
   - 当移动DOM的位置，或是搞个动画的时候
   - 当修改css样式的时候
   - 当Resize窗口的时候（移动端没有这个问题），或是滚动的时候
   - 当修改网页的默认字体时
   - 改变窗囗大小；
   - 改变文字大小；
   - 添加/删除样式表；
   - 内容的改变，如用户在输入框中输入信息；
   - 激活伪类，如:hover；
   - 操作class属性；
   - 脚本操作dom；
   - 获取dom的offsetWidth和offsetHeight；
   - 设置style属性。

   **reflow的优化：**

   1. 尽可能限制reflow的影响范围，修改dom层级较低的结点。不要通过父级元素影响子元素样式。最好直接加在子元素上。改变子元素样式尽可能不要影响父元素和兄弟元素的尺寸；
   2. 不要一条一条的修改dom的样式，最好通过设置class的方式。 避免重复触发reflow和repaint；
   3. 经常reflow的元素，比如动画，position设为fixed或absolute，使其脱离文档流，不影响其它元素的布局；
   4. 权衡速度的平滑。比如实现一个动画，以1px为单位移动这样最平滑，但reflow就会过于频繁，CPU很快就会被完全占用。如果以3个像素为单位移动就会好很多；
   5. 不要用tables布局。tables中某个元素一旦触发reflow就会导致table里所有的其它元素reflow。在适合用table的场合，可以设置table-layout为auto或fixed，这样可以让table一行一行的渲染，这种做法也是为了限制reflow的影响范围；
   6. 避免使用css expression（每次都会重新计算）；
   7. 减少不必要的dom层级（DOM depth）。改变dom树中的一级会导致所有层级的改变，上至根部，下至被改变节点的子节点。这导致大量时间耗费在执行reflow上面；
   8. 避免不必要的复杂的css选择器，尤其是后代选择器（descendant selectors），因为为了匹配选择器将耗费更多的cpu；
   9. 尽量不要频繁的增加、修改、删除元素，可以先把dom节点抽离到内存中进行复杂的操作然后再display到页面上。（display:none的节点不会被加入render树，而visibility:hidden会；display:none会触发reflow，而visibility:hidden只会触发repaint，因为layout没有变化）。

4. 重绘Repaint

   当各种盒子的位置，大小以及其他属性，例如颜色、字体大小等都确定下来后，浏览器于是把这些元素都按照各自的特性绘制了一遍，于是页面的内容出现了，这个过程称之为repaint。

   触发Repaint：

   - DOM改动
   - CSS改动

   最大程度的降低Repaint（优化性能）

   ​		例如：用户输入，然后提交后，再隐藏用户输入的内容，显示返回结果。输出结果如果有n个，也不要一个一个填充到这个dom节点中去，而是把结果全部放在一个document片段里，一次性放到dom节点中，从而减少repaint

   

   > **简而言之，如果页面的变化会导致dom的位置发生变化，则会触发reflow，如果不会导致dom的位置发生变化，则会触发repaint。如果触发了reflow则一定会触发repaint，而触发repaint则不一定会触发reflow。另外，reflow的成本比repaint高很多，dom树里每个结点的reflow都可能触发其子结点、祖先结点、兄弟结点的reflow。reflow过于频繁是导致页面性能下降的关键因素之一（也是页面性能优化的主要方向）。**

5. 布局Layout

## js运行机制

~~~javascript
console.log(1);
setTimeout(function(){
console.log(2)
},0)
console.log(3);

//132
~~~

js是单线程的，也就是js在同一时间只能做一件事。

任务队列：

- 同步任务：console.log()

- 移步任务：setTimeout()、setInterval()

~~~javascript
for(var i=0;i<4;i++){
  setTimeout(function(){
    console.log(i)
  }, 1000)
}
//输出四个4，for循环体执行完才会去执行setTimeout(),异步任务的放入时间和执行时间。
//原理：到时间了，定时器才会把setTimeout丢到异步任务队列中，然后在队列中再等待一个叫事件循环的东西来执行
~~~

任务队列Event Loop

[http://www.ruanyifeng.com/blog/2013/10/event_loop.html](http://www.ruanyifeng.com/blog/2013/10/event_loop.html) 

什么时候会开启异步任务

- setTimeout()   setInterval()
- DOM事件
- ES6中的Promise

## 页面性能

### 提升页面性能的方法：

1. 资源压缩合并，减少http请求

2. 非核心代码的异步加载——异步加载的方式——这些异步加载的区别

   异步加载的方式：

   - 动态脚本加载
   - defer：defer是在html解析完之后才会执行，如果是多个，按照加载的顺序依次执行
   - async：async是在加载完之后立即执行，如果是多个，执行顺序和记载顺序无关，也就是哪个先回来哪个就先执行  

3. 利用浏览器缓存——缓存的分类——缓存的原理

   浏览器缓存其实就是资源文件在浏览器的备份，或者说是副本。

   - **强缓存**：问都不问，不直接去请求，直接就拿来用

     **Expires**	Expires:Thu,21 Jan 2020 23:20:02 GMT  （在http头上会携带Expires，是绝对时间，在这个时间是服务器的时间，下发时候是服务器时间）

     **Cache-Control**	Cache-Control:max-age=3600	（这个是相对时间，3600是秒，也就是当我拿到请求结果3600s之内，都不会再重新请求服务器了，在这个时间之内都会从浏览器拿缓存数据）

     如果这两个时间都下发了，那么以后者为准。

   - **协商缓存**：浏览器发现我的本地有这个副本，但是不确定能不能用，要向浏览器问一下是否可以用，是否过期，再判断是否进行调取

     **Last-Modified If-Modified-Since**	Last-Modified:Wed,26 Jan 2020 00:30:11 GMT	（我拿到某个资源文件的时候，会通过这个字段Last-Modified 下发某个时间，当我下次再去请求，问服务器这个资源有没有什么变化，是用http请求头中加这个k值 If-Modified-Since，但是他俩的值是一个。

     **Etag If-None-Match**	哈希值

4. 使用CDN

   

5. 预解析DNS

   ~~~javascript
   <neta http-equiv="x-dns-prefetch-control" content="on">	//页面中的a标签，浏览器是默认打开dns预解析的，但是，你这个页面是https开头的，很多浏览器是关闭这个功能的，<neta http-equiv="x-dns-prefetch-control" content="on">这句话意思就是就是强制打开dns预解析
   <link rel="dns-prefetch" href="//host_name_to_prefetch.com">
     //预解析DNS rel="dns-prefetch"
   ~~~

   

## 错误监控

问：如何进行错误监控/如何保证产品质量体系？

### 前端错误的分类

1. 即时运行错误
   - try……catch
   - window.onerror
2. 资源加载错误
   - object.onerror
   - performance.getEntries()    返回值是一个数组，所以可以通过forEach进行遍历查看
   - Error事件捕获    

延伸：跨域的js运行错误可以捕获代码吗？错误提示是什么？应该怎样处理？

答：也是可以拿到的，错误提示：Script error.

处理：1、在script标签上，增加crossorigin属性。2、设置js资源响应头Access-Control-Allow-Origin:*![image-20200707181305198](../../../Library/Application Support/typora-user-images/image-20200707181305198.png)

### 错误的捕获方式

#### 同步错误同步错误

##### 一、 `SyntaxError`：语法错误

语法错误，这一类错误在预解析的过程中如果遇到，就会导致整个`js`文件都无法执行。在`vue`项目中如果存在语法错误，将直接无法运行，打包也将会直接报错

##### 二、`Uncaught ReferenceError`：引用错误

引用一个不存在的变量时发生的错误。将一个值分配给无法分配的对象，比如对函数的运行结果或者函数赋值。此类错误可以通过`try-catch`捕获到

```
try {
    a()
} catch(e) {
	console.log('捕获到错误引用的错误==>',e)
    // 捕获到错误引用的错误==> Uncaught ReferenceError: a is not defined
}
复制代码
```

##### 三、`RangeError`:范围错误

`RangeError`是当一个只超出有效范围时发生的错误。主要的有几种情况，第一是数组长度为负数，第二是`Number`对象的方法参数超出范围，以及函数堆栈超过最大值。此类错误可以通过`try-catch`捕获到

```
try{
    [].length=-5
} catch(e) {
    console.log('捕获到范围错误==>',e)
    // 捕获到范围错误==> Uncaught RangeError: Invalid array length
}
复制代码
```

##### 四、`TypeError`:类型错误

变量或参数不是预期类型时发生的错误。比如使用new字符串、布尔值等原始类型和调用对象不存在的方法就会抛出这种错误，因为new命令的参数应该是一个构造函数。此类错误可以通过`try-catch`捕获到

```
try{
    const a = {}
    a()
} catch(e) {
    console.log('捕获到类型错误==>',e)
    // 捕获到类型错误==> TypeError: a is not a function
}
复制代码
```

##### 五、`URIError,URL`错误

主要就是相关函数的参数不正确；URI相关参数不正确时抛出的错误，主要涉及`encodeURI、decodeURI()、encodeURIComponent()、decodeURIComponent()、escape()和unescape(）`六个函数。此类错误可以通过`try-catch`捕获到

```
try{
    decodeURI('%')
} catch(e) {
    console.log('捕获URI错误==>',e)
    // 捕获URI错误==> URIError: URI malformed
    //                       at decodeURI (<anonymous>)
}
复制代码
```

#### 异步错误

##### 一、`promise/async-await`错误

`Promise` 是异步编程的一种解决方案，比传统的解决方案`callback`更加的优雅。它最早由社区提出和实现的，`ES6` 将其写进了语言标准，统一了用法，原生提供了`Promise`对象。`Promise`虽然可以避免回调地狱，但是一旦出现问题，无法使用`try-catch`进行捕获；这就对我们的错误捕获及处理就造成了不必要的麻烦。

好在`ES8`加入了对`async/await`的支持，也就我们所说的`异步函数`，这是一个很实用的功能。 `async/await`将我们从头痛的回调地狱中解脱出来了，使整个代码看起来很简洁。`async-await`的加入是我们又可以使用`try-catch`捕获异步的错误了

```
async function test (){
    try {
        // 假设a是一个异步函数
        await a()
    } catch(e){
        console.log('捕获到异步的错误==>',e)
    }
}
复制代码
```

##### 二、`settimeout/setinterval/callBack`错误

在`vue`中可以使用`window.onerror()`进行监听`settimeout/setinterval/callBack`的错误;

```
window.onerror = (message,url,lineNo,cloumnNo,error) => {
    // message 错误信息
    // url 文件名
    // lineNo 行号
    // cloumnNo 列号
    // error 错误信息
}
复制代码
```

#### 资源加载错误

使用`window.addEventListener('error')`捕获，`window.onerror`捕获不到资源加载错误;`window.onerror`和`window.addEventListener('error')`的异同:相同点是都可以捕获到`window`上的`js`运行时错误。区别是1.捕获到的错误参数不同 2.`window.addEventListener('error')`可以捕获资源加载错误，但是`window.onerror`不能捕获到资源加载错误

#### AJAX请求错误

这个错误可以在axios的请求拦截器中进行捕获该错误



### 上报错误的基本原理

1. 用Ajax通信的方式上报
2. 利用Image对象上报![image-20200707181433213](../../../Library/Application Support/typora-user-images/image-20200707181433213.png)

## MS技巧

准备要充分、描述要演练、引导找时机、优势要发挥、回答要灵活

团队协作能力：主动描述

- 团队协作的能力
- 主动推动去做的事情
- 带队能力
- 组织能力
- 学习能力

HR：考察的是一个同学的性格等

- 乐观积极
- 主动沟通
- 逻辑顺畅
- 上进有责任心
- 有主张，做事果断
- 职业竞争力：
  - 业务能力
  - 思考能力（对同一件事可以从不同角度思考，找到最优解）
  - 学习能力（不断学习心得业务和技术，沉淀、总结）
  - 无上限的付出（对于无法解决的问题可以熬夜加班）
- 职业规划

![image-20200708152549819](../../../Library/Application Support/typora-user-images/image-20200708152549819.png)

~~~
ls	｜查看当前目录
cd	｜进入目录
touch index.html	｜创建index.html文件
open -a atom index.html	|打开index.html文件，open 指定编辑器
~~~







[1、面试题基础](https://blog.csdn.net/come0across/article/details/104895118)

[2、老内容面试](https://zhuanlan.zhihu.com/p/84212558)

[3、新内容vue](https://www.cnblogs.com/JokerAn/p/12720329.html)

















