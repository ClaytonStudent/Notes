# JAVAScript

## 简介

Node.js 是JS运行环境

## 基础知识

- 我们可以使用一个 `<script>` 标签将 JavaScript 代码添加到页面中。
- `type` 和 `language` 特性（attribute）不是必需的。
- 外部的脚本可以通过 `<script src="path/to/script.js"></script>` 的方式插入。

## 代码结构

大部分时候可以省略分号，但是最好不要省略分号

现代模式 '`us strict`', **确保 “use strict” 出现在最顶部**

创建变量 `let` 旧版用 `var`

常量 `const` 需要大写硬编码

JS 是动态类型(dynamically typed) 不会限制为某一数据类型

JS 八种基本数据类型

1. number 整数和浮点数，范围 -2^53 --- 2^53 
2. bigInt 代表任意长度的整数
3. string 单双引号无区别，反引号是功能扩展。${变量名}
4. boolean: true, false
5. null 用于未知值
6. undefined 用于未定义值
7. symbol 用于唯一的标识符
8. object 复杂数据类型

我们可以通过 `typeof` 运算符查看存储在变量中的数据类型。

类型转换： 

String() 

Number() undefined--NaN, null --- 0,  

Boolean() 显示为0的都为false， 其他为true

+如果任一运算元是字符串，那么其它运算元也将被转化为字符串。

+运用于非数字，与Number()效果相同，转化为数字

++前置返回新值，后置返回旧值

== 区分不出 0 false 和空字符，需要用严格相等运算符===

aler 会弹窗，显示信息

prompt会问题，输入文本，确定

confirm 会问题，点击选择，确定

`break <labelName>` 语句跳出循环至标签处

函数

- 作为参数传递给函数的值，会被复制到函数的局部变量。
- 函数可以访问外部变量。但它只能从内到外起作用。函数外部的代码看不到函数内的局部变量。
- 函数可以返回值。如果没有返回值，则其返回的结果是 `undefined`。

函数声明 vs 函数表达式

- 如果函数在主代码流中被声明为单独的语句，则称为“函数声明”。**在函数声明被定义之前，它就可以被调用。**
- 如果该函数是作为表达式的一部分创建的，则称其“函数表达式”。**函数表达式是在代码执行到达时被创建，并且仅从那一刻起可用。**

箭头函数

```javascript
let func = (arg1, arg2, ...argN) => expression
// expression 是return
// let sum = (a, b) => a + b;
```

## 对象

```javascript
let user = new Object(); // “构造函数” 的语法
let user = {};  // “字面量” 的语法
```

添加直接赋值，删除用`delete`,最后一个属性应以逗号结尾

属性名（key）必须是字符串或 Symbol

遍历 for key in object 特殊顺序：整数属性会被进行排序，其他属性则按照创建的顺序显示。

**变量存储的不是对象本身，而是“内存中的地址”，换句话说就是对象的“引用”。**

**当对象被复制的时候 — 引用被复制了一份, 对象并没有被复制**

比较引用时，等号 `==` 和严格相等 `===` 没有差别

**两个对象只有在它们其实是一个对象时才会相等，两个独立的对象不相等，即便内容一样**

一个被 `const` 修饰的对象是 **可以** 被修改，`const`是修饰的是user本身存储的值，就是指向对象的引用，如果对象内容改变对这个没有影响

可以用`Object.assign`来复制对象，克隆出一份新的对象，合并多个对象到一个。对于更复杂的情况，用`lodash`里的函数`_.clondDeep(obj)`进行深拷贝

垃圾回收： reachability. 垃圾回收是自动完成的，回收不可达的对象

Symbol：唯一的，括号里面是描述，不会被自动转换为字符串(.toString())可以用来创建隐藏属性，加上[]，在 for in 循环中会被跳过，Object.keys(user)也会忽略，但是Object.assign会复制。

方法可以将对象引用为 `this`

构造函数在技术上是常规函数。不过有两个约定：

1. 它们的命名以大写字母开头。
2. 它们只能由 `"new"` 操作符来执行

通常构造器中没有return

## 数据类型

### 数据类型

“对象包装器”对于每种原始类型都是不同的，它们被称为 `String`、`Number`、`Boolean` 和 `Symbol`提供轻量级的临时对象。比如`str.toUpperCase()` 会创建一个轻量级的对象，调用方法然后销毁

特殊的原始类型 `null` 和 `undefined` 是例外。它们没有对应的“对象包装器”

**原始类型不是对象，不能存储额外的数据**

### 数字类型

默认的64位双精度浮点数

可以使用科学计数e

十六进制 0x  八进制0o  二进制 0b

`toString(base)` 返回在给定 `base` 进制数字系统中 `num` 的字符串表示形式。

```javascript
alert(num.toString(36)); // 一般的使用
alert( 123456..toString(36) ); // 直接在数字上使用，用两个点表示小数后面为空
```

舍入可以用 `Math.round`但是只有一位，多位使用 ：`+ num.toFixed(5)`，先返回string，再用加号转换成number

精度损失也可以用`toFixed()`来去掉不必要的小数部分

`isNaN(value)` 将其参数转换为数字，然后测试它是否为 `NaN`：

`isFinite(value)` 将其参数转换为数字，如果是常规数字，则返回 `true`，而不是 `NaN/Infinity/-Infinity`

有时候需要从字符串中“读取”数字，直到无法读取为止。如果发生 error，则返回收集到的数字。函数 `parseInt` 返回一个整数，而 `parseFloat` 返回一个浮点数。但必须以数字开头

**在处理小数时避免相等性检查，否则可能因为精度损失而不相等**

### 字符串

JavaScript 中的字符串使用的是 UTF-16 编码。

所有的特殊字符都以反斜杠字符 `\` 开始。它也被称为“转义字符”

`\´`插入引号，但是在双引号和反引号的string中不需要

查找子字符串，`str.indexOf(substr,pos)`

`str.includes(substr,pos)`类似的还有startsWith, endsWith

获取子字符串：`substring`、`substr` 和 `slice`。

`slice(start,end)`:返回字符串从 `start` 到（但不包括）`end` 的部分

`substring(start,end)`: slice几乎相同，允许start大于end

`substr(strat,length)`: 返回字符串从 `start` 开始的给定 `length` 的部分。

根据语言比较字符串时使用 `localeCompare`，否则将按字符代码进行比较。

`str.trim()` —— 删除字符串前后的空格 (“trims”)

`str.repeat(n)` —— 重复字符串 `n` 次