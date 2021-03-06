---
title: js函数的定义与调用
date: 2020-03-12 20:37:12
tags: [javascript,前端]
categories: [javascript]
---
<img src="http://lishengyu.xyz/pubgm/IMG_5446.JPG" >

### 1.定义函数
在JavaScript中，定义函数的方式如下：
```javascript
function abs(x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
```
上述`abs()`函数的定义如下：

- `function`指出这是一个函数定义；
- `abs`是函数的名称；
- `(x)`括号内列出函数的参数，多个参数以,分隔；
- `{ ... }`之间的代码是函数体，可以包含若干语句，甚至可以没有任何语句。

注意，函数体内部的语句在执行时，一旦执行到`return`时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。

如果没有`return`语句，函数执行完毕后也会返回结果，只是结果为`undefined`。

由于JavaScript的函数也是一个对象，上述定义的abs()函数实际上是一个函数对象，而函数名abs可以视为指向该函数的变量。

因此，第二种定义函数的方式如下：
```javascript
var abs = function (x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
};
```
在这种方式下，`function (x) { ... }`是一个**匿名函数**，它没有函数名。但是，这个匿名函数赋值给了变量abs，所以，通过变量abs就可以调用该函数。

上述两种定义完全等价，**注意第二种方式按照完整语法需要在函数体末尾加一个;表示赋值语句结束**。

### 2.调用函数

调用函数时，按顺序传入参数即可：
```javascript
abs(10); // 返回10
abs(-9); // 返回9
```
由于JavaScript允许传入任意个参数而不影响调用，因此**传入的参数比定义的参数多也没有问题，虽然函数内部并不需要这些参数**：

```javascript
abs(10, 'blablabla'); // 返回10
abs(-9, 'haha', 'hehe', null); // 返回9
```
传入的参数比定义的少也没有问题：
```javascript
abs(); // 返回NaN
```
此时`abs(x)`函数的参数x将收到`undefined`，计算结果为`NaN`。

要避免收到`undefined`，可以对参数进行检查：
```javascript
function abs(x) {
    if (typeof x !== 'number') {
        throw 'Not a number';
    }
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
}
```
#### arguments

JavaScript还有一个关键字`arguments`，它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。`arguments`类似Array但它不是一个Array。利用`arguments`，你可以获得调用者传入的所有参数。也就是说，即使函数不定义任何参数，还是可以拿到参数的值：
```javascript
function abs() {
    if (arguments.length === 0) {
        return 0;
    }
    var x = arguments[0];
    return x >= 0 ? x : -x;
}

abs(); // 0
abs(10); // 10
abs(-9); // 9
```
实际上`arguments`最常用于判断传入参数的个数。你可能会看到这样的写法：
```javascript
// foo(a[, b], c)
// 接收2~3个参数，b是可选参数，如果只传2个参数，b默认为null：
function foo(a, b, c) {
    if (arguments.length === 2) {
        // 实际拿到的参数是a和b，c为undefined
        c = b; // 把b赋给c
        b = null; // b变为默认值
    }
    // ...
}
```
要把中间的参数b变为“可选”参数，就只能通过`arguments`判断，然后重新调整参数并赋值。

#### rest参数

由于JavaScript函数允许接收任意个参数，于是我们就不得不用`arguments`来获取所有参数：
```javascript
function foo(a, b) {
    var i, rest = [];
    if (arguments.length > 2) {
        for (i = 2; i<arguments.length; i++) {
            rest.push(arguments[i]);
        }
    }
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}
```
为了获取除了已定义参数a、b之外的参数，我们不得不用`arguments`，并且循环要从索引2开始以便排除前两个参数，这种写法很别扭，只是为了获得额外的`rest`参数，有没有更好的方法？

ES6标准引入了`rest`参数，上面的函数可以改写为：

```javascript
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
`rest`参数只能写在最后，前面用...标识，从运行结果可知，传入的参数先绑定a、b，多余的参数以数组形式交给变量`rest`，所以，不再需要`arguments`我们就获取了全部参数。

如果传入的参数连正常定义的参数都没填满，也不要紧，`rest`参数会接收一个空数组（注意不是`undefined`）。

### return
JavaScript引擎有一个在行末自动添加分号的机制，这可能让你栽到return语句的一个大坑：
```javascript
function foo() {
    return { name: 'foo' };
}

foo(); // { name: 'foo' }
```

如果把return语句拆成两行：
```javascript
function foo() {
    return
        { name: 'foo' };
}

foo(); // undefined
```
要小心了，由于JavaScript引擎在行末自动添加分号的机制，上面的代码实际上变成了：
```javascript
function foo() {
    return; // 自动添加了分号，相当于return undefined;
        { name: 'foo' }; // 这行语句已经没法执行到了
}
```
所以正确的多行写法是：
```javascript
function foo() {
    return { // 这里不会自动加分号，因为{表示语句尚未结束
        name: 'foo'
    };
}
```
