# JavaScript_learning

## Sixth_day

### Function-object

#### Name attribute
function sayHi() {  
  alert("Hi");  
}  

alert(sayHi.name); // sayHi  

let user = {  
  
  sayHi() {  
    // ...  
  },  

  sayBye: function() {  
    // ...  
  }  

}  

alert(user.sayHi.name); // sayHi  
alert(user.sayBye.name); // sayBye  
  
#### Length_attribute

function f1(a) {}  
function f2(a, b) {}  
function many(a, b, ...more) {}  

alert(f1.length); // 1  
alert(f2.length); // 2  
alert(many.length); // 2 => rest is not counted  

#### Customise_attribute
function sayHi() {  
  alert("Hi");  
  sayHi.counter++;  
}  
sayHi.counter = 0;  

sayHi(); // Hi  
sayHi(); // Hi  

alert( `Called ${sayHi.counter} times` ); // Called 2 times  
Can replace closure.  
let count = 0  
function sayHi(){... count++}  

### Named Function Expression
let sayHi = function func(who) {  
  if (who) {  
    alert(`Hello, ${who}`);  
  } else {  
    func("Guest"); // 使用 func 再次调用函数自身  
  }  
};  
  
1. 
function makeCounter() {  
  let count = 0;  

  function counter() {  
    return count++;  
  }  

  counter.set = value => count = value;  

  counter.decrease = () => count--;  

  return counter;  
}
  
  let counter = makeCounter();  => why this calling makeCounter()//important
  
  alert( counter() ); // 0  
  alert( counter() ); // 1  
  
  counter.set(10); // set the new count  
  
  alert( counter() ); // 10  
  
  counter.decrease(); // decrease the count by 1  
  
  alert( counter() ); // 10 (instead of 11)  

  ### 装饰者模式和转发，call/apply

  function slow(x) {  
  // 这里可能会有重负载的 CPU 密集型工作  
  alert(`Called with ${x}`);  
  return x;  
}  

function cachingDecorator(func) {  
  let cache = new Map();  

  return function(x) {  
    if (cache.has(x)) {    // 如果缓存中有对应的结果  
      return cache.get(x); // 从缓存中读取结果  
    }  

    let result = func(x);  // 否则就调用 func  

    cache.set(x, result);  // 然后将结果缓存（记住）下来  
    return result;  
  };  
}  

slow = cachingDecorator(slow);  

alert( slow(1) ); // slow(1) 被缓存下来了  
alert( "Again: " + slow(1) ); // 一样的  

alert( slow(2) ); // slow(2) 被缓存下来了  
alert( "Again: " + slow(2) ); // 和前面一行结果相同  

  
// 我们将对 worker.slow 的结果进行缓存  
let worker = {  
  someMethod() {  
    return 1;  
  },  

  slow(x) {  
    // 可怕的 CPU 过载任务  
    alert("Called with " + x);  
    return x * this.someMethod(); // (*)  
  }  
};  

// 和之前例子中的代码相同  
function cachingDecorator(func) {  
  let cache = new Map();  
  return function(x) {  
    if (cache.has(x)) {  
      return cache.get(x);  
    }  
    let result = func(x); // (**)  => let result = func.call(this, x);  
    cache.set(x, result);  
    return result;  
  };  
}  

alert( worker.slow(1) ); // 原始方法有效  

worker.slow = cachingDecorator(worker.slow); // 现在对其进行缓存  

alert( worker.slow(2) ); // 蛤！Error: Cannot read property 'someMethod' of undefined  

In this case, 'this' is undefined, so needs to bind this with function.

If passing many parameters:  
let worker = {  
  slow(min, max) {  
    alert(`Called with ${min},${max}`);  
    return min + max;  
  }  
};  

function cachingDecorator(func, hash) {  
  let cache = new Map();  
  return function() {  
    let key = hash(arguments); // (*)  
    if (cache.has(key)) {  
      return cache.get(key);  
    }  

    let result = func.call(this, ...arguments); // (**)  

    cache.set(key, result);  
    return result;  
  };  
}  

function hash(args) {  
  return args[0] + ',' + args[1];  
}  

worker.slow = cachingDecorator(worker.slow, hash);  

alert( worker.slow(3, 5) ); // works  
alert( "Again " + worker.slow(3, 5) ); // same (cached)  
  
