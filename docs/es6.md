## es6部分

* 简要介绍es6
* promise
* ES6 let, const, promise, 解构，async, await
* var和let的区别，var作用域提升，let块级作用域
* 解构

### 1、[es6 必知必会 十道题](https://www.zhihu.com/people/wei-chang-ran/activities)

以下 promise 均指代 Promise 实例，环境是 Node.js。
* 题目一
```
const promise = new Promise((resolve, reject) => {
  console.log(1)
  resolve()
  console.log(2)
})
promise.then(() => {
  console.log(3)
})
console.log(4)
```
运行结果：1
```
2
4
3
```

解释：
```
Promise 构造函数是同步执行的，promise.then 中的函数是异步执行的。
```
* 题目二
```
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success')
  }, 1000)
})
const promise2 = promise1.then(() => {
  throw new Error('error!!!')
})

console.log('promise1', promise1)
console.log('promise2', promise2)

setTimeout(() => {
  console.log('promise1', promise1)
  console.log('promise2', promise2)
}, 2000)

```
运行结果：
```
promise1 Promise { <pending> }
promise2 Promise { <pending> }
(node:50928) UnhandledPromiseRejectionWarning: Unhandled promise rejection (rejection id: 1): Error: error!!!
(node:50928) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
promise1 Promise { 'success' }
promise2 Promise {
  <rejected> Error: error!!!
    at promise.then (...)
    at <anonymous> }
```
解释：
```
promise 有 3 种状态：pending、fulfilled 或 rejected。
状态改变只能是 pending->fulfilled 或者 pending->rejected，状态一旦改变则不能再变。
上面 promise2 并不是 promise1，而是返回的一个新的 Promise 实例。
```
* 题目三
```
const promise = new Promise((resolve, reject) => {
  resolve('success1')
  reject('error')
  resolve('success2')
})

promise
  .then((res) => {
    console.log('then: ', res)
  })
  .catch((err) => {
    console.log('catch: ', err)
  })
```
运行结果：
```
then: success1
```
解释：
```
构造函数中的 resolve 或 reject 只有第一次执行有效，多次调用没有任何作用，
呼应代码二结论：promise 状态一旦改变则不能再变。
```
* 题目四
```
Promise.resolve(1)
  .then((res) => {
    console.log(res)
    return 2
  })
  .catch((err) => {
    return 3
  })
  .then((res) => {
    console.log(res)
  })
```
运行结果：
```
1
2
```
解释：
```
promise 可以链式调用。提起链式调用我们通常会想到通过 return this 实现，
不过 Promise 并不是这样实现的。promise 每次调用 .then 或者 .catch
都会返回一个新的 promise，从而实现了链式调用。
```
* 题目五
```
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('once')
    resolve('success')
  }, 1000)
})

const start = Date.now()
promise.then((res) => {
  console.log(res, Date.now() - start)
})
promise.then((res) => {
  console.log(res, Date.now() - start)
})
```
运行结果：
```
once
success 1005
success 1007
```
解释：
```
promise 的 .then 或者 .catch 可以被调用多次，但这里 Promise 构造函数只执行一次。
或者说 promise 内部状态一经改变，并且有了一个值，
那么后续每次调用 .then 或者 .catch 都会直接拿到该值。
```
* 题目六
```
Promise.resolve()
  .then(() => {
    return new Error('error!!!')
  })
  .then((res) => {
    console.log('then: ', res)
  })
  .catch((err) => {
    console.log('catch: ', err)
  })
  ```
运行结果：
```angular2html
then: Error: error!!!
    at Promise.resolve.then (...)
    at ...
```
解释：
```angular2html
.then 或者 .catch 中 return 一个 error 对象并不会抛出错误，
所以不会被后续的 .catch 捕获，需要改成其中一种：
return Promise.reject(new Error('error!!!'))throw new Error('error!!!')
因为返回任意一个非 promise 的值都会被包裹成 promise 对象，
即 return new Error('error!!!') 等价于
 return Promise.resolve(new Error('error!!!'))。
```
* 题目七
```angular2html
const promise = Promise.resolve()
  .then(() => {
    return promise
  })
promise.catch(console.error)
```
运行结果：
```angular2html
TypeError: Chaining cycle detected for promise #<Promise>
    at <anonymous>
    at process._tickCallback (internal/process/next_tick.js:188:7)
    at Function.Module.runMain (module.js:667:11)
    at startup (bootstrap_node.js:187:16)
    at bootstrap_node.js:607:3
```
解释：
```angular2html
.then 或 .catch 返回的值不能是 promise 本身，否则会造成死循环。类似于：process.nextTick(function tick () {
  console.log('tick')
  process.nextTick(tick)
})
```
* 题目八
```angular2html
Promise.resolve(1)
  .then(2)
  .then(Promise.resolve(3))
  .then(console.log)
```
运行结果：
```angular2html
1
```
解释：
```angular2html
.then 或者 .catch 的参数期望是函数，传入非函数则会发生值穿透。
```
* 题目九
```angular2html
Promise.resolve()
  .then(function success (res) {
    throw new Error('error')
  }, function fail1 (e) {
    console.error('fail1: ', e)
  })
  .catch(function fail2 (e) {
    console.error('fail2: ', e)
  })
```
运行结果：
```angular2html
fail2: Error: error
    at success (...)
    at ...
```
解释：
```angular2html
.then 可以接收两个参数，第一个是处理成功的函数，第二个是处理错误的函数。
.catch 是 .then 第二个参数的简便写法，但是它们用法上有一点需要注意：
.then 的第二个处理错误的函数捕获不了第一个处理成功的函数抛出的错误，
而后续的 .catch 可以捕获之前的错误。当然以下代码也可以：

Promise.resolve()
  .then(function success1 (res) {
    throw new Error('error')
  }, function fail1 (e) {
    console.error('fail1: ', e)
  })
  .then(function success2 (res) {
  }, function fail2 (e) {
    console.error('fail2: ', e)
  })
```
* 题目十
```angular2html
process.nextTick(() => {
  console.log('nextTick')
})
Promise.resolve()
  .then(() => {
    console.log('then')
  })
setImmediate(() => {
  console.log('setImmediate')
})
console.log('end')
```
运行结果：
```angular2html
end
nextTick
then
setImmediate
```
解释：
```angular2html
process.nextTick 和 promise.then 都属于 microtask，
而 setImmediate 属于 macrotask，在事件循环的 check 阶段执行。
事件循环的每个阶段（macrotask）之间都会执行 microtask，
事件循环的开始会先执行一次 microtask。
```