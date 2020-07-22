# javascript——对象

[TOC]

## 前言

什么是对象？

ES5中提到，ECMAScript中的对象，是一组数据和功能的集合。是某个特定引用类型的实例。

新对象是使用new操作符后跟一个构造函数来创建的。

ES5中讲到，Object的每个实例都具有下列属性和方法：

1. constructor：
2. hasOwnProperty
3. isPrototypeOf
4. propertyIsEnumerable
5. toLocaleString
6. toString
7. valueOf



## 浅谈ECMAScript中的数据类型

### 基本类型  <sub>(Undefined、Null、Boolean、Number、String、Object、Symbol)</sub>

5种简单数据类型：Undefined、Null、Boolean、Number、String。

1种复杂数据类型：Object（Object实际上是由一组无序的名值对组成）。

ES6引入了一种新的原始数据类型 Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型。它也是基本数据类型。

**基本类型特点**

- 基本数据类型的值是按值访问的
- 基本类型的值是不可变的
- 基本类型的比较是它们的值的比较
- 基本类型的变量是存放在栈内存（Stack）里的

**基本类型图解**

- 栈内存中包括了变量的标识符和变量的值

  ![object-type1](/Users/zhangml/[个人文件]/技术宅/Array/object-type1.png)

### 引用类型 <sub>(Object、Array、Date、RegExp、Function、基本包装类型、单体内置对象)</sub>

引用类型的值（对象）是引用类型的一个实例。

 ECMAScript 中，引用类型是一种数据结构，用于将数据和功能组织在一起。它也常被称为类，但这种称呼并不妥当。

引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。

而我们看到的大多数引用类型值都是Object类型的实例。引用类型有：Object类型、Array类型、Date类型、RegExp类型、Function类型、基本包装类型（Boolean、Number、String）、单体内置对象（Global 对象、Math对象）

**引用类型特点**

- 引用类型的值是按引用访问的
- 引用类型的值是可变的
- 引用类型的比较是引用的比较
- 引用类型的值是保存在堆内存（Heap）中的对象（Object） 与其他编程语言不同，JavaScript 不能直接操作对象的内存空间（堆内存）。

**引用类型图解**

- 栈内存中保存了变量标识符和指向堆内存中该对象的指针

- 堆内存中保存了对象的内容

  ![object-type2](/Users/zhangml/[个人文件]/技术宅/Array/object-type2.png)

##检测变量类型的办法 <sub>(typeof、 toString、instanceof)</sub>

> **如果你要判断的是基本数据类型或 JavaScript 内置对象，使用`toString`； 如果要判断的是自定义类型，请使用`instanceof`。**
>
> **为什么不用 typeof ？**
>
> 我们知道检测基本数据类型可以用 typeof，但是`typeof`只能用于基本数据类型检测，对于 null 还有 Bug。
>
> Bug：使用`typeof`检查 null 时会返回 “object”，这是由于不同的对象在底层都表示为二进制，在 JavaScript 中二进制前三位都为 0 的话会被判断为 object 类型，null 的二进制表示全是 0，自然前三位也是 0，所以执行`typeof`时会返回 “object”。

### typeof 方法



### toString 方法

`toString`方法是 Object 的实例方法，因为所有对象都是 Object 的实例，所以所有对象都有该方法。如果此方法在自定义对象中未被覆盖，`toString()`会返回 “[object type]”，其中 type 是对象类型。

不过 Array、Data 会重写从 Object.prototype 继承来的`toString`方法，所以检测时应当直接调用`Object.prototype.toString`来检测。

从 javascript 1.8.5 开始可以检测 undefined 与 null。

~~~javascript
var a = []
 
Object.prototype.toString.call(a) // "[object Array]"
Object.prototype.toString.call(undefined) // "[object Undefined]"
Object.prototype.toString.call(null) // "[object Null]"
~~~

### instanceof 方法

`instanceof`运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。我们使用的所有对象都是对象子类型，它们要么是内置构造函数的实例，要么是我们自定义构造函数的实例。因此可以使用`instanceof`来判断这些对象的类型。

