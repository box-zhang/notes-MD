# call apply

[TOC]

不知大家有没有像曾经的我一样，一听到call apply，就一头雾水，感觉怎么也弄不清楚。为了能让自己妥妥的记住，特总结了这篇小文，以便再忘记了的时候，能够对学习的痕迹有所追寻。

ECMAScript 规范给`所有函数`都定义了` call` 与 `apply` 两个方法，它们的应用非常广泛，作用也是一模一样，只是`传参形式有区别`而已，并且他们的**目的**都是为了**`改变this的指向`**。

## 一、apply()

> **apply()** 方法调用一个具有给定`this`值的函数，以及作为一个数组（或[类似数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#Working_with_array-like_objects)）提供的参数。

> ```javascript
> //apply语法
> func.apply(thisArg, [argsArray])
> ```
>
> - thisArg（可选值）
>
>   在 *func* 函数运行时使用的 `this` 值，即func的this指向thisArg这个参数。
>
>   请注意，`this`可能不是该方法看到的实际值：如果这个函数处于[非严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)下，则指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。
>
> - argsArray（可选值）
>
>   `一个数组`或者`类数组对象`，其中的数组元素将作为单独的参数传给 `func` 函数。如果该参数的值为 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 或  [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)，则表示不需要传入任何参数。从ECMAScript 5 开始可以使用类数组（类数组：具有.length属性的对象）对象。
>
> - 返回值
>
>   使用调用者提供的`this`值和参数调用该函数的返回值。若该方法没有返回值，则返回`undefined`。

例如：

~~~javascript
var obj = {
    name : 'boxZhang'
}
function func(person1, person2){
    console.log(person1 + ' ' + this.name + ' ' + person2);
}
func.apply(obj, ['小明','小红']);    // 小明 boxZhang 小红

// 其中 obj 作为函数上下文的对象，函数func中的 this 指向了 obj 这个对象，所以func方法里面的this.name是obj.name。
// 参数 '小明' 和 '小红' 放在数组中传入 func 函数，分别对应 func 参数的列表元素person1，person2。
~~~



小练习：用apply将数组arrayA添加到数组arrayB中

~~~javascript
var arrayA = ['a','b','c'];
var arrayB = [1,2,3];
arrayA.push.apply(arrayB, arrayA);
console.log(arrayB);	//[1, 2, 3, "a", "b", "c"]
console.log(arrayA);	//["a", "b", "c"]
~~~



apply()的**便易**，可以通过下面一段代码简单介绍一下【[摘自MDN apply()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)】：

~~~javascript
/* 找出数组中最大/小的数字 */
var numbers = [5, 6, 2, 3, 7];

/* 应用(apply) Math.min/Math.max 内置函数完成 */ 
/*当心：如果某个引擎限制了方法参数，你的参数数组又非常大，用下面这种方法 会导致传入的数组有可能是不完整的。*/
var max = Math.max.apply(null, numbers); /* 基本等同于 Math.max(numbers[0], ...) 或 Math.max(5, 6, ..) */
var min = Math.min.apply(null, numbers);

/* 代码对比： 用简单循环完成 */
max = -Infinity, min = +Infinity;
for (var i = 0; i < numbers.length; i++) {
  if (numbers[i] > max)
    max = numbers[i];
  if (numbers[i] < min) 
    min = numbers[i];
}
~~~

## 二、call()

> **`call()`** 方法调用一个函数, 其具有一个指定的`this`值和分别地提供的参数(**参数的列表**)。

> ~~~javascript
> //call() 语法
> fun.call(thisArg, arg1, arg2, ...)
> ~~~
>
> - thisArg
>
>   在*fun*函数运行时指定的`this`值
>
>   请注意，`this`可能不是该方法看到的实际值：如果这个函数处于[非严格模式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)下，则指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。
>
> - arg1, arg2, ...
>
>   指定的参数列表。
>
> - 返回值
>
>   使用调用者提供的`this`值和参数调用该函数的返回值。若该方法没有返回值，则返回`undefined`。

例如：

```javascript
var obj = {
    name : 'boxZhang'
}
function func(person1, person2){
    console.log(person1 + ' ' + this.name + ' ' + person2);
}
func.call(obj, '小明','小红');    // 小明 boxZhang 小红

// 其中 obj 作为函数上下文的对象，函数func中的 this 指向了 obj 这个对象，所以func方法里面的this.name是obj.name。
// 参数 '小明' 和 '小红' 作为单独的参数中传入 func 函数，分别对应 func 参数的列表元素person1，person2。
// 对比apply可以看出，参数 '小明' 和 '小红' ，不是放入数组中传入的，而是作为单独参数传入的。
```

使用call方法，调用父构造函数：

~~~javascript
function Product(name, price) {
  this.name = name;
  this.price = price;
}
function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}
var cheese = new Food('feta', 5);
console.log(cheese.name);	//feta
~~~

