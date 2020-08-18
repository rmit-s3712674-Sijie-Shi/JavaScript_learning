# JavaScript_learning

## Fifth_day

### Recursion

let company = { // 是同一个对象，简洁起见被压缩了  
  sales: [{name: 'John', salary: 1000}, {name: 'Alice', salary: 1600 }],  
  development: {  
    sites: [{name: 'Peter', salary: 2000}, {name: 'Alex', salary: 1800 }],  
    internals: [{name: 'Jack', salary: 1300}]  
  }  
};  

// 用来完成任务的函数  
function sumSalaries(department) {  
  if (Array.isArray(department)) { // 情况（1）  
    return department.reduce((prev, current) => prev + current.salary, 0); // 求数组的和  
  } else { // 情况（2）  
    let sum = 0;  
    for (let subdep of Object.values(department)) {  
      sum += sumSalaries(subdep); // 递归调用所有子部门，对结果求和  
    }  
    return sum;  
  }  
}  

alert(sumSalaries(company)); // 7700  

### List
let list = {  
  value: 1,  
  next: {  
    value: 2,  
    next: {  
      value: 3,  
      next: {  
        value: 4,  
        next: null  
      }  
    }  
  }  
};  

#### print the list
function printList(list) {  
    alert (list.value)  
if(list.next){  
        printList(list.next)  
    }  
}  

#### reverse print
function printList(list) {      
if(list.next){  
        printList(list.next)  
    }  
    alert (list.value)  
}  

### Rest and spread

#### Rest

function sum(a, b) {  
  return a + b;  
}  

alert( sum(1, 2, 3, 4, 5) ); // only shows 3 => 1+2

function sumAll(...args) { // 数组名为 args
  let sum = 0;  

  for (let arg of args) sum += arg;  

  return sum;  
}

alert( sumAll(1) ); // 1  
alert( sumAll(1, 2) ); // 3  
alert( sumAll(1, 2, 3) ); // 6  
  
...rest 必须处在最后  

#### Spread
let arr1 = [1, -2, 3, 4];  
let arr2 = [8, 3, -8, 1];  

alert( Math.max(1, ...arr1, 2, ...arr2, 25) ); // 25  
  

let arr = [3, 5, 1];  
let arr2 = [8, 9, 15];  

let merged = [0, ...arr, 2, ...arr2];  

alert(merged); // 0,3,5,1,2,8,9,15（0，然后是 arr，然后是 2，然后是 arr2） 

copy array:  
let arr = [1, 2, 3];
let arrCopy = [...arr];  

### Closure
A closure is a function that remembers its outer variables and can access them. In some languages, that’s not possible, or a function should be written in a special way to make it happen. But as explained above, in JavaScript, all functions are naturally closures (there is only one exception, to be covered in The "new Function" syntax).  

1. 
function sum(a) {  

  return function(b) {=>为了使第二个括号有效，第一个（括号）必须返回一个函数。  
    return a + b; // 从外部词法环境获得 "a"  
  };  

}  

alert( sum(1)(2) ); // 3  
alert( sum(5)(-1) ); // 4  

2.  
let users = [  
  { name: "John", age: 20, surname: "Johnson" },  
  { name: "Pete", age: 18, surname: "Peterson" },  
  { name: "Ann", age: 19, surname: "Hathaway" }  
];  
  
// 通过 name (Ann, John, Pete)  
users.sort((a, b) => a.name > b.name ? 1 : -1);  
   
// 通过 age (Pete, Ann, John)  
users.sort((a, b) => a.age > b.age ? 1 : -1);  
  
users.sort(byField('name'));  
users.sort(byField('age'));  
  
function byField(fieldName){  
  return (a, b) => a[fieldName] > b[fieldName] ? 1 : -1;  
}  
