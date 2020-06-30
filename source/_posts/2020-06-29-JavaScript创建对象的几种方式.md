---
title: JavaScript创建对象的几种方式
date: 2020-06-29 23:09:22
tags:
- 前端
- 前端面试题
- JavaScript object
- javascript对象
- object
category:
- [前端]
- [JavaScript]
---

> 一般情况下，JS中创建对象的方式可以用构造函数`Object`或者对象字面量的方式，但需要创建几个具有相同属性或方法的对象时，就得写大量的冗余代码。故而出现了下述几种创建对象的方法。

## 使用对象字面量创建对象

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

## 通过`new`操作符创建对象

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

## Prototype（原型）模式

## 工厂模式

使用同一个接口创建很多对象，会产生大量的重复代码。为了解决这个问题，开始使用工厂模式的一种变体。

原理：通过将对象的创建封装到一个方法中，可以无数次调用这个函数 
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

## Constructor（构造函数）模式




## Constructor（构造函数）+ Prototype（原型）模式

## 动态原型模式

## 寄生构造函数模式

## 稳妥构造函数模式

## ES6中Class定义类

## ES5中提供[`Object.create()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)方法创建

## 参考链接

> [JS创建对象](https://blog.csdn.net/Luck_ZZ/article/details/102984112)
> [JavaScript中创建对象的几种方式](https://juejin.im/post/5cb34b456fb9a0688a680676)
> [js 创建对象的几种方式](https://segmentfault.com/a/1190000013003584)
> [阮一峰-JavaScript封装](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html)
> [MDN-Object-create](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
