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

* ES6 规定， var 命令和 function 命令声明的全局变量，属于全局对象的属性； let 命令、 const 命令、 class 命令声明的全局变量，不属于全局对象的属性。

* 解构赋值

  ```js
  let [a, b, c] = [1, 2, 3];
  let [foo, [[bar], baz]] = [1, [[2], 3]];
  let [,,third] = ["foo", "bar", "baz"];
  let [head, ...tail] = [1, 2, 3, 4];
  let [a, [b], d] = [1, [2, 3], 4];
  let [foo] = false;
  let [foo] = 'Hello';
  let [x, y='b'] = ['a'];
  let [v1, v2, ..., vN ] = array;
  let [a, b, c] = new Set(["a", "b", "c"]);
  let [a, b, c, d, e] = 'hello';
  let {length : len} = 'hello'; // len === 5
  ```
  
  本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。如果解构不成功，变量的值就等于undefined。

  如果对undefined或null进行解构，会报错，这是因为解构只能用于数组或对象。其他原始类型的值都可以转为相应的对象，但是，undefined和null不能转为对象，因此报错。
  
  只要某种数据结构具有Iterator接口，都可以采用数组形式的解构赋值。
  
  由于JavaScript引擎内部，某些场合时，字符串会被转为类似数组的对象。因此，字符串也可以解构赋值。
