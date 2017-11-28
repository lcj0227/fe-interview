## javascript部分
### 1、 深拷贝与浅拷贝

浅拷贝是指仅仅复制对象的引用，而不是复制对象本身；
深拷贝则是把复制对象所引用的全部对象都复制一遍。
```
function getType(obj){
       //tostring会返回对应不同的标签的构造函数
       var toString = Object.prototype.toString;
       var map = {
          '[object Boolean]'  : 'boolean', 
          '[object Number]'   : 'number', 
          '[object String]'   : 'string', 
          '[object Function]' : 'function', 
          '[object Array]'    : 'array', 
          '[object Date]'     : 'date', 
          '[object RegExp]'   : 'regExp', 
          '[object Undefined]': 'undefined',
          '[object Null]'     : 'null', 
          '[object Object]'   : 'object'
      };
      if(obj instanceof Element) {
           return 'element';
      }
      return map[toString.call(obj)];
   }
   
   
   function deepClone(data){
          var type = getType(data);
          var obj;
          if(type === 'array'){
              obj = [];
          } else if(type === 'object'){
              obj = {};
          } else {
              //不再具有下一层次
              return data;
          }
          if(type === 'array'){
              for(var i = 0, len = data.length; i < len; i++){
                  obj.push(deepClone(data[i]));
              }
          } else if(type === 'object'){
              for(var key in data){
                  obj[key] = deepClone(data[key]);
              }
          }
          return obj;
      }
```



### 2、函数柯里化实现

### 3、函数节流与去抖

### 4、```instanceof```与```typeof```，以及优缺点
* ```typeof```主要用来判断基本类型
```
   typeof 0   // return 'number'
   typeof '0'   //return 'string'，字符串同时也是一个类数组对象
   typeof false  // return 'boolean'
   function fn(){ }
   typeof fn   // return 'function'
   var param;
   typeof param   // return 'undefined'
   //ES6 新加入的类型
   typeof Symbol()  // 'symbol'
```
* ```typeof```不能区分出数组，null和普通对象，那么instanceof解决了这个问题
```angular2html
   //typeof
   typeof [1, 2, 3]  // return 'object'
   typeof null   // return 'object'
   typeof {x: 1}  // return 'object'
   
   //instanceof
   [1, 2, 3] instanceof Array  //return true
   null instanceof Object  // return false
   var obj = {}
   obj instanceof Object   // return true
   
```

