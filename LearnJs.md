# JavaScript：从入门到有所了解

## 数据类型

- Number

  Js不区分整数和浮点数，统一用Number表示

  ```javascript
  123; // 整数123
  0.456; // 浮点数0.456
  1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
  -99; // 负数
  NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
  Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为              Infinity
  ```

- String

  字符串是以单引号'或双引号"括起来的任意文本，比如`'abc'`，`"xyz"`等等。请注意，`''`或`""`本身只是一种表示方式，不是字符串的一部分，因此，字符串`'abc'`只有`a`，`b`，`c`这3个字符。

- Boolean

  逻辑与，或，非分别为`&&`，`||`，`!`。

  JavaScript把`null`、`undefined`、`0`、`NaN`和空字符串`''`视为`false`，其他值一概视为`true`。

- 比较运算符

  JavaScript允许对任意数据类型做比较：

  ```javascript
  2 > 5; // false
  5 >= 2; // true
  7 == 7; // true
  false == 0; // true
  false === 0; // false
  ```

  相等运算符`==`。JavaScript在设计时，有两种比较运算符：

  第一种是`==`比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；

  第二种是`===`比较，它不会自动转换数据类型，如果数据类型不一致，返回`false`，如果一致，再比较。

  由于JavaScript这个设计缺陷，不要使用`==`比较，始终坚持使用`===`比较。

  另一个例外是`NaN`这个特殊的Number与所有其他值都不相等，包括它自己：

  ```javascript
  NaN === NaN; // false
  ```

  唯一能判断`NaN`的方法是通过`isNaN()`函数：

  ```javascript
  isNaN(NaN); // true
  ```

  最后要注意浮点数的相等比较：

  ```javascript
  1 / 3 === (1 - 2 / 3); // false
  ```

  这不是JavaScript的设计缺陷。浮点数在运算过程中会产生误差，因为计算机无法精确表示无限循环小数。要比较两个浮点数是否相等，只能计算它们之差的绝对值，看是否小于某个阈值：

  ```javascript
  Math.abs(1 / 3 - (1 - 2 / 3)) < 0.0000001; // true
  ```

- NULL 和undefined

  `null`表示空值，类似于java里的`null`，`undefined`表示 ‘未定义’，通常情况下用`null`，在判断函数参数是否传递时用`undefined`

- 数组

  数组是一组按顺序排列的集合，集合的每个值称为元素。JavaScript的数组可以包括任意数据类型。例如：

  ```javascript
  [1, 2, 3.14, 'Hello', null, true];
  ```

  上述数组包含6个元素。数组用`[]`表示，元素之间用`,`分隔。

  另一种创建数组的方法是通过`Array()`函数实现：

  ```javascript
  new Array(1, 2, 3); // 创建了数组[1, 2, 3]	
  ```

  然而，出于代码的可读性考虑，强烈建议直接使用`[]`。

  数组的元素可以通过索引来访问。请注意，索引的起始值为`0`：

  ```javascript
  var arr = [1, 2, 3.14, 'Hello', null, true];
  arr[0]; // 返回索引为0的元素，即1
  arr[5]; // 返回索引为5的元素，即true
  arr[6]; // 索引超出了范围，返回undefined
  ```

- Object

  JavaScript的对象是一组由键-值组成的无序集合，例如：

  ```javascript
  var person = {
      name: 'Bob',
      age: 20,
      tags: ['js', 'web', 'mobile'],
      city: 'Beijing',
      hasCar: true,
      zipcode: null
  };
  ```

  JavaScript对象的键都是字符串类型，值可以是任意数据类型。上述`person`对象一共定义了6个键值对，其中每个键又称为对象的属性，例如，`person`的`name`属性为`'Bob'`，`zipcode`属性为`null`。

  要获取一个对象的属性，我们用`对象变量.属性名`的方式：

  ```javascript
  person.name; // 'Bob'
  person.zipcode; // null
  ```

## 变量

使用`var`来声明一个局部变量，如果一个变量没有通过`var`申明就被使用，那么该变量就自动被申明为全局变量。

