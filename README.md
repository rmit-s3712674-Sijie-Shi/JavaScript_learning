# JavaScript_learning

## First_day

### Syntactic sugar
语法糖: CoffeeScript

### Handbook
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference

### Compatibility
http://caniuse.com 

### Type attribute for JS
<script type=""></script>  
Nolonger in ues  
Also for language attributes  
<script language=""></script>  

### If include src attribute, inner code is invalid
Like: 
<script src="file.js">  
  alert(1); // 此内容会被忽略，因为设定了 src  
</script>  
Must write like:  
<script src="file.js"></script>  
<script>  
  alert(1);  
</script>  

### use strict
https://www.runoob.com/js/js-strict.html  

### BigInt type
if number > (2^53-1) or < -(2^53-1)  
// 尾部的 "n" 表示这是一个 BigInt 类型  
const bigInt = 1234567890123456789012345678901234567890n;  

### alert is a kind of modal
Same as Modal component  

### prompt
let age = prompt('How old are you?', 100);  
Will first show a modal that has an input column which has the number of 100  

### confirm
A modal with yes or no, returns true or false  

### Type change
Number(true) => 1  
Number(false) => 0  
Boolean(1) => true  
Boolean(0) => false  

### Remainder %
5 % 2 => 1  
8 % 3 => 2  

### Exponentiation **
2 ** 2 = 4  
2 ** 3 = 8  
2 ** 4 = 16  
4 ** (1/2) = 2  
8 ** (1/3) = 2  

### Unary +
Change the operand(操作数) to number  
+true = 1  
+"" = 0  

### compare
alert( null === undefined ); // false  
alert( null == undefined ); // true  

### null vs 0
alert( null > 0 );  // (1) false  
alert( null == 0 ); // (2) false  
alert( null >= 0 ); // (3) true  

### undefined vs 0
alert( undefined > 0 ); // false (1) => undefined transferred to NaN  
alert( undefined < 0 ); // false (2) => undefined transferred to NaN  
alert( undefined == 0 ); // false (3) => undefined only equals to null  

### if and ?
let age = prompt('age?', 18);  

let message = (age < 3) ? 'Hi, baby!' :  
  (age < 18) ? 'Hello!' :  
  (age < 100) ? 'Greetings!' :  
  'What an unusual age!';  

alert( message );  

if (age < 3) {  
  message = 'Hi, baby!';  
} else if (age < 18) {  
  message = 'Hello!';  
} else if (age < 100) {  
  message = 'Greetings!';  
} else {  
  message = 'What an unusual age!';  
}  

### ||
一个或运算 "||" 的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。  

let firstName = "";  
let lastName = "";  
let nickName = "SuperCoder";  

alert( firstName || lastName || nickName || "Anonymous"); // SuperCoder  

### &&
当两个操作数都是真值，与操作返回 true，否则返回 false  
与运算符返回第一个假值，如果没有假值就返回最后一个值  
The precedence of AND && is higher than ||, so it executes first.

### !
!! will convert value to boolean 

### ??
let firstName = null;  
let lastName = null;  
let nickName = "Supercoder";  

// 显示第一个不是 null/undefined 的值  
alert(firstName ?? lastName ?? nickName ?? "Anonymous"); // Supercoder  
重要的区别是：  

|| 返回第一个 真值。  
?? 返回第一个 已定义的值。  

let height = 0;  

alert(height || 100); // 100  
alert(height ?? 100); // 0  

precedence is very low, a bit higher than ? and =  

### label for break and continue in for loop

labelName: for(;;){  
    for(;;){  
       if() break labelName   => jump outof the first for loop directly
    }  
}  

### Object
let user = new Object() => let user = {}  
  
const user = {
    name: "..."
    "like bird": false  
}  
user.name = "...." => it's ok even user is const  
user = {...} => it's not eligible  
user["like bird"] = true; delete user["like bird"] => needs brackets  
  
let key = "name"
alert( user[key] );=>right  
alert( user.key );=>wrong  