### 5、引起内存泄漏的操作有哪些
```angular2html
1.全局变量引起
2.闭包引起
3.dom清空，事件未清除
4.子元素存在引用
5.被遗忘的计时器
```
参考：
[【译】JavaScript 内存泄漏问题](http://octman.com/blog/2016-06-28-four-types-of-leaks-in-your-javascript-code-and-how-to-get-rid-of-them/)、
[JavaScript 常见的内存泄漏原因](https://juejin.im/entry/58158abaa0bb9f005873a843)

* 移动端适配
* 组件封装、对组件的看法、如何抽象一个组件

* 观察者模式
* 父子组件通信
* 闭包
* call，apply，bind
* 如何判断一个对象是否是数组


### 事件代理的原理

* 事件代理就是说我们将事件添加到本来要添加事件的父节点，
将事件委托给父节点来触发处理函数，这通常会使用在大量的同级元素需要添加同一类事件的时候，
比如一个动态的非常多的列表，需要为每个列表项都添加 点击事件，这时可以使用事件代理，
通过判断e.target.nodeName来判断发生的具体元素，从而判断是否是在 列表项中触发，
这样的好处是可以减少事件绑定，同时动态的DOM结构仍然可以监听。事件代理发生在冒泡阶段。

参考：[事件代理](http://www.bubuko.com/infodetail-2290096.html)、[浅析JavaScript的事件代理和委托](https://yq.aliyun.com/articles/185645)

* 事件委托
* 跨域

### 原型、原型链、继承
* 我们知道在es6之前，js没有类和继承的概念，js是通过原型来实现继承的。
在js中一个构造函数默认自带有一个prototype属性， 这个的属性值是一个对象，
同时这个prototype对象自带有一个constructor属性，这个属性指向这个构造函数，
同时每一个实例 都有一个__proto__属性指向这个prototype对象，
我们可以将这个叫做隐式原型，我们在使用一个实例的方法的时候，
会先检查 这个实例中是否有这个方法，
没有则会继续向上查找这个prototype对象是否有这个方法，
刚刚我们说到prototype是一个对象，
那么也即是说这个是一个对象的实例，
那么这个对象同样也会有一个__proto__属性指向对象的prototype对象。


* 设计模式的了解、会用到哪些
* 柯里化，有什么应用
* 本地存储cookie和storage区别
* this的指向
### js函数节流和去抖动


 ```
/**------- 编码题目一 --------- **/

/**
 * 说明：生成一个指定长度（默认6位）的随机字符，随机字符包含字母数字。
 * 输入：输入随机字符长度，无输入默认6位
 * 输出：随机字符，如"6bij0v"
 */

function idGenerator(len = 6) {}
```


```
/**------- 编码题目二 --------- **/
   
   /**
    * 说明：数组去重合并
    * 输入：[1, 5, 3, 9], [1, 9, 2, 7, 5]
    * 输出：[1, 5, 3, 9, 2, 7]
    */
   
   function mergeArray(arr1,arr2) {}
```

```
/**
 * 说明：简单实现一个模板解析方案
 * 要求：
 * const tpl = '<input value="${value + 1}" />'
 * const html = render(tpl, {
 *   value: 1,
 * });
 * 输出 <input value="2" />
 */
function render(tpl,data){

```
   
   
  ### 可视化相关的问题
  比如在没写过图表的前提下，怎么抽象数据与图形的映射，怎么去组合不同的图表部件。
  
  有一块区域要展示一组数据，但数据需要请求 3 个接口才能计算得到，
  请问前端是怎么做的，如何优化，前端什么情况下可以放弃合并接口的要求。
  这个地方至少会考察到异步，本地缓存，延展下会问下并发，竞态，协程等。
  答得好不好完全在于你的知识面的深度和广度，能否一直让我延展下去
  
 
 
  ### 对js模块化的理解
  * 在ES6出现之前，js没有标准的模块化概念，
  这也就造成了js多人写作开发容易造成全局污染的情况，
  以前我们可能会采用立即执行 函数、对象等方式来尽量减少变量这种情况，
  后面社区为了解决这个问题陆续提出了AMD规范和CMD规范，
  这里不同于Node.js的 CommonJS的原因在于服务端所有的模块都是存在于硬盘中的，
  加载和读取几乎是不需要时间的，而浏览器端因为加载速度取决于网速，
  因此需要采用异步加载，AMD规范中使用define来定义一个模块，
  使用require方法来加载一个模块，现在ES6也推出了标准的模块 加载方案，
  通过exports和require来导出和导入模块。
  
  ### 如何实现一个JS的AMD模块加载器
  * AMD（[AMD (中文版)](https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88))）是解决JS模块化的规范，
  实现这样的一个模块加载器的关键在于解决每个模块依赖的解析。
  首先我们需要有一个模块的入口，也就是主模块，
  比如我们使用 一个use方法作为入口，之后以数组的形式列出了主模块的依赖，
  这时候我们要想到的是如何解析这一个一个的依赖，
  也就是如何解析出一个个js文件的绝对地址， 我们可以制定一个规则，
  如默认为主模块的路径为基准，也可以像requirejs一样
  使用一个config方法来指定一个baseurl和为每一个模块指定一个path，
  最后就是 模块的问题，我们需要暴露一个define方法来定义模块，也就是模块名，
  依赖以及每个模块的各自代码。其中每个模块的代码都应该在依赖加载完之后执行，
  这就是一个 回调函数，模块的依赖、回调函数、状态、名字、模块导出等
  可以看做是一个模块的属性，因此我们可以使用一个对象来保存所有的模块，
  然后每个模块的各个属性存放在一个对象中。 最后我们来考虑一下模块加载的问题，
  上面我们说到use方法，use方法的逻辑就是遍历依赖，然后对每个模块进行加载，
  也就是解析地址然后使用插入script，我们假设 使用loadModule方法来加载依赖，
  那么这个函数的逻辑就应该是检查我们的模块是否已经加载过来判断是否需要加载，
  如果这个模块还有依赖则调用use方法继续解析，模块依赖中我们 
  还没有提到的问题就是每个模块的依赖是需要被传进模块里来使用的，
  解决方法就是每个模块的callback方法执行后的返回的export记录下来
  然后使用apply之类的方法将这些参数传递进去。 大致就是这样子的。

[动手实现一个AMD模块加载器(一)](https://github.com/huruji/blog/issues/13)
[动手实现一个AMD模块加载器(二)](https://github.com/huruji/blog/issues/16)
[动手实现一个AMD模块加载器(三)](https://github.com/huruji/blog/issues/17)

### 使用new操作符实例化一个对象的具体步骤
* 1.构造一个新的对象
  
  2.将构造函数的作用域赋给新对象（也就是说this指向了新的对象）
  
  3.执行构造函数中的代码
  
  4.返回新对象

### 递归和迭代的区别是什么，各有什么优缺点？
```angular2html
 * 程序调用自身称为递归
 使用递归要注意的有两点:
    1)递归就是在过程或函数里面调用自身;
    2)在使用递归时,必须有一个明确的递归结束条件,称为递归出口.
 优点：大问题转化为小问题，可以减少代码量，同时应为代码精简，可读性好， 
 缺点：递归调用浪费了空间，而且递归太深容易造成堆栈的溢出，
      由于递归引起一系列的函数调用,并且有可能会有一系列的重复计算,
      递归算法的执行效率相对较低.。
```
```angular2html
 * 利用变量的原值推出新值称为迭代
 优点：代码运行效率好，因为时间只因循环次数增加而增加，而且没有额外的空间开销，
 缺点：代码不如递归简
```
  
  
  
  参考：
  * [1、深究递归和迭代的区别、联系、优缺点及实例对](http://blog.csdn.net/laoyang360/article/details/7855860)
  * [2、「递归」和「迭代」有哪些区别？](https://www.zhihu.com/question/20278387)
  

### 斐波那契数列

### 策略模式是什么，说一下你的理解？
* 策略模式就是说我们将一系列的算法封装起来，使其相互之间可以替换，
封装的算法具有一定的独立性，不会随客户端的变化而变化，
比较常见的使用常见就是类似于 表单验证这种多场景的情况，
我们使用策略模式就可以避免使用一堆的if...else。

### 什么是事件循环（EVENT LOOP）？
* 我们常常说js是单线程的，是指js执行引擎是单线程的，除了这个单线程，
还有一个 任务队列，在执行js代码的过程中，执行引擎遇到注册的延时方法，如定时器，DOM事件，
会将这些方法交给相应的浏览器模块处理，当这些延时方法有触发条件去触发的时候，
这些延时方法会被添加至任务队列，而这些任务队列中的方法只有js的主线程空闲了才会执行，
这也就是说我们常常用的定时器定的时间参数只是一个触发条件，
具体多少时间后执行其实还需要看 js主线程空闲与否

参考：
* [【转向Javascript系列】从setTimeout说事件循环模型](http://www.alloyteam.com/2015/10/turning-to-javascript-series-from-settimeout-said-the-event-loop-model/)
* [深入浅出Javascript事件循环机制(上)](https://zhuanlan.zhihu.com/p/26229293)
* [深入浅出JavaScript事件循环机制(下)](https://zhuanlan.zhihu.com/p/26238030)
* [并发模型与事件循环](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/EventLoop)

### 原生JS操作DOM的方法有哪些？
* 获取节点的方法:getElementById、getElementsByClassName、getElementsByTagName、getElementsByName、querySelector、querySelectorAll,
 对元素属性进行操作: getAttribute、 setAttribute、removeAttribute方法，
 对节点进行增删改:appendChild、insertBefore、replaceChild、removeChild、createElement等
  
### javascript做类型判断的方法有哪些？
* typeof、instanceof 、 Object.prototype.toString()