> strict模式：不使用`var`来声明变量有时会导致变量作用域的问题，因此推出strict模式。在strict模式下运行的JavaScript代码，强制通过`var`申明变量，未使用`var`申明变量就使用的，将导致运行错误。
>
> 启用strict模式的方法是在JavaScript代码的第一行写上：
>
> ```javascript
> 'use strict';
> ```

## 字符串

字符串可以用单引号`''`和双引号`""`表示，并可在字符串中使用转义字符`\`，ASCII字符可以以`\x##`形式的十六进制表示，例如：

```javascript
'\x41'; // 完全等同于 'A'
```

还可以用`\u####`表示一个Unicode字符：

```javascript
'\u4e2d\u6587'; // 完全等同于 '中文'
```

由于多行字符串用`\n`写起来比较费事，所以最新的ES6标准新增了一种多行字符串的表示方法，用反引号` `` `表示：

```javascript
`这是一个
多行
字符串`;
```

- 模板字符串

  要把多个字符串连接起来，可以用`+`号连接：

  ```javascript
  var name = '小明';
  var age = 20;
  var message = '你好, ' + name + ', 你今年' + age + '岁了!';
  alert(message);
  ```

  如果有很多变量需要连接，用`+`号就比较麻烦。ES6新增了一种模板字符串，表示方法和上面的多行字符串一样，但是它会自动替换字符串中的变量：

  ```javascript
  var name = '小明';
  var age = 20;
  var message = `你好, ${name}, 你今年${age}岁了!`;
  alert(message);
  ```

- 字符串的操作

  1. 获取字符串长度

     ```js
     var s = 'Hello, world!';
     s.length; // 13
     ```

  2. 获取某个位置的字符

     要获取字符串某个指定位置的字符，使用类似Array的下标操作，索引号从0开始：

     ```javascript
     var s = 'Hello, world!';
     
     s[0]; // 'H'
     s[6]; // ' '
     s[7]; // 'w'
     s[12]; // '!'
     s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined
     ```

  3. 常用的方法

     ```javascript
     s.toUpperCase(); //把一个字符串全部变为大写
     s.toLowerCase(); //把一个字符串全部变为小写
     s.indexOf(str); //搜索指定字符串出现的位置
     s.substring(index1,index2);  //返回指定索引区间的子串
     ```

## 数组

> JavaScript的`Array`可以包含任意数据类型，并通过索引来访问每个元素。

### Array的属性

要取得`Array`的长度，直接访问`length`属性：

```javascript
var arr = [1, 2, 3.14, 'Hello', null, true];
arr.length; // 6
```

直接给`Array`的`length`赋一个新的值会导致`Array`大小的变化：

```javascript
var arr = [1, 2, 3];
arr.length; // 3
arr.length = 6;
arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
arr.length = 2;
arr; // arr变为[1, 2]
```

### Array的方法

---

#### indexOf

可以通过`indexOf()`来搜索一个指定的元素的位置：

```javascript
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(10); // 元素10的索引为0
arr.indexOf(20); // 元素20的索引为1
arr.indexOf(30); // 元素30没有找到，返回-1
arr.indexOf('30'); // 元素'30'的索引为2
```

#### slice

截取`Array`的部分元素，然后返回一个新的`Array`：

```javascript
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
```

注意`slice()`的起止参数包括开始索引，不包括结束索引。

如果不给`slice()`传递任何参数，它就会从头到尾截取所有元素。利用这一点，可以复制一个`Array`：

```javascript
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```

#### pop和push

`push()`向`Array`的末尾添加若干元素，`pop()`则把`Array`的最后一个元素删除掉：

```javascript
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```

#### unshift和shift

如果要往`Array`的头部添加若干元素，使用`unshift()`方法，`shift()`方法则把`Array`的第一个元素删掉：

```js
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
```

#### sort

`sort()`可以对当前`Array`进行排序，它会直接修改当前`Array`的元素位置，直接调用时，按照默认顺序排序：

```js
var arr = ['B', 'C', 'A'];
arr.sort();
arr; // ['A', 'B', 'C']
```

#### reverse

`reverse()`把整个`Array`的元素给反转：

```js
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
```

#### splice

`splice()`方法是修改`Array`的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素。splice的基本语法为

```js
arr.splice(<开始索引>,<要删除的元素个数>,<添加元素1>,<添加元素2>, ...<添加元素n>)
```

