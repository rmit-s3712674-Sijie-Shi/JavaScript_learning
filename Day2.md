# JavaScript_learning

## Second_day

### Array methods
# 把array变成map就能提出里面的东西了，还可以编辑每一项东西！！！！

#### Searching in array  
arr.indexOf() => the position of element  
arr.includes() => return true or false  
arr.find() => like let user = users.find(item => item.id == 1); to get the element that in item and has ID "1"  
arr.filter() => like let someUsers = users.filter(item => item.id < 3);  

#### Transform an array
truning array into map, and can use methods in map:  
let result = arr.map(item => item.length); => to get the length of each item in array  
sort array:  
let arr = [ 1, 2, 15 ];  
arr.sort(); => result will be 1, 15, 2  
In sort() function, sorting algrithm can be added,  
like:   
function compareNumeric(a, b) {  
  if (a > b) return 1;  
  if (a == b) return 0;  
  if (a < b) return -1;  
}  

let arr = [ 1, 2, 15 ];  

arr.sort(compareNumeric);  

alert(arr);  // 1, 2, 15  

or:  
arr.sort( (a, b) => a - b );  

split array:  
let arr = 'Bilbo, Gandalf, Nazgul, Saruman'.split(', ', 2);  

alert(arr); // Bilbo, Gandalf  

join array:  
let arr = ['Bilbo', 'Gandalf', 'Nazgul'];  

let str = arr.join(';'); // glue the array into a string using ;  

alert( str ); // Bilbo;Gandalf;Nazgul  

let arr = [1, 2, 3, 4, 5];  

let result = arr.reduce((sum, current) => sum + current, 0);  

alert(result); // 15  

also:  

let result = arr.reduce((sum, current) => sum - current); => result -13/if has initial 0, like (sum, current) => sum - current, 0 result will be -15  

#### Array.isArray
alert(typeof {}); // object  
alert(typeof []); // object  

alert(Array.isArray({})); // false  
alert(Array.isArray([])); // true  

#### test
1.  
function camelize(str){  
  let res = str.split('-')  
  let result = res.map((string, index)=>index == 0 ? string : string[0].toUpperCase()+ string.slice(1)).join('')  
  return result  
}  
2.  
use filter  
3.  
array.sort((a,b) => b- a)  
4.  
function copySorted(arr){
    let array = new Array  
    for (item of arr){  
        array = arr  
    }
    array.sort()  
    return array  
}
5.  
function Calculator() {  

    this.method = {  
      "+": (a,b) => a+b,  
      "-": (a,b) => a-b,  
    }  
    this.calculate = function calculate(input){  
      let split = input.split(" ")  
      let a = +split[0]  
      let operator = split[1]  
      let b = +split[2]  
      //这里要用this.method[operator]意义是属性名从operator获取，同理下面都是这个写法  
      if(!this.method[operator]){  
        return NaN  
      }else{  
        return this.method[operator](a,b)  
      }  
      
    };  
    this.addMethod = function addMethod(string,func){  
      return this.method[string] = func  
    }  

}  
let user = {  
  // ...
};  
function sayHifunc() {  
  alert("Hello!");  
};  
let sayHi = "sayHi"  
user[sayHi] = sayHifunc;  
user[sayHi](); // Hello!  
6.  


