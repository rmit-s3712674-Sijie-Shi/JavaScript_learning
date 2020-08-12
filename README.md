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