例：

```js
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```

#### concat

`concat()`方法把当前的`Array`和另一个`Array`连接起来，并返回一个新的`Array`：

```js
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']
```

*请注意*，`concat()`方法并没有修改当前`Array`，而是返回了一个新的`Array`。

实际上，`concat()`方法可以接收任意个元素和`Array`，并且自动把`Array`拆开，然后全部添加到新的`Array`里：

```js
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```

#### join

`join()`方法是一个非常实用的方法，它把当前`Array`的每个元素都用指定的字符串连接起来，然后返回连接后的字符串：

```js
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-');  // 'A-B-C-1-2-3'
```

如果`Array`的元素不是字符串，将自动转换为字符串后再连接。

## 对象

JavaScript的对象是一种无序的集合数据类型，它由若干键值对组成。例：

```js
var object = {prop1:value1,prop2:value2, ...};
```

要访问对象的属性，需要用`.`，如`object.prop1`。如果属性名不是标准的标识符，则需要用双引号括起来

```js
var object = {prop1:value1,"prop2":value2, ...};
```

要访问此类属性，需要用`object["prop2"]`。当访问不存在的属性时返回`undefined`。Js是动态语言，可以自由的增加或删除属性。

```js
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
```

如果我们要检测`xiaoming`是否拥有某一属性，可以用`in`操作符：

```js
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};
'name' in xiaoming; // true
'grade' in xiaoming; // false
```

但是`in`，不能判断属性是否是继承的，要判断一个属性是否是`xiaoming`自身拥有的，而不是继承得到的，可以用`hasOwnProperty()`方法：

```js
var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```

## Map和Set

### Map

`Map`是一组键值对的结构，具有极快的查找速度。

举个例子，假设要根据同学的名字查找对应的成绩，如果用`Array`实现，需要两个`Array`：

```js
var names = ['Michael', 'Bob', 'Tracy'];
var scores = [95, 75, 85];	
```

给定一个名字，要查找对应的成绩，就先要在names中找到对应的位置，再从scores取出对应的成绩，Array越长，耗时越长。

如果用Map实现，只需要一个“名字”-“成绩”的对照表，直接根据名字查找成绩，无论这个表有多大，查找速度都不会变慢。用JavaScript写一个Map如下：

```js
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael'); // 95
```

初始化`Map`需要一个二维数组，或者直接初始化一个空`Map`。`Map`具有以下方法：

```js
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
```

由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉：

```js
var m = new Map();
m.set('Adam', 67);
m.set('Adam', 88);
m.get('Adam'); // 88
```

### Set

`Set`和`Map`类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在`Set`中，没有重复的key。

要创建一个`Set`，需要提供一个`Array`作为输入，或者直接创建一个空`Set`：

```js
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
```

重复元素在`Set`中自动被过滤：

```js
var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}
```

注意数字`3`和字符串`'3'`是不同的元素。

通过`add(key)`方法可以添加元素到`Set`中，可以重复添加，但不会有效果：

```js
s.add(4);
s; // Set {1, 2, 3, 4}
s.add(4);
s; // 仍然是 Set {1, 2, 3, 4}
```

通过`delete(key)`方法可以删除元素：

```js
var s = new Set([1, 2, 3]);
s; // Set {1, 2, 3}
s.delete(3);
s; // Set {1, 2}
```

## 函数

在JavaScript中，定义函数的方式如下：

```js
function abs(x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
```

如果没有`return`语句，函数执行完毕后也会返回结果，只是结果为`undefined`。

### arguments

关键字`arguments`只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。`arguments`类似`Array`但它不是一个`Array`。可以像使用array一样使用argument来访问传入的所有参数，包括没有定义形参的函数。

```js
function abs() {
    if (arguments.length === 0) {
        return 0;
    }
    var x = arguments[0];
    return x >= 0 ? x : -x;
}
```

### rest参数

rest参数定义在其他形参之后，在前面用`...`，标识，可以用于表示数量不确定的所有形参

```js
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

foo(1);
// 结果:
// a = 1
// b = undefined
// Array []
```

如果传入的参数连正常定义的参数都没填满，rest参数会接收一个空数组（注意不是`undefined`）。