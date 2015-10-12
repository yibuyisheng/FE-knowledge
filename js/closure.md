* 且看如下一段代码：

  ```js
  function fn() {
    var a = 1;
    return function () {
        var a = a;
        alert(a);
    };
  }

  fn()();
  ```