## 对象分类

### 本地对象

> ECMA-262把本地对象（native object）定义为“独立于宿主环境的 ECMAScript 实现提供的对象”。

Object、Function、Boolean、Symbol、Array、Number、Date、String、RegExp、Map、Set、WeakMap、WeakSet、Promise、Generator、Reflect、Proxy、Error……

### 内置对象

> “ 由ECMAScript实现提供的，独立与宿主环境的所有对象，在ECMAScript程序开始执行时出现”。这意味着开发者不必明确实例化内置对象，它已经被实例化了。ECMA只定义了两个内置对象，即Global和Math（它们也是本地对象，根据定义，所有内置对象都是本地对象）。

- Global：在 JavaScript 中，所有的本地对象、全局属性、全局函数都是 Global 对象的属性。
- Math

### 宿主对象

> 所有非本地对象都是宿主对象，即由ECMAScript实现的宿主环境提供的对象。

所有的 BOM 和 DOM 对象都是宿主对象。JavaScript 中常用的宿主对象主要包括以下：

- BOM 对象：window、location、navigator、screen、history
- DOM 对象：Document、Body、Event、Form、Image、事件对象 event……

### 用户自定义对象

> 开发者通过 Js 代码创建的自己的对象。

## 属性

**prototype**

返回对象类型原型的引用。prototype 属性是 object 共有的。

一般用来给实例添加方法和属性。

## 创建对象

### 简单做法 <sub>(Object构造函数、对象字面量、ES6、工厂模式)</sub>

1. **使用Object构造函数创建**

   ~~~javascript
   // 对象实例的创建
   var obj = new Object();
   obj.key = 'value';   //使用构造函数创建一个空对象，并赋值
   console.log(obj);	//{key: "value"}
   ~~~

2. **使用对象字面量表示法创建**

   ~~~javascript
   //使用字面量创建一个对象
   var obj = {
       key1: 'value1',
       key2: 'value2'
   }  
   ~~~

3. **ES6更简洁的方式创建对象**

   ~~~javascript
   var age = 20
   var sex = "sexy"
    
   var a = {
       name: 'jack',
       age, 	// 简洁表示法，等同于 age: age
       sayName(){}, 	// 简洁表示法，等同于 sayName: function() {}
       ['lo' + 'ver']: 'rose', 	// 属性名表达式，等同于 lover: 'rose'
       [sex]: 'male'	// 属性名表达式，等同于 sexy: 'male'
   }
   console.log(a);	//{name: "jack", age: 20, sayName: ƒ, lover: "rose", sexy: "male"}
   ~~~

4. **工厂模式**

   > 工厂模式 即可实现具有相同属性元素的批量生产。
   >
   > 即用函数来封装创建对象的细节。多次调用该函数来创建多个相似对象。

   ~~~javascript
   function createPerson(name, age, job){
       var o = new Object();
       o.name = name;
       o.age = age;
       o.job = job;
       o.sayName = function(){
           alert(this.name);
       };
   	return o; 
   }
   var person1 = createPerson("Nicholas", 29, "Software Engineer");
   var person2 = createPerson("Greg", 27, "Doctor");
   ~~~

   `! 工厂模式虽然解决多创建多个相似对象的问题，但却没有解决对象识别的问题（即怎样知道一个对象的类型）。`于是，新的模式出现了。

### 模仿“类”的设计 <sub>（构造函数模式、原型模式）</sub>

> **JavaScript 类**
>
> - JavaScript 是面向对象的语言，但 JavaScript 不使用类。即JavaScript 和面向类的语言不同，它并没有类作为对象的抽象模式或者说蓝图。JavaScript 中只有对象。`所以此处称为模仿“类”的设计`
> - 在 JavaScript 中，不会创建类，也不会通过类来创建对象（就像在其他面向对象的语言中那样）。
> - JavaScript 基于 prototype，而不是基于类的。
> - 所谓的类就是拥有共同属性的一类群体

