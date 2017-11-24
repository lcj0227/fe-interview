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
```
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
* new一个实例内部发生了什么
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
* js函数节流和去抖动

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
