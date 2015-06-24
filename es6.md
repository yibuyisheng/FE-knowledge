* 考虑下面代码的输出：

  ```js
  let foo = 'outer';

  function bar(func = x => foo) {
    let foo = 'inner';
    console.log(func()); // outer
  }
  
  bar();
  ```
  
  这段代码等同于：
  
  ```js
  let foo = 'outer';
  let f = x => foo;
  
  function bar(func = f) {
    let foo = 'inner';
    console.log(func()); // outer
  }
  
  bar();
  ```

* ES6规定， var 命令和 function 命令声明的全局变量，属于全局对象的属性； let 命令、 const 命令、 class 命令声明的全局变量，不属于全局对象的属性。
