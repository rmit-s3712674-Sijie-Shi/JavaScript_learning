# JavaScript_learning

## Second_day

### Array methods


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

