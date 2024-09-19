## 回调
``` javascript
function loadScript(src) {
  // 创建一个 <script> 标签，并将其附加到页面
  // 这将使得具有给定 src 的脚本开始加载，并在加载完成后运行
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}
loadScript('path/to/script.js');
// 其他代码可以立即运行
```
其他代码可以立即运行，因为脚本加载是异步的，所以它不会阻止其他脚本的加载。
假如我们想在脚本加载完成后执行一些代码，我们可以将这些代码作为回调函数传递给 loadScript，这样我们就可以确保它们在脚本加载完成后运行：
``` javascript
function loadScript(src, callback) {
  let script = document.createElement('script');
    script.src
    = src;
    script.onload = () => callback(script);
    document.head.append(script);
}
loadScript('path/to/script.js', script => { alert(`Cool, the ${script.src} is loaded`); });
```

### 回调地狱
乍一看，它像是一种可行的异步编程方式。的确如此，对于一个或两个嵌套的调用看起来还不错。但是，当我们有多个异步调用时，代码就会变得难以阅读和维护。
嵌套调用的“金字塔”随着每个异步行为会向右增长。很快它就失控了。所以这种编码方式不是很好。可以通过使每个行为都成为一个独立的函数来尝试减轻这种问题
``` javascript
loadScript('1.js', step1);

function step1(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadScript('2.js', step2);
  }
}

function step2(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadScript('3.js', step3);
  }
}

function step3(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...加载完所有脚本后继续 (*)
  }
}
```





## Promise 函数

### executer
1. 传递给 new Promise 的函数被称为 executor。当 new Promise 被创建，executor 会自动运行。它包含最终应产出结果的生产者代码。
2. executor 的参数 resolve 和 reject 是 JavaScript 引擎提供的两个回调函数。
    + resolve(value) —  如果任务成功完成并带有结果
    + reject(error) — 如果出现了错误，error就是返回的错误
3. executor 会自动运行并尝试执行一项工作。尝试结束后，如果成功则调用 resolve，如果出现 error 则调用 reject。
4. 构造器返回的 promise 对象具有以下内部属性：
    + state — 初始值为 "pending"，然后变为 "fulfilled" 或 "rejected"。
    + result — 初始值为 undefined，然后变为 value 或 error。
5. executor 应该执行一项工作，然后调用 resolve 或 reject 来改变对应的 promise 对象的状态。**executor 只能调用一个 'resolve' 或一个 'reject'。**任何状态的更改都是最终的。所有其他的再对 'resolve' 或一个 'reject' 的调用都会被忽略：

6. reject的参数可以是任何值，就像resolve一样， 建议使用是一个 Error 对象，或者继承自 Error 的对象。

### then
`.then` 的第一个参数是一个函数，该函数将在 promise resolved 且接收到结果后执行。
`.then` 的第二个参数也是一个函数，该函数将在 promise rejected 且接收到 error 信息后执行。
 例子：
```javascript
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve("done!"), 1000);
});

// resolve 运行 .then 中的第一个函数
promise.then(
  result => alert(result), // 1 秒后显示 "done!"
  error => alert(error) // 不运行
);
```
```javascript
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});
// reject 运行 .then 中的第二个函数
promise.then(
  result => alert(result), // 不运行
  error => alert(error) // 1 秒后显示 "Error: Whoops!"
);
```
如果我们只对成功完成的情况感兴趣，那么我们可以只为 .then 提供一个函数参数：
```javascript
let promise = new Promise(resolve => {
  setTimeout(() => resolve("done!"), 1000);
});
promise.then(alert); // 1 秒后显示 "done!"
```
如果我们只对 error 感兴趣，那么我们可以使用 null 作为第一个参数：.then(null, errorHandlingFunction)。或者我们也可以使用 .catch(errorHandlingFunction)，其实是一样的
```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("Whoops!")), 1000);
});

// .catch(f) 与 promise.then(null, f) 一样
promise.catch(alert); // 1 秒后显示 "Error: Whoops!"
```

### finally
+ finally 处理程序没有得到前一个处理程序的结果（它没有参数）。而这个结果被传递给了下一个合适的处理程序。
+ 如果 finally 处理程序返回了一些内容，那么这些内容会被忽略。
+ 当 finally 抛出 error 时，执行将转到最近的 error 的处理程序。

### 附加处理程序
如果 promise 为 pending 状态，.then/catch/finally 处理程序（handler）将等待它的结果。
但是如果 promise 已经 settled，那么处理程序将会立即执行。





## Promise 链

1. 例子
```javascript
new Promise(function(resolve, reject) {
  setTimeout(() => resolve(1), 1000); // (*)
}).then(function(result) { // (**)
  alert(result); // 1
  return result * 2;
}).then(function(result) { // (***)
  alert(result); // 2
  return result * 2;
}).then(function(result) {
  alert(result); // 4
  return result * 2;
});
// 初始 promise 在 1 秒后 resolve (*)，然后 .then 处理程序被调用 (**)，
// 它又创建了一个新的 promise（以 2 作为值 resolve）。下一个 then (***) 
// 得到了前一个 then 的值，对该值进行处理（*2）并将其传递给下一个处理程序。
```

2. 简化
```javascript
function loadScript(src) {
  return new Promise(function(resolve, reject) {
    let script = document.createElement('script');
    script.src = src;
    script.onload = () => resolve(script);
    script.onerror = () => reject(new Error(`Script load error for ${src}`));
    document.head.append(script);
  });
}
loadScript("/article/promise-chaining/one.js")
  .then(script => loadScript("/article/promise-chaining/two.js"))
  .then(script => loadScript("/article/promise-chaining/three.js"))
  .then(script => {
    // 脚本加载完成，我们可以在这儿使用脚本中声明的函数
    one();
    two();
    three();
  });
```

3. 返回 promise 或者 thenable 对象
如果处理程序返回一个 promise，那么下一个 then 将等待其完成。
如果处理程序返回一个 thenable 对象，那么它将被自动包装为 promise 并等待其完成。

注意点：
** promise.then(f1).catch(f2); 与 promise.then(f1, f2); 是不一样的。**
promise.then(f1).catch(f2); 会捕获 f1 中的错误,error 会传递到 f2 中。


