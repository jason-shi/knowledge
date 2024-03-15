### 类究竟是个什么?
- Function 是一个内建类型.
- 类(class/function)是 Function 的实例(instance).
- 类使用 function 关键字来定义(实例化一个Function).
- 类的实例是用 new 关键字来创建: new.
~~~ javascript 
// 定义一个 Person 类
function Person(){
	// 在构造函数中初始化类的 Fields
	this.name = 'person';
	this.age = 10;
}
// 使用 prototype 初始化类的 Methods
Person.prototype.introduceSelf = function(){
	return `Hi, I'm ${this.name}, my age is ${this.age}.`;
}

// 查看Person是谁的实例
console.log(Person.constructor); // [Function: Function]
// 检查Person是否是Function的实例
console.log(Person instanceof Function); // true
console.log(Person.constructor == Function); // true
console.log(Person.__proto__ == Function.prototype); // true
console.log(Person.constructor == Function.prototype.constructor); // true
// 检查Person继承自谁
console.log(Person.prototype.__proto__.constructor); // [Function: Object]
// 检查Person是否继承自Object
console.log(Person.prototype.__proto__ == Object.prototype); // true

// 检查Person.prototype是否是Object的实例
console.log(Person.prototype instanceof Object); // true

~~~

### 如何实例化类, 类的实例究竟是个什么样的?
~~~ javascript 
// 实例化一个Person
let sjs = new Person();
// 检查sjs是谁的实例
console.log(sjs.constructor); // [Function: Person]
// 检查sjs是否是Person的实例
console.log(sjs instanceof Person); // true
console.log(sjs.constructor == Person); // true
console.log(sjs.__proto__ == Person.prototype); // true
console.log(sjs.constructor == Person.prototype.constructor); // true
// 检查sjs继承自谁
console.log(sjs.prototype); // undefined, sjs是实例，不是类

~~~

### 额外知识点
- 直接在Person中定义方法, 相当于C#定义的表态方法(static method), 如果要定义其实例能调用的方法, 则定义在 Person.prototype 中
``` js
// Person 的静态方法
Person.staticFunc = function(){
	// ...
}
// 直接调用表态方法
Person.staticFunc();
// Person 的实例方法
Person.prototype.instanceFunc = function(){
	this.name = "xxx";
}
// 实例化成员再调用实例方法
let person = new Person();

```

- 类的构造函数不要写返回值, 这样在使用 new 关键字实例化时, 才能正确的实例化此类; 如果函数中带返回值, 则 new 关键字实例化时, 会返回此函数的返回值.
``` js

// 定义一个带返回值的 function
function Foo() {
    this.name = 'this name';
    return {
        desc: 'return a object',
    };
}
// 调用 new Foo()
let foo = new Foo();
// 测试 foo 是个什么, 是否是 Foo 的实例
console.log(foo); // { desc: 'return a object' }
console.log(foo == Foo.prototype); // false
console.log(foo instanceof Foo); // false


```