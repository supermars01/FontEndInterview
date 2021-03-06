# JavaScript面试准备

## 1. 简介

### Web发展史（了解）

英语+互联网+金融（政治是目的，金融是手段）金融就是加杠杆，金融最厉害的玩法是最低成本，末端是期货、股票。最低成本为王。股票的震源来自外汇，高明玩法是国债。金融是实现暴富的手段，技术是生存的根本。

### 浏览器的组成

- `Shell`部分
- 内核部分
  - 渲染引擎（语法规则和渲染）
  - `js`引擎
  - 其他模块

主流浏览器

| 主流浏览器 | 内核             |
| ---------- | ---------------- |
| IE         | `trident`        |
| Chrome     | `webkit`/`blink` |
| firefox    | `Gecko`          |
| Opera      | `presto`         |
| Safari     | `webkit`         |

### JavaScript	轻量级弱类型脚本语言

- 脚本语言（解释性语言）： 不能自己独立运行，需要依赖别的语言
- 单线程
  - 执行队列：轮转时间片

`js` 依赖的是`html`

- `html` 超文本标记语言（基础语言）

- `css` 层叠样式表（不是语言）

- `js` 脚本语言

`js` 是在做什么

- 通过我们的语法，来控制页面上标签（DOM）出现一些变化
- 通过我们的语法，来控制浏览器发生一些变化

`js` 的三大核心

- `ECMAScript`（表示我们的语法）
- `DOM`
  - 拥有一套成熟的`API`，用来操作页面中的标签
- `BOM`
  - 拥有一套成熟的`API`，用来操作浏览器的

JavaScript如何引用

```html
<body>
    <script>
    	// 第一种引入方法 内部嵌入
	</script>
    
    <!-- 第二种引入方式 引入外部文件 -->
    <script src="./index"></script>
</body>
```



## 2.基本语法

语句后面要用分号结束

`js`语法错误会引发后续代码终止，但不会影响其他`js`代码块

### 1. 变量

- 形式
- 规则
- 规范

1. 形式

```javascript
var n1 = 100;
// var 声明一个变量的关键词
// n1 变量的名称
// = 赋值运算（把右边的值赋值给左边的变量名）
```

2. 规则：

- 一个变量名，只能由**数字、下划线、美元符号（$）**组成
- 不能以数字开头
- 严格区分大小写，每一个字母都区分大小写
- 不能使用 关键字 和 保留字
- 不能有空格

3. 规范：

- 变量名尽量有意义（语义化）
- 驼峰命名法
- 不要使用中文或拼音

内存

- 栈内存 `stack`
- 堆内存 `heap`

### 2. 数据类型

- 基本数据类型
- 引用数据类型
- 判断数据类型
- 数据类型转换

1. 基本数据类型
   - 数值 `Number`
     - `NaN`
   - 字符串`String`
   - 布尔值 `Boolean`
   - 空对象指针 `Null`
   - 未定义数据类型 `undefined`

2. 引用数据类型

   - 数组`[]`

     - 类数组

       1. 可以利用属性名模拟数组的特性
       2. 可以动态的增加`length`属性
       3. 如果强行让类数组调用`push`方法，则会根据`length`属性值的位置进行属性的扩充

       属性要为索引（数字）属性，必须要有`length`属性，最好加上`push`

       ```javascript
       var obj = {
           "2": "a",
           "3": "b",
           "length": 2,
           "push": Array.prototype.push
       }
       obj.push('c')
       obj.push('d')
       
       console.log(obj)
       // { '2': 'c', '3': 'd', length: 4, push: [Function: push] }
       ```

   - 对象 `{}`

   - 函数 `Function`

   - ...

3. 判断数据类型

   - `typeof` 关键字进行判断

     ```javascript
     // typeof 待检测的变量
     // typeof(待检测的变量)
     typeof {}	// "object"
     typeof []	// "object"
     typeof null	// "object"
     ```

     `typeof` 能返回的数据类型有（6种）：number string boolean object undefined function

     `typeof` 关键字的返回值是待检测变量的数据类型，且该条返回值的数据类型是 字符串String

   - `isNaN`

     检测数据是不是一个非有效数字

     1. 先进行隐式调用 `Number()`
     2. 执行`isNaN()`

     ```javascript
     isNaN("abc")	// true
     isNaN(null)		// false
     isNaN(undefined)	// true
     ```

   - `instanceof`

     根据原型链向上查找，如果能找到返回`true`，否则返回`false`

     ```javascript
     // A instanceof B
     // A对象 是不是 B构造函数构造出来的
     // 看A对象的原型链上 有没有 B的原型
     ```

   - `Object.prototype.toString.call()`

     ```javascript
     console.log(Object.prototype.toString.call([]))		// [object Array]
     console.log(Object.prototype.toString.call(123))	// [object Number]
     console.log(Object.prototype.toString.call({}))		// [object Object]
     ```

   - 自己封装的类型判断方法`myType`

     ```javascript
     function myType(target){
         var template = {
             "[object Array]": "array",
             "[object Object]": "object",
             "[object Number]": "number-object",
             "[object String]": "string-object",
             "[object Boolean]": "boolean-object"
         }
         
         if(target === null){
             return "null"
         }else if(typeof(target) == "object"){
             var str = Object.prototype.toString.call(target)
             return template[str]
         }else{
             return typeof(target)
         }
     }
     ```

