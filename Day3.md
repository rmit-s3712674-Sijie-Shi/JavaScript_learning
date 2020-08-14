# JavaScript_learning

## Third_day

### Iterable object

One method to get all value from object:  
let  o = {  
  'name': 'huixisheng',  
  'mail': 'huixisheng@gmial.com'  
};  
Object.values(o); // ['huixisheng', 'huixisheng@gmial.com']  
https://huixisheng.github.io/object-loop/  
#### Symbol.iterator
let range = {  
  from: 1,  
  to: 5  
};  

// 1. for..of 调用首先会调用这个：  
range[Symbol.iterator] = function() {  

  // ……它返回迭代器对象（iterator object）：  
  // 2. 接下来，for..of 仅与此迭代器一起工作，要求它提供下一个值  
  return {  
    current: this.from,  
    last: this.to,  

    // 3. next() 在 for..of 的每一轮循环迭代中被调用  
    next() {  
      // 4. 它将会返回 {done:.., value :...} 格式的对象  
      if (this.current <= this.last) {  
        return { done: false, value: this.current++ };  
      } else {  
        return { done: true };  
      }  
    }  
  };  
};  

// 现在它可以运行了！  
for (let num of range) {  
  alert(num); // 1, 然后是 2, 3, 4, 5  
}  

#### Array.from
let arrayLike = {  
  0: "Hello",  
  1: "World",  
  length: 2  
};  

let arr = Array.from(arrayLike); // (*)  
alert(arr.pop()); // World（pop 方法有效）  

let str = '𝒳😂';  

// 将 str 拆分为字符数组  
let chars = Array.from(str);  

alert(chars[0]); // 𝒳  
alert(chars[1]); // 😂  
alert(chars.length); // 2  

const length = 3;  
const init   = 0;  
const result = Array.from({ length }, () => init);  

result; // => [0, 0, 0]  

const length = 3;  
const init   = 0;  
const result = Array(length).fill(init);  

fillArray2(0, 3); // => [0, 0, 0]  
https://juejin.im/post/6844903926823649293  
### Map

new Map() —— 创建 map。  
map.set(key, value) —— 根据键存储值。  
map.get(key) —— 根据键来返回值，如果 map 中不存在对应的 key，则返回 undefined。  
map.has(key) —— 如果 key 存在则返回 true，否则返回 false。  
map.delete(key) —— 删除指定键的值。  
map.clear() —— 清空 map。  
map.size —— 返回当前元素个数。 
   
map.set('1', 'str1')  
  .set(1, 'num1')  
  .set(true, 'bool1');  
#### iterate
let recipeMap = new Map([  
  ['cucumber', 500],  
  ['tomatoes', 350],  
  ['onion',    50]  
]);

// 遍历所有的键（vegetables）  
for (let vegetable of recipeMap.keys()) {  
  alert(vegetable); // cucumber, tomatoes, onion  
}  

// 遍历所有的值（amounts）  
for (let amount of recipeMap.values()) {  
  alert(amount); // 500, 350, 50  
}  

// 遍历所有的实体 [key, value]  
for (let entry of recipeMap) { // 与 recipeMap.entries() 相同  
  alert(entry); // cucumber,500 (and so on)  
}  

recipeMap.forEach( (value, key, map) => {  
  alert(`${key}: ${value}`); // cucumber: 500 etc  
});  
#### Create map from object
let obj = {  
  name: "John",  
  age: 30  
};  

let map = new Map(Object.entries(obj));  

alert( map.get('name') ); // John  
#### create object from map
let map = new Map();  
map.set('banana', 1);  
map.set('orange', 2);  
map.set('meat', 4);  
let obj = Object.fromEntries(map);  

### set
new Set(iterable) —— 创建一个 set，如果提供了一个 iterable 对象（通常是数组），将会从数组里面复制值到 set 中。  
set.add(value) —— 添加一个值，返回 set 本身  
set.delete(value) —— 删除值，如果 value 在这个方法调用的时候存在则返回 true ，否则返回 false。  
set.has(value) —— 如果 value 在 set 中，返回 true，否则返回 false。  
set.clear() —— 清空 set。  
set.size —— 返回元素个数。  

Because set has no key, to iterate it, only can use forEach and for...of  
Also, set has:  
set.keys() —— 遍历并返回所有的值（returns an iterable object for values），  
set.values() —— 与 set.keys() 作用相同，这是为了兼容 Map，  
set.entries() —— 遍历并返回所有的实体（returns an iterable object for entries） [value, value]，它的存在也是为了兼容 Map。  

