# JavaScript_learning

## Fourth_day

### Destructuring assignment

#### Array destructuring

let arr = ["Ilya", "Kantor"]  

// destructuring assignment  
// sets firstName = arr[0]  
// and surname = arr[1]  
let [firstName, surname] = arr;  

alert(firstName); // Ilya  
alert(surname);  // Kantor  
  
let user = {};  
[user.name, user.surname] = "Ilya Kantor".split(' ');  

alert(user.name); // Ilya  
  
let user = {  
  name: "John",  
  age: 30  
};  

// loop over keys-and-values  
for (let [key, value] of Object.entries(user)) {  
  alert(`${key}:${value}`); // name:John, then age:30  
}  
  
let user = new Map();  
user.set("name", "John");  
user.set("age", "30");  

for (let [key, value] of user) {  
  alert(`${key}:${value}`); // name:John, then age:30  
}  
  
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];  

alert(name1); // Julius  
alert(name2); // Caesar  

// Note that type of `rest` is Array.  
alert(rest[0]); // Consul  
alert(rest[1]); // of the Roman Republic  
alert(rest.length); // 2  
  
// runs only prompt for surname  
let [name = prompt('name?'), surname = prompt('surname?')] = ["Julius"];  
  
alert(name);    // Julius (from array)  
alert(surname); // whatever prompt gets  
  
#### Object destructuring
let options = {  
  title: "Menu",  
  width: 100,  
  height: 200  
};  

let {title, width, height} = options;  

alert(title);  // Menu  
alert(width);  // 100  
alert(height); // 200  
  
let options = {  
  title: "Menu",  
  width: 100,  
  height: 200  
};  

// { sourceProperty: targetVariable }  
let {width: w, height: h, title} = options;  
  
// width -> w  
// height -> h  
// title -> title  
  
alert(title);  // Menu  
alert(w);      // 100  
alert(h);      // 200  
  
let options = {  
  title: "Menu"  
};  
  
let {width = prompt("width?"), title = prompt("title?")} = options;  
  
alert(title);  // Menu  
alert(width);  // (whatever the result of prompt is)  
  
2.  
function topSalary(salaries) {  
  
  let max = 0;  
  let maxName = null;  
  
  for(let [name, salary] of Object.entries(salaries)) {  
    if (max < salary) {  
      max = salary;  
      maxName = name;  
    }  
  }  
  
  return maxName;  
}
  
### Date and time
#### Create date
new Date(year, month, date, hours, minutes, seconds, ms)  

year 必须是四位数：2013 是合法的，98 是不合法的。  
month 计数从 0（一月）开始，到 11（十二月）结束。    
date 是当月的具体某一天，如果缺失，则为默认值 1。  
如果 hours/minutes/seconds/ms 缺失，则均为默认值 0。  
  
getFullYear()  
获取年份（4 位数）  
getMonth()  
获取月份，从 0 到 11。  
getDate()  
获取当月的具体日期，从 1 到 31，这个方法名称可能看起来有些令人疑惑。  
getHours()，getMinutes()，getSeconds()，getMilliseconds()  
获取相应的时间组件。  
getDay()  
获取一周中的第几天，从 0（星期日）到 6（星期六）。  
当然，也有与当地时区的 UTC 对应项，它们会返回基于 UTC+0 时区的日、月、年等：getUTCFullYear()，getUTCMonth()，getUTCDay()。  
getTime()  
返回日期的时间戳 —— 从 1970-1-1 00:00:00 UTC+0 开始到现在所经过的毫秒数。  

### JSON, toJSON
JSON.stringify 将对象转换为 JSON。  
JSON.parse 将 JSON 转换回对象。    
字符串使用双引号。JSON 中没有单引号或反引号。所以 'John' 被转换为 "John"。  
对象属性名称也是双引号的。这是强制性的。所以 age:30 被转换成 "age":30。 

#### JSON.stringify
let json = JSON.stringify(value[, replacer, space])  
let room = {  
  number: 23  
};  

let meetup = {  
  title: "Conference",  
  participants: [{name: "John"}, {name: "Alice"}],  
  place: room // meetup 引用了 room  
};  

room.occupiedBy = meetup; // room 引用了 meetup  

alert( JSON.stringify(meetup, ['title', 'participants']) );  
// {"title":"Conference","participants":[{},{}]}   
  
JSON.stringify 也可以应用于原始（primitive）数据类型。  
JSON 支持以下数据类型：
Objects { ... }  
Arrays [ ... ]  
Primitives：  
strings，  
numbers，  
boolean values true/false，  
null。  
跳过：  
函数属性（方法）。  
Symbol 类型的属性。  
存储 undefined 的属性。  

#### JSON.parse
let value = JSON.parse(str, [reviver]);  
reviver:  
可选的函数 function(key,value)，该函数将为每个 (key, value) 对调用，并可以对值进行转换。  
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';  

let meetup = JSON.parse(str, function(key, value) {  
  if (key == 'date') return new Date(value);  
  return value;  
});  

alert( meetup.date.getDate() ); // 现在正常运行了！=> Or, getDate is not a function  
  