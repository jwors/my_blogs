### 数据类型

#### Javascript数据类型有哪些

1. number
2. string
3. null
4. bigint
5. symbol
6. object
7. boolean
8. undefined

#### 检测数据类型有哪些

1. typeof 只可以检测基本数据类型，无法检测引用数据类型
2. instanceOf 只可以检测引用数据类型，无法检测基本数据类型
3. constructor 不建议用来判断类型，因为数据类型的原型是可以被修改的
4. Object.prototype.toString.call() 万能的，用Object.toString而不用Array、function的，是因为它们原型的上toString都重写了

#### 判断数组的方式

> 3、4、5 本质都是判断原型链

1. Array.isArray([])
2. Object.prototype.tostring().call()
3. [] instanceof Array
4. [].__proto__ == Array.prototype
5. Array.prototype.isPrototypeOf([])

#### null 和 undefined 的区别

> undefined 是定义了没赋值，那么默认值就是undefined, null 则代表空对象，然后 **tyepeof判断下 null是对象，undefined不是js中的保留字，也就是可以定义一个名为undefined的变量或者常量名**

### typeof null 是什么

> 结果为 object,好像是因为js有一个类型标签的东西，然后object的类型标签和null的类型标签一样导致的

#### 其他值到字符串的转换规则？

* Null 和 Undefined 类型 ，null 转换为 "null"，undefined 转换为 "undefined"，
* Boolean 类型，true 转换为 "true"，false 转换为 "false"。
* Number 类型的值直接转换，不过那些极小和极大的数字会使用指数形式。
* Symbol 类型的值直接转换，但是只允许显式强制类型转换，使用隐式强制类型转换会产生错误。
* 对普通对象来说，除非自行定义 toString() 方法，否则会调用 toString()（Object.prototype.toString()）来返回内部属性 [[Class]] 的值，如"[object Object]"。如果对象有自己的 toString() 方法，字符串化时就会调用该方法并使用其返回值。

#### 其他值到布尔类型的值的转换规则
>
> 以下这些是假值： • undefined • null • false • +0、-0 和 NaN • "",假值的布尔强制类型转换结果为 false。从逻辑上说，假值列表以外的都应该是真值。

#### 箭头函数

* 相对于普通函数更加简洁
* 没有自己的__this__,只会继承在创建的时候上一层的this，之后就不会改变
* call()、bind()、apply()无法改变箭头函数的this
* 箭头函数不可以是当作构造函数

#### new 操作符实现原理

* 首先创造了一个空对象
* 设置原型，将对象的圆形设置为函数的prototype对象
* 让函数的 this 指向这个对象，执行这个构造函数
* 判断函数的返回值类型，如果是值类型，返回创建的对象。如果是引用类型，就返回这个引用类型的对象

``` javascript

function objectFactory(obj,...rest){
 // 基于obj的原型创建一个新的对象
 const newobj = Object.create(obj.prototype);
 const result = obj.apply(newobj,rest)

 return typeof result === 'object' ? result : newobj
}

const person1 = myNew(Person, 'Alice', 30);
```

## isNaN and Number.isNana of distinction

* If the argument(参数) passed to isNaN() is not a number, isNaN() returns true.
* If the argument is a number, isNaN() tries to convert it to a number first. If the conversion is successful and the resulting value is NaN, isNaN() returns true. If the conversion results in a valid number, isNaN() returns false.
* Number.isNaN： judge arg is NaN
