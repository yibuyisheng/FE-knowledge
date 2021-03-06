* "user strict" 是 ECMAScript 5 引入的一条指令。只能出现在脚本代码的开始或者函数体的开始、任何实体语句之前。但它不必一定出现在脚本的首行或函数体的首行，因为 "use strict" 指令之后或之前都可能有其他字符串直接量表达式语句，并且 JavaScript 的具体实现可能将它们解析为解释器自有的指令。在脚本或者函数体内第一条常规语句之后字符串直接量表达式语句只当做普通的表达式语句对待；它们不会当做指令解析，它们也没有任何副作用。

* 严格模式和非严格模式的区别如下：

  - 在严格模式中禁止使用 with 语句。
  - 在严格模式中，所有变量都要事先声明，如果给一个未声明的变量、函数、函数参数、catch 从句参数或全局对象的属性赋值，将会抛出一个引用错误异常（在非严格模式中，这种隐式声明的全局变量的方法是给全局对象新增一个属性）。
  - 在严格模式中，调用函数（不是方法）中的一个 this 值是 undefined 。（在非严格模式中，调用的函数中的 this 值总是全局对象）。可以利用这种特性来判断 JavaScript 实现是否支持严格模式：
  
  ```js
  var hasStrictMode = (function () { "use strict"; return this === undefined; });
  ```
  
  - 在严格模式中，当通过 call() 或 apply() 来调用函数时，其中的 this 值就是通过 call() 或 apply() 传入的第一个参数（在非严格模式中， null 和 undefined 值被全局对象和转换为对象的非对象值所代替）。
  
  - 在严格模式中，给只读属性赋值和给不可扩展的对象创建新成员都将抛出一个类型错误异常（在非严格模式中，这些操作只是简单地操作失败，不会报错）。
  
  - 在严格模式中，传入 eval() 的代码不能在调用程序所在的上下文中声明变量或定义函数，而在非严格模式中是可以这样做的。相反，变量和函数的定义是在 eval() 创建的新作用域中，这个作用域在 eval() 返回时就弃用了。
  
  - 在严格模式中，函数里的 arguments 对象拥有传入函数值的静态副本。在非严格模式中，arguments 里的数组元素和函数参数都是指向同一个值的引用。
  
  - 在严格模式中，当 delete 运算符后跟随非法的标识符（比如变量、函数、函数参数）时，将会抛出一个语法错误异常（在非严格模式中，什么也不做，返回 false ）。
  
  - 在严格模式中，试图删除一个不可配置的属性将抛出一个类型错误异常（在非严格模式中，delete 表达式操作失败，并返回 false ）。
  
  - 在严格模式中，在一个对象直接量中定义两个或多个同名属性将产生一个语法错误（在非严格模式中不会报错）。
  
  - 在严格模式中，函数声明中存在两个或多个同名的参数将产生一个语法错误（在非严格模式中不会报错）。
  
  - 在严格模式中是不允许使用八进制整数直接量（以0为前缀，而不是0x为前缀）的（在非严格模式中某些实现是允许八进制整数直接量的）。
  
  - 在严格模式中，标识符 eval 和 arguments 当做关键字，它们的值是不能更改的。不能给这些标识符赋值，也不能把它们声明为变量、用做函数名、用做函数参数或用做 catch 块的标识符。
  
  - 在严格模式中限制了对调用栈的检测能力，在严格模式的函数中， arguments.caller 和 arguments.callee 都会抛出一个类型错误异常。严格模式的函数同样具有 caller 和 arguments 属性，当访问这两个属性时将抛出类型错误异常（有一些 JavaScript 的实现在非严格模式里定义了这些非标准的属性）。