4. 数据类型转换

   转换成数字类型

   - `Number（要转换的内容）`只认完整的数据，可进行数据类型转换，但不认'100a'这样的数据

     ==把这个数据当做一个整体来看==

     尽可能地转换成数字

     转换成功，返回一个数值；不成功，返回`NaN`

     ```javascript
     Number(false)	// 0
     Number(undefined)	// NaN
     Number("a")	// NaN
     Number("123")	// 123
     Number("-123")	// -123
     Number("-123abc")	// NaN
     ```

   - `parseInt（要转换的内容）`只识整数，不认数据类型转换

     ==把这个数据当做一个文本来看，从左到右一位一位的看==

     只认识数，不认识true、false、null、undefined

     如果第一个位置就不能转换，那么直接返回NaN

     不认识小数点，只能解析整数

     ```javascript
     parseInt(true)	// NaN
     parseInt(false)	// NaN
     parseInt(null)	// NaN
     parseInt(undefined)	// NaN
     ```

   - `parseFloat（要转换的内容）`

     ==把这个数据当做一个文本来看，从左到右一位一位的看==

   - 进行一个非 + 运算

   转换成字符串类型

   - `String()`

   - 数据`.toString()`

     `undefined` 和 `null` 不能用`.toString()`

   - `+`运算

     只要+有一边的数据是字符串类型，就会进行字符串拼接

     只有+两边都是数字或者布尔的时候，才会进行数学运算

   转换成布尔类型

   - `Boolean()`

     在`js`中只有以下五种数据能转换成false，其余都是true

     `0`，`''`，`NaN`，`undefined`，`null` 这五个是false

   隐式数据类型转换

   - `isNaN()`

   - ++、 --、 +、 - （一元正负）

     ```javascript
     var a = 1;
     +a;
     -a;
     ```

   - +

   - -、*、/、%

   - &&、||

   - <、>、<=、>=

   - == 、!=

   ```javascript
   null == 0;	// false
   undefined == null;	// true
   undefined == 0;	// false
   ```


### 3. 运算符

```javascript
// == 相等 与 ===全等 的区别
```

```javascript
// 前置++ 先运算后赋值
// ++后置 先赋值后运算
var a = 10;
var b = ++a - 1 + a++;
console.log(b)

// result =>
// 21
```

```javascript
// && 和 || 优先级：先执行 && 后执行 ||
```

```javascript
// 三元运算符 ()?():()
```

```javascript
// + 数学运算/字符串拼接
// - * / %
```



### 4. 条件分支&循环结构

```javascript
if(){}else{}
while(){}
switch(n){
    case 1:
        console.log(1);
        break;
    default:
        console.log('default')
}
for(var i = 0; i < 10; i++)
```

```javascript
// continue
// 在循环中使用的时候，当执行到continue时，会结束本次循环，进入到下一次循环中

// break
// 在循环中使用时，当执行到break的时候，会终止循环
```

### 5. 函数

#### 声明

函数声明（声明式函数）

函数表达式（命名式）

#### 形参、实参

函数的参数和`arguments`存在映射机制

```javascript
function test(a, b){
  a = 3;
  console.log(arguments[0])
}
test(1, 2)	// 3
```

但是这种映射机制是在函数运行的一瞬间建立

```javascript
function test(a, b){
  b = 4;
  console.log(arguments[1])
}
test(1)	// undefined
```



#### 预编译（预解释）

##### 四部曲

1. 创建`AO`对象
2. 找形参和变量声明，将变量和形参名作为`AO`属性名，值为`undefined`
3. 将实参值和形参统一
4. 在函数体里面找函数声明，值赋予函数体

- 就是在代码执行之前，对代码进行通读，把一些东西提前解析出来

解析（一共解析两点）：

- 声明式函数 `function fn() {}`：声明一个变量，并将函数地址赋值给这个变量
- var 声明：只声明一个变量，并不赋值

问题：如果声明一个变量和函数，变量名和函数名一样会怎么样？

```javascript
console.log(fn)
fn()
var fn = 100;
function fn(){
    console.log('hello world')
}
fn()

// result => hello world
// throw an error!!!
```

预解析后，在声明变量前，还能使用函数名来执行函数；

在声明变量后，就不能执行函数了

#### 作用域

- 运行期上下文： 当函数执行时，会创建一个称为==执行期上下文==的内部环境。一个执行期上下文定义了一个函数执行时的环境，函数每次执行时对应的执行上下文都是独一无二的，所以多次调用一个函数会导致创建多个执行上下文，当函数执行完毕，它所产生的执行上下文被销毁
- 查找变量：从作用域链的顶端依次向下查找

### 6. 编程形式