## 三、call() 和 apply()

> **注意：**
>
> call()方法的作用和 apply() 方法类似
>
> - 第一个参数都是 **在*fun*函数运行时指定的`this`值**
>
> 区别就是，第二个参数（或call中的第二个以及第二个以后的参数）：
>
> - `call()`方法接受的是**参数列表**（把参数按顺序穿进调用call的方法里） ：func.call(``this``, arg1, arg2); 
> - `apply()`方法接受的是**一个参数数组**（把参数放在数组里统一传到调用call的方法里）：func.apply(``this``, [arg1, arg2])

## 四、bind()

> **`bind()`**方法与call和apply相似，也是可以改变this指向。
>
> **bind()** 函数会`创建一个新函数`，叫**绑定函数**。当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind() 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。调用**绑定函数**通常会导致执行**包装函数**。

> ~~~javascript
> // bind()语法
> function.bind(thisArg[, arg1[, arg2[, ...]]])
> ~~~
>
> - thisArg
>
>   调用绑定函数时作为`this`参数传递给目标函数的值。 如果使用[`new`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)运算符构造绑定函数，则忽略该值。当使用`bind`在`setTimeout`中创建一个函数（作为回调提供）时，作为`thisArg`传递的任何原始值都将转换为`object`。如果`bind`函数的参数列表为空，执行作用域的`this`将被视为新函数的`thisArg`。
>
> - arg1, arg2, ...
>
>   当目标函数被调用时，预先添加到绑定函数的参数列表中的参数。
>
> - 返回值
>
>   `返回一个原函数的拷贝`，并拥有指定的**this**值和初始参数。

例如：

```javascript
var bar = function(){
	console.log(this.x);
}
var foo = {x:3}
bar(); // undefined
var func = bar.bind(foo);	//bind()函数会创建一个新的函数，叫绑定函数
func(); // 3 调用绑定函数

// 这里创建了一个新的函数 func，当使用 bind() 创建一个绑定函数之后，它被执行的时候，它的 this 会被设置成 foo ， 而不是像我们调用 bar() 时的全局作用域。
```

bind的参数

~~~javascript
function func(a, b, c) {
    console.log(a, b, c);
}
var func1 = func.bind(null,'boxZhang');	//创建了一个新的函数func1

func('A', 'B', 'C');            // A B C
func1('A', 'B', 'C');           // boxZhang A B
func1('B', 'C');                // boxZhang B C
func.call(null, 'boxZhang');      // boxZhang undefined undefined

//可见，bind中的实参 是在 bind 中参数的基础上再往后排。
~~~

##五、apply()、call()、bind() 比较

```javascript
var obj = {
    name: 'boxZhang'
}
function func() {
   return this.name;
}
console.log(func.bind(obj)());  //boxZhang 多了个括号，因为bind()要返回一个原函数的拷贝
console.log(func.call(obj));    //boxZhang
console.log(func.apply(obj));   //boxZhang

// 三个输出的都是boxZhang，但是注意看使用 bind() 方法的，他后面多了对括号。
// 也就是说，区别是，bind 方法不会立即执行，而是回调执行的时候，使用 bind() 方法。bind()的返回值是一个函数。
// 而 apply和call 则会立即执行函数。
```

## 六、总结

- apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；
- apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；
- apply 、 call 、bind 三者都可以利用后续参数传参；
- bind 返回值是对应的函数，便于稍后调用
- apply 、call 则是立即调用 。

## 原文地址追溯

[【优雅代码】深入浅出 妙用Javascript中apply、call、bind](https://www.cnblogs.com/coco1s/p/4833199.html)

MDN-javascript：

- [`Function.prototype.apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
- [`Function.prototype.call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

- [`Function.prototype.bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