1. **构造函数模式**

   构造函数包括像 Array、Object 这样的原生构造函数，他们在 js 运行时会自动出现在执行环境中。

   此外，我们可以创建自定义构造函数，从而定义自定义类型的属性和方法。现在使用构造函数重写上个例子：

   ~~~javascript
   // 按照惯例，构造函数首字母要大写，非构造函数首字母小写。因为构造函数也是函数，只不过可以用来创造对象而已，所以要以示区别。
   function Person(name, age, job){
           this.name = name;
           this.age = age;
           this.job = job;
           this.sayName = function(){
               alert(this.name);
   }; }
   var person1 = new Person("Nicholas", 29, "Software Engineer");
   var person2 = new Person("Greg", 27, "Doctor");
   
   console.log(person1 instanceof Person);	//true 	person1是Person类型的
   console.log(person1.constructor ==Person);	//true	对象的 constructor 属性最初是用来标识对象类型的
   ~~~

   构造函数创建的对象特点：

   - 没有显示的创建对象
   - 直接将属性和方法赋给了this对象
   - 没有return语句

   通过构造函数创建新的实例，必须使用 new 操作符，发生构造函数调用时 经历以下4个步骤：

   - 创建一个新对象
   - 将构造函数的作用域赋给新对象（因此this就指向了这个新对象）
   - 执行构造函数中的代码（为这个对象添加属性）
   - 返回新对象

   构造函数与函数的唯一区别：**调用它的方式不同**。任何函数只要通过`new` 操作符来调用，那它就可以作为构造函数。

   ~~~javascript
   // 作为构造函数使用
   var person = new Person("Nicholas", 29, "Software Engineer"); 
   person.sayName(); //"Nicholas"
   // 作为普通函数调用
   Person("Greg", 27, "Doctor"); // 添加到window
   window window.sayName(); //"Greg"
   // 在另一个对象的作用域中调用
   var o = new Object();
   Person.call(o, "Kristen", 25, "Nurse"); 
   o.sayName(); //"Kristen"
   ~~~

   由于构造函数调用时会自动执行 [[Prototype]] （使用双中括号是为了表示这个是构造函数的Prototype）链接，也就是把新对象的原型链指向构造函数的 prototype。所以使用`instanceof`或`isPrototypeOf`方法可以判断他们的类型。(instanceof运算符用于测试构造函数的prototype属性是否出现在对象的原型链中的任何位置)

   上面这种构造函数解决了对象类型识别的问题，但是每个方法都要在每个实例上重新创建一遍，在上面的例子中，a 和 b 都有个名为`sayName()`的方法，这两个方法虽然名字、内容、功能相同，但却分别在 a 和 b 中都重新创建了一次，这是没有必要的。

   更好的方法应该是将公用的方法放到他们的原型上，也就是下面要说的原型模式。

2. **原型模式**

   所有函数都有一个不可枚举的 [prototype（原型）属性](https://juejin.im/post/5c765cdce51d453f4142d25a)，这个属性是一个指针，指向一个对象。

   使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法。

   ~~~javascript
   function Foo() {};
   Foo.prototype;	 // {}
   ~~~

   这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法，我们通常称这个对象为 Foo 的**原型**。

   上一节【构造函数模式】里面有说，`new`操作符会新建一个对象，并把该对象的原型链指向构造函数的 prototype 所指向的对象。

   这里出现了一个重点词**原型链**，我们先解释下什么叫做原型链。

   > **原型链**
   >
   > 原型链也被称为 [[Prototype]]链（规范中用 [[Prototype]] 表示对象隐式的原型，在 JavaScript 中用 \_\_proto\_\_ 表示），是对象的内置属性。原型链是 ECMAScript 中实现继承的主要办法，其基本思想就是让一个引用类型继承另一个引用类型的属性和和方法。

   例如我们新建个对象 a，然后给它指定它的原型链的指向：

### 面向委托的设计



## 对象的内容





## 对象的方法





## 对象的实例方法





## 引用列表







