# JavaScript_learning

## Seventh_day

### Prototype inheritance

#### prototype
let animal = {  
  eats: true  
};  
let rabbit = {  
  jumps: true  
};  

rabbit.__proto__ = animal; // (*)  
   
// 现在这两个属性我们都能在 rabbit 中找到：  
alert( rabbit.eats ); // true (**)  
alert( rabbit.jumps ); // true  
  
let animal = {  
  eats: true,  
  walk() {  
    alert("Animal walk");  
  }  
};  
  
let rabbit = {  
  jumps: true,  
  __proto__: animal  
};  
  
let longEar = {  
  earLength: 10,  
  __proto__: rabbit  
};  
  
// walk 是通过原型链获得的  
longEar.walk(); // Animal walk  
alert(longEar.jumps); // true（从 rabbit）  
  
let user = {  
  name: "John",  
  surname: "Smith",  
  
  set fullName(value) {  
    [this.name, this.surname] = value.split(" ");  => remember this usage
  },  
  
  get fullName() {  
    return `${this.name} ${this.surname}`;  
  }  
};  

let admin = {  
  __proto__: user,  
  isAdmin: true  
};  

alert(admin.fullName); // John Smith (*)  
  
// setter triggers!  
admin.fullName = "Alice Cooper"; // (**)  
  
for..in 循环在其自身和继承的属性上进行迭代。所有其他的键/值获取方法仅对对象本身起作用。  
Object.keys 只返回自己的 key  

### F.prototype
let animal = {  
  eats: true  
};  

function Rabbit(name) {  
  this.name = name;  
}  

Rabbit.prototype = animal;  

let rabbit = new Rabbit("White Rabbit"); //  rabbit.__proto__ == animal  

alert( rabbit.eats ); // true  

  
### Class

#### Class syntactic

class User {  
  
  constructor(name) {  
    this.name = name;  
  }  
  
  sayHi() {   
    alert(this.name);  
  }  
  
}  

// 用法：  
let user = new User("John");  
user.sayHi();  

#### compute name

class User {  
  
  ['say' + 'Hi']() {  
    alert("Hello");  
  }  
  
}  

new User().sayHi();  

#### Override

class Animal {  
  name = 'animal'  //..change to showName(){alert("animal)}
  
  constructor() {  
    alert(this.name); // (*)  
  }  
}  
  
class Rabbit extends Animal {  
  name = 'rabbit';  //..change to showName(){alert("rabbit")}
}  
  
new Animal(); // animal  
new Rabbit(); // animal =>parent constructor always uses its own field value, not the overridden one.  
  
#### Super
class Animal {  
  
  constructor(name) {  
    this.speed = 0;  
    this.name = name;  
  }  
  
  // ...
}  

class Rabbit extends Animal {  
  
  constructor(name, earLength) {  
    super(name);  
    this.earLength = earLength;  
  }  

  // ...
}  
  
// 现在可以了  
let rabbit = new Rabbit("White Rabbit", 10);  
alert(rabbit.name); // White Rabbit  
alert(rabbit.earLength); // 10  
  
#### protected and read only

class CoffeeMachine {  
  _waterAmount = 0;  
  
  set waterAmount(value) {  //if no setter
    if (value < 0) throw new Error("Negative water");  
    this._waterAmount = value;  
  }  
  
  get waterAmount() {  
    return this._waterAmount;  
  }  
  
  constructor(power) {  
    this._power = power;  
  }  
  
}  

// 创建咖啡机  
let coffeeMachine = new CoffeeMachine(100);  

// 加水  
coffeeMachine.waterAmount = -10; // Error: Negative water  // if no setter, this is error  

or like:  
setWaterAmount(){}  
getWaterAmount(){}

#### instanceof

class Rabbit {}  
let rabbit = new Rabbit();  

// rabbit 是 Rabbit class 的对象吗？  
alert( rabbit instanceof Rabbit ); // true  

let arr = [1, 2, 3];  
alert( arr instanceof Array ); // true  
alert( arr instanceof Object ); // true  

#### mixin
 
let sayMixin = {  
  say(phrase) {  
    alert(phrase);  
  }  
};  
  
let sayHiMixin = {  
  __proto__: sayMixin, // (或者，我们可以在这儿使用 Object.create 来设置原型)  
  
  sayHi() {  
    // 调用父类方法  
    super.say(`Hello ${this.name}`); // (*)  
  },  
  sayBye() {  
    super.say(`Bye ${this.name}`); // (*)  
  }  
};  
  
class User {  
  constructor(name) {  
    this.name = name;  
  }  
}  
  
// 拷贝方法  
Object.assign(User.prototype, sayHiMixin);  
  
// 现在 User 可以打招呼了  
new User("Dude").sayHi(); // Hello Dude!  
  