- 面向过程
- 面向对象

### 7. 原型

#### 定义

​	原型是function对象的一个属性，它定义了构造函数制造出的对象的公共祖先。通过该构造函数产生的对象，可以继承该原型的属性和方法。原型也是对象。

利用原型的特点和概念，可以提取共有属性。

```javascript
function Car(){}
Car.prototype = {
    lang: 4900,
    height: 5200
}
Car.prototype.name = "BMW"
var car = new Car();

console.log(car.name)	// "BMW"
console.log(car.lang)	// 4900
console.log(car.height)	// 5200
```

`prototype.key = value` 和 `prototype = {}` 的区别

```javascript
Person.prototype.name = "sunny";
function Person(){};
var person = new Person();
Person.prototype = {
    name: 'cherry'
}

console.log(person.name)	// "sunny"
```

```javascript
Person.prototype.name = "sunny";
function Person(){};
var person = new Person();
Person.prototype.name = "cherry";

console.log(person.name)	// "cherry"
```

```javascript
Person.prototype.name = "sunny";
function Person(){};

Person.prototype = {
    name: 'cherry'
}
var person = new Person();

console.log(person.name)	// "sunny"
```



对象如何查看原型 --> 隐式属性`__proto__`

```javascript
// 对象的__proto__属性指向该对象的原型
// car.__proto__ => Car.prototype
```



对象如何查看对象的构造函数 -->  `constructor`

#### 原型链

如何构成原型链

原型链上属性的增删改查

```javascript
// 如果原型上的某个属性是引用值，那么子代可以通过这样的方式修改父代的属性
function Father(){
    this.fortune = {
        card1: "visa"
    }
}

var father = new Father();
function Son(){

}
Son.prototype = father;
var son = new Son()
son.fortune.card2 = 'master'

console.log(father.fortune.card2)	// "master"
```



绝大多数对象的最终都会继承自`Object.prototype`

```javascript
Object.create(null)

// [Object: null prototype] {}
```



`Object.create（原型）`

```javascript
var obj = {name: 'mlq', age: 18}
var obj1 = Object.create(obj)	// 指定一个原型，只能放对象（引用类型数据），null或undefined类型

console.log(obj1.__proto__)	// {name: 'mlq", age 18}
```



#### `call()` 和 `apply()`

`call()`的应用

```javascript
function Person(name, age){
    this.name = name;
    this.age = age;
}
function Student(name, age, tel){
    Person.call(this, name, age)
    this.tel = tel
}

var student = new Student("mlq", 18, 5522)

console.log(student)	// Student { name: 'mlq', age: 18, tel: 5522 }
```

`call()`和 `apply()`都是改变`this`指向的，区别是传入参数不同

`call()`需要把实参按照形参的个数传进去

`apply()`需要传一个`arguments`



#### this

1. 函数预编译过程	`this` --> `window`
2. 全局作用域里		`this` --> `window`
3. `call()` 和 `apply()` 可以改变函数运行时 `this` 指向
4. `obj.func()`；`func()`里面的`this`指向`obj`



#### 继承

1. 传统形式-->原型链

   过多的继承了没用的属性

2. 借用构造函数

   不能继承借用构造函数的原型

   每次构造函数都要多走一个函数

3. 共享原型

   不能随便改动自己的原型

4. 圣杯模式

   ```javascript
   function Father(){}
   function Son(){}
   function inherit(Target, Origin){
       function F(){}
       F.prototype = Origin.prototype;
       Target.prototype = new F();
   }
   inherit(Son, Father)
   Father.prototype.name = "mlq"
   var son = new Son()
   console.log(son.name)
   
   // Yahoo实现
   var inherit = (function () {
       var F = function(){}
       return function(Target, Origin){
           F.prototype = Origin.prototype;
           Target.prototype = new F();
           Target.prototype.constructor = Target;
           Target.prototype.uper = Origin.prototype;	// uper => super
       }
   }())
   ```

5. 继承公有属性

   ```javascript
   // 1) Object.setPrototypeOf(Child.prototype, Parent.prototype)
   // Child.prototype.__proto__ = Parent.prototype
   // 2) Child.prototype = Object.create(Parent.prototype)
   ```

6. 继承私有属性

   ```javascript
   // Parent.call(this)
   class Child extends Parent{
       constructor(){
           super()	// Parent.call(this)
       }
   }
   ```




#### new关键字

```javascript
function test(c){
    // var this = Object.create(test.prototype)
    var a = 123;
    function b(){}
}
new test();

test(1)	// AO {
//			arguments: [1],
//			this: window,
//			c: 1,
//			a: undefined,
//			b: function(){}
//		}
```



### 闭包

#### 作用

- 实现公有变量
  - 函数累加器
- 可以做缓存 （存储结构）
- 可以实现封装，属性私有化
- 模块化开发，防止污染全局变量



#### 高级单例模式

```javascript
var nameSpace = (function () {
    var n = 12;
    function fn(){
        // ...
    }
    return {
        fn: fn
    }
})()
```

