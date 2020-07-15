---
title: JavaScript创建对象的几种方式
date: 2020-07-08 14:14:24
tags:
- 前端
- 前端面试题
- Object
- Create object
- JavaScript object
- 创建对象
category:
- [前端]
- [JavaScript]
---

## 理解对象

**何为对象？（Object）**

> ECMA-262把对象定义为：“无序属性的集合，其属性可以包含基本值、对象或者函数。”
> 严格来讲，对象是一组没有特定顺序的值。对象的每个属性或方法都有一个名字，而每个名字都映射到一个值，可以把`ECMAScript`的对象想象成散列表：无非就是一组名值对，其中值可以是数据或函数（*来源：JavaScript 高级程序设计 第3版*）

最简单的方式，创建一个Object的实例，然后再为它添加属性和方法，如下：

```javascript
var person = new Object(); // new了一个`Object`的实例对象并保存名为`person`的变量中
person.name = 'Chace'; // 给`person`对象添加了一个名为name的属性并赋值为字符串'Chace'
person.age = 18; // 给`person`对象添加了一个名为age的属性并赋值为数字18
person.job = 'Software Engineer'; // 给`person`对象添加了一个名为job的属性并赋值为字符串'Software Engineer'

person.sayName = function () {
  alert(this.name);
}; // 给person对象添加了一个名为`sayName()`的方法，这个方法用于显示`this.name`(将被解析为`person.name`)的值
```

## 创建对象

> 一般情况下，JS中创建对象的方式可以用构造函数`Object`或者对象字面量的方式，但需要创建几个具有相同属性或方法的对象时，就得写大量的冗余代码。故而出现了下述几种创建对象的方法。

### 使用对象字面量创建对象

对象字面量是对象定义的一种简写方式，目的在于简化创建包含大量属性的对象的过程

```javascript
var person = {
  name: 'Br3ad',
  gender: 'male',
  age: 18
};

console.log(person.name); // 'Br3ad'
console.log(person.gender); // 'male'
console.log(person.age); // 18
```

在使用对象字面量语法时，属性名也可以使用字符串，例子如下：

```javascript
var person = {
  "name": 'Br3ad',
  "gender": 'male',
  "age": 18
};

console.log(person); // {name: 'Br3ad', gender: 'male', age: 18}
```

另外，使用对象字面量语法时，如果留空其花括号，则可以定义只包含默认属性和方法的对象，例子如下：

```javascript
var person = {}; // 与 new Object() 相同
person.name = 'Br3ad';
person.gender = 'male';
person.age = 18;
```

**对象字面量的语法，推荐只在考虑对象名的可读性时使用。**

对象字面量创建方式也是向函数传递大量可选参数的首选方式，例如：

```javascript
function displayInfo(args) {
  var output = '';
  if (typeof args.name == 'string') {
    output += 'Name: ' + args.name + '\n';
  }
  if (typeof args.age == 'number') {
    output += 'Age：' + args.age + '\n';
  }
  console.log(output);
};

displayInfo({
  name: 'Nicholas',
  age: 18
});
// Name：Nicholas
// Age：18

displayInfo({
  name: 'Br3ad'
});
// Name：Br3ad
```

### 通过`new`操作符创建对象

使用`new`操作符创建并初始化一个新对象，关键字`new`后跟随一个`Object`构造函数，例子如下：

```javascript
var person = new Object(); // 创建一个空对象并保存在变量person中，和{}一样
person.name = 'Br3ad';
person.gender = 'male';
person.age = 18;

console.log(person.name); // 'Br3ad'
console.log(person.gender); // 'male'
console.log(person.age); // 18
```

JavaScript语言核心中的原始类型都包含内置构造函数，例如：

```javascript
var o = new Object(); // 创建一个空对象，和 {} 一样
var a = new Array(); // 创建一个空数组，和 [] 一样
var d = new Date(); // 创建一个表示当前时间的 Date 对象
var r = new RegExp('js'); // 创建一个可以进行模式匹配的 RegExp 对象
```

### 工厂模式（Factory pattern）

工厂模式是软件工程使用同一个接口创建很多对象，会产生大量的重复代码。为了解决这个问题，开始使用工厂模式的一种变体。

这种模式抽象了创建具体对象的过程。考虑到在ECMAScript中无法创建类，用函数来封装以特定接口创建对象的细节，这个就被称工厂模式（Factory Pattern）

**原理：通过将对象的创建封装到一个方法中，可以无数次调用这个函数**

```javascript
function createPerson (name, age, gender, job) {
  var o = new Object();
  o.name = name;
  o.age = age;
  o.gender = gender;
  o.job = job;
  o.sayName = function () {
    console.log(this.name);
  };
  return o;
};
var person1 = createPerson('Br3ad', 18, 'male', 'Software Engineer');
var person2 = createPerson('Nicholas', 29, 'female', 'Doctor');
console.log(person1); // {name: "Br3ad", age: 18, gender: "male", job: "Software Engineer", sayName: ƒunction () {} }
console.log(person2); // {name: "Nicholas", age: 29, gender: "female", job: "Doctor", sayName: ƒunction () {} }
```

### 构造函数（Constructor）模式

> 关键字new后跟随一个函数调用，这里的函数称作构造函数（`Constructor`）

ECMAScript 中的构造函数可用来创建特定类型的对象，像`Object`和`Array`这样的原生构造函数，在运行时会自动出现在执行环境中，也可以创建自定义的构造函数，从而定义自定义对象类型的属性和方法

```javascript
function Person (name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function() {
    console.log(this.name);
  };
};
var person1 = new Person('Br3ad', 18, 'Software Enginner');
var person2 = new Person('Li', 29, 'Doctor');

person1.sayName(); // 'Br3ad'
person2.sayName(); // 'Li'
```

**对比工厂模式，可以发现以下区别：**

1、没有显示地创建对象
2、直接将属性和方法赋给了`this`对象；
3、没有`return`语句
4、创建对象时需要使用`new`关键字

*PS：按照惯例，构造函数始终都应该以一个大写字母开头，而非构造函数则应该以一个小写字母开头。（借鉴其他OO语言，为了区别其他ECMAScript中的其他函数）因为构造函数本身也是函数，只不过可以用来创建对象而已。*

要创建`Person`的新实例，必须使用`new`操作符。

**构造函数执行的几个步骤：**
(1)、创建一个新对象
(2)、将构造函数的作用域赋给新对象（因此`this`就指向了这个新对象）
(3)、执行构造函数中的代码（为这个新对象添加属性）
(4)、放回新对象

**构造函数和普通函数的区别？**

1、构造函数本身也是函数，只不过可以用来创建对象
2、调用方式不同，任何函数只要通过`new`操作符来调用，那它就可以作为构造函数（Constructor）；不通过`new`操作符来调用，那和普通函数没什么区别

通过构造函数创建的实例对象都有一个`constructor`（构造函数）属性，该属性指向实例对象的构造函数`Person`，请看下面的例子：

```javascript
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function () {
    console.log(this.name);
  }
}

var person1 = new Person('Br3ad', 29, 'Software Engineer');
var person2 = new Person('Chace', 18, 'Doctor');

// 构造函数创建的实例对象会有一个constructor属性，用与指向实例对象的构造函数Person
console.log(person1.constructor == Person); // true
console.log(person2.constructor == Person); // true
```

**将构造函数当函数来使用**
例子如下：

```javascript
// 当作构造函数使用
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
};
var person = new Person('Br3ad', 29, 'Software Engineer');
person.sayName(); // 'Br3ad'

// 当作普通函数来调用
Person('Chace', 18, 'Front-end Developer'); // 添加到window对象
window.sayName(); // 'Chace'

// 在另一个对象的作用域中调用
var o = new Object();
Person.call(o, 'imoldy', 20, 'Teacher');
o.sayName(); // 'imoldy'
```

**构造函数的问题**




### 原型模式

### Constructor（构造函数）+ 原型模式

### 动态原型模式

### 寄生构造函数模式

### 稳妥构造函数模式

### ES6中Class定义类

### ES5中提供[`Object.create()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)方法创建

> [MDN-Object.create()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)方法创建一个新对象，使用现有的对象来提供新创建的对象的`__proto__`

```javascript
const person = {
  isHuman: false,
  sayHi: function () {
    console.log(`my name is ${this.name}. Am I human ? ${this.isHum}`)
  }
}
const me = Object.create(person);

me.name = 'Chace Xie';
me.isHuman = true; // inherited properties can be overwritten
me.sayHi(); // my name is Chace Xie. Am I human ? true
```

## 参考链接

> [JS创建对象](https://blog.csdn.net/Luck_ZZ/article/details/102984112)
> [JavaScript中创建对象的几种方式](https://juejin.im/post/5cb34b456fb9a0688a680676)
> [js 创建对象的几种方式](https://segmentfault.com/a/1190000013003584)
