## Generator 函数

Generator 函数有两个特征。1. function 和函数名之间有一个`*`号。2. 函数体内部使用 yield 表达式，定义不同的内部状态，表达函数暂停执行。

执行 Generator 函数会返回一个遍历器对象。这个遍历器函数可以使用 next 方法遍历 Generator 函数内部的每一个状态。比如：
```
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```
Generator 函数的调用方法与普通函数相同，不同的是调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个指向内部状态的指针对象，就是遍历器对象。接着调用遍历器对象的 next 方法，使指针移向下一个状态，即 下一个 yield 表达式。

## yield 表达式

yield 表达式表示暂停，调用 next 方法将内部指针移到该语句的时候才会执行，返回一个对象，它的 value 属性就是当前 yield 表达式的值，done属性的值是一个布尔值，如果是false，表示遍历还没有结束。

遍历器对象的 next 方法执行逻辑如下：

1.遇到yield表达式，暂停执行后面的操作，将 yield 后面的值当成表达式的值返回。

2.次调用 next 方法时，再继续往下执行，直到执行到下一个 yield 表达式。

3.如果没有再遇到新的 yield 表达式，就一直运行到函数结束，直到 return 语句为止，并将 return 语句后面的表达式的值，作为返回的对象的 value 属性值。

4.如果该函数没有 return 语句，则返回的对象的 value 属性值是 undefined。

#### 与 return 的异同

##### 相同

返回紧跟在语句后面的表达式的值

##### 区别

1. yield 会暂停操作，下一次继续从这个位置执行。但是 return 语句只能执行一次。但是 yield 可以执行多次返回多个值，因为有多个 yield 。

2. yield 表达式只能在 Generator 函数里面使用，在其余地方使用会报错。


