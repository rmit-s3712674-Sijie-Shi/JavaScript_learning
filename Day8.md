# JavaScript_learning

## Seventh_day

### Call back

loadScript('/my/script.js'); // 这个脚本有 "function newFunction() {…}"  

newFunction(); // 没有这个函数！  

function loadScript(src, callback) {  
  let script = document.createElement('script');  
  script.src = src;  
  
  script.onload = () => callback(script);  
  
  document.head.append(script);  
}
  
### Promise
let promise = new Promise(function(resolve, reject) {  
  // executor  
});  
传递给 new Promise 的函数被称为 executor。当 new Promise 被创建，executor 会自动运行。  
它的参数 resolve 和 reject 是由 JavaScript 自身提供的回调。我们的代码仅在 executor 的内部。  
由 new Promise 构造器返回的 promise 对象具有以下内部属性：  

state — 最初是 "pending"，然后在 resolve 被调用时变为 "fulfilled"，或者在 reject 被调用时变为 "rejected"。  
result — 最初是 undefined，然后在 resolve(value) 被调用时变为 value，或者在 reject(error) 被调用时变为 error。  
  
let promise = new Promise(function(resolve, reject) {  
  setTimeout(() => resolve("done!"), 1000); => NOT RETURN!!!!!!!  
});  
  
// resolve 运行 .then 中的第一个函数  
promise.then(  
  result => alert(result), // 1 秒后显示 "done!"  
  error => alert(error) // 不运行  
); 
  
let promise = new Promise(function(resolve, reject) {  
  setTimeout(() => reject(new Error("Whoops!")), 1000); => Only choose one can be executed, resolve or reject!!!!  
  resolve();
});  

// reject 运行 .then 中的第二个函数  
promise.then(  
  result => alert(result), // 不运行  
  error => alert(error) // 1 秒后显示 "Error: Whoops!"  
);  

2. 
function delay(ms) {  
  return new Promise(resolve, reject){
      setTimeout(() => resolve(), ms)  //setTimeout(resolve, ms)
  }
}  
  
delay(3000).then(() => alert('runs after 3 seconds'));  

1. 
new Promise(function(resolve, reject) {  
  setTimeout(() => {  
    throw new Error("Whoops!");  
  }, 1000);  
}).catch(alert); => catch will not work
  
new Promise(function(resolve, reject) {  
setTimeout(() => {  
reject(new Error("Whoops!"));  
}, 1000);  
}).catch(alert);  

### Promise API

#### promise all
let urls = [  
  'https://api.github.com/users/iliakan',  
  'https://api.github.com/users/remy',  
  'https://api.github.com/users/jeresig'  
];  
  
// 将每个 url 映射（map）到 fetch 的 promise 中  
let requests = urls.map(url => fetch(url));  
  
// Promise.all 等待所有任务都 resolved  
Promise.all(requests)  
  .then(responses => responses.forEach(  
    response => alert(`${response.url}: ${response.status}`)  
  ));  

  #### promise.allSettled

  let urls = [  
  'https://api.github.com/users/iliakan',  
  'https://api.github.com/users/remy',  
  'https://no-such-url'  
];  

Promise.allSettled(urls.map(url => fetch(url)))  
  .then(results => { // (*)  
    results.forEach((result, num) => {  
      if (result.status == "fulfilled") {  
        alert(`${urls[num]}: ${result.value.status}`);  
      }  
      if (result.status == "rejected") {  
        alert(`${urls[num]}: ${result.reason}`);  
      }  
    });  
  });  
result will be like:

[  
  {status: 'fulfilled', value: ...response...},  
  {status: 'fulfilled', value: ...response...},  
  {status: 'rejected', reason: ...error object...}  
]  
  
#### async
函数前面的关键字 async 有两个作用：  
  
让这个函数总是返回一个 promise。  
允许在该函数内使用 await。  

### import and export

#### export default

export class User {...} => import {User} from ...  
export default class User {...} => import User from ...