let user = {  
    name, => the same as name:name  
    age:30  
}  
  
let key = "age"    
key in user => true. 

#### Object referencing, copying
Referencing:  
let user = { name: "mm" };
let admin = user;
Now, if change the admin.name to John, the name in user will be John, and user === admin as well  

Copying:  
let user = { name: "mm", age: 30 };  
let clone = {};  
for(let key in user){ clone[key] = user[key] };  
Now change clone.name does not interfere user.name  

Deep copying:  
Use to copy objects like:  
let user = {  
     name: {  
         firstName: 'John',  
         secondName: 'Smith'  
     }  
     age: 30 
}  
https://lodash.com/docs/4.17.15#cloneDeep  

#### Hint
Only three kinds of hints: string, number, default  
let user = {  
  name: "John",  
  money: 1000,  
  
  [Symbol.toPrimitive](hint) {  
    alert(`hint: ${hint}`);  
    return hint == "string" ? `{name: "${this.name}"}` : this.money;  
  }  
};  
  
alert(user); // hint: string -> {name: "John"}  
alert(+user); // hint: number -> 1000  
alert(user + 500); // hint: default -> 1500  

### Data type
#### Methods of primitives
基本类型不是对象。   
基本类型不能存储数据。  
所有的属性/方法操作都是在临时对象的帮助下执行的。  
null和undefined是原始类型，但没有对应‘对象包装器’  
一个函数可以作为一个属性存储到相应的对象中，但原始类型不具有此种功能，不能存储额外数据  

So:   
let str = "Hello";  

str.test = 5;  

alert(str.test);  
can't run, because the str is basic data type, not an object  
#### Number type
1 billion = 1e9 => 1 and 9 zeros following by  
0.001 = 1e-3 => 3 zeros behind 1  
let num = 255  
num.toString(16) => ff  
num.toString(2) => 11111111  

123456..toString(36) => not 123456.toString(36), can be (123456).toString(36)  
num.toFixed(1) => remain the last one number after dot, 四舍五入  

alert( parseFloat('12.3.4') ); // 12.3  
alert( parseInt('100px') ); // 100  
alert( parseInt('0xff', 16) ); // 255  
alert( parseInt('ff', 16) ); // 255  

isFinite to transfer to number then test if it is number  
isNaN to transfer to number then test if it is NaN 


|       | Math.floor    | Math.ceil     |  Math.round    |  Math.trunc  |  
| ---------- | :-----------:  | :-----------: | :-----------: | :-----------: |  
| 3.1     | 3     |4     | 3     | 3     |   
| 3.1     | 3     | 4     | 4     | 3     |   
| 3.1     | -2     | -1     | -1    | -1     |   
| 3.1     | -2     | -1     | -2     | -1     |
#### String
Base on the practices 

#### Array
对于栈来说，最后放进去的内容是最先接收的，也叫做 LIFO（Last-In-First-Out），即后进先出法则。而与队列相对应的叫做 FIFO（First-In-First-Out），即先进先出。  
push 在末端添加一个元素.  
pop 从末端取出一个元素.  
shift 取出队列首端的一个元素，整个队列往前移，这样原先排第二的元素现在排在了第一  
unshift Add element at the beginning  
  
for (let item of arr) 遍历数组  
for (let i in arr) — 永远不要用这个 => 这个提取的是key， like arr[i]  
arr.forEach() => iterate array

const numbers1 = [1, 2, 3, 4, 5];
const numbers2 = [ ...numbers1, 1, 2, 6,7,8]; // this will be [1, 2, 3, 4, 5, 1, 2, 6, 7, 8] => (...) also can be used in object https://www.techug.com/post/what-do-the-three-dots-mean-in-javascript.html
Also this can be considered as a replacement of arr.concat(arg1,arg2)  
let arr = [1, 2];  
let arrayLike = {  
  0: "something",  
  1: "else",  
  [Symbol.isConcatSpreadable]: true,  
  length: 2  
};  
alert( arr.concat(arrayLike) ); // 1,2,something,else  





