## javascript部分
### 1、 深拷贝与浅拷贝

浅拷贝是指仅仅复制对象的引用，而不是复制对象本身；深拷贝则是把复制对象所引用的全部对象都复制一遍。
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


* 移动端适配
* 组件封装、对组件的看法、如何抽象一个组件

* 观察者模式
* 父子组件通信
* 闭包
* js原型继承
* call，apply，bind
* 如何判断一个对象是否是数组


* 事件代理的原理基本


* 事件委托
* 跨域
* new一个实例内部发生了什么
* 原型、原型链、继承


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

function idGenerator(len = 6) {
```


```
/**------- 编码题目二 --------- **/
   
   /**
    * 说明：数组去重合并
    * 输入：[1, 5, 3, 9], [1, 9, 2, 7, 5]
    * 输出：[1, 5, 3, 9, 2, 7]
    */
   
   function mergeArray(arr1,arr2) {
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
   
   
   
   
   
