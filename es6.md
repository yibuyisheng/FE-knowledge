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

