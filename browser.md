* IE6/7 下，navigator 对象在父窗口和 iframe 之间是共享的。
* 可以利用 iframe 来避免当前页面的原生内容污染。比如有人修改了 Array.prototype.slice 方法，为了使用到纯正的 slice 方法，则可以新建一个 iframe，从这个 iframe 中获取 slice 方法。
* [Comet：基于 HTTP 长连接的“服务器推”技术](http://www.ibm.com/developerworks/cn/web/wa-lo-comet/)。
* [JavaScript 跨域总结与解决办法](http://www.cnblogs.com/rainman/archive/2011/02/20/1959325.html)。
* 纯前端的 utf8 和 gbk 编码互转。比如在 utf8 页面需要生成一个 gbk 的 encodeURIComponent 字符串，可以通过页面加载一个 gbk 的 iframe ，然后主页面与子页面通信的方式实现转换，这样就不用在页面上插入一个非常巨大的编码映射表文件了，其中子页面内容：

  ```html
  <!doctype html>
  <html>
    <head>
      <meta charset="gbk">
      <script>
        window.encoding = function(str){
          //利用a元素的href属性来encode
          var a = document.createElement("a");
          a.href = "/?q=" + str;
          var url = a.href; //这里读取的时候会自动编码
          a.href = "/?q=";
          return url.replace(a.href, "");
        };
      </script>
    </head>
  </html>
  ```

  把这个 iframe 部署到父页面的同源服务上，就能在父页面直接调用 iframe 中的 encoding 接口了。

* 从 IE5 开始，IE 支持 attachEvent() 、 detachEvent() 。

* attachEvent() 允许相同的事件处理程序函数注册多次，当特定的事件类型发生时，注册函数的调用次数和注册次数一样。

* 通常调用事件处理程序时把事件对象作为它们的一个参数。在 IE8 及以前版本中，通过设置属性注册事件处理程序，当调用它们时并未传递事件对象，取而代之，需要通过全局对象 window.event 来获得事件对象。

* 使用 attachEvent() 注册的处理程序作为函数调用，它们的 this 值是全局 Window 对象。

* 通常情况下，通过设置对象属性或 HTML 属性来添加事件回调函数，在函数返回 false 的时候可以阻止这个事件相关的默认操作。在支持 addEventListener() 的浏览器中，通过调用事件对象的 preventDefault() 方法取消事件的默认操作。在 IE9 之前的 IE 中，设置事件对象的 returnValue 属性为 false 来达到同样的效果。

* 当某个事件发生时，浏览器必须按如下规则调用所有的事件处理程序：

  - 通过设置对象属性或 HTML 属性注册的处理程序一直优先调用；
  - 使用 addEventListener() 注册的处理程序按照它们的注册顺序调用；
  - 使用 attachEvent() 注册的处理程序可能按照任何顺序调用。

* focus 、 blur 、 scroll 不会冒泡；文档元素上的 load 事件会冒泡，但会在 Document 对象上停止冒泡而不会传播到 Window 对象。只有当整个文档都加在完毕时才会触发 Window 的 load 事件。

* 在支持 addEventListener() 的浏览器中，调用 stopPropagation() 来阻止事件继续传播，包括捕获阶段、事件目标本身中和冒泡阶段； IE9 之前的 IE 通过 cancelBubble 设置为 true 来阻止传播。

* stopImmediatePropagation()

* 当文档准备就绪时调用函数：
  
  ```js
  /**
  *  DOMContentLoaded 、 readystatechange 、 或 load 事件发生的时候会触发回调
  */
  var whenReady = (function() {
    var funcs = [];
    var ready = false;
    
    function handler(e) {
      if (ready) return;
      
      if (e.type === 'readystatechange' && document.readystate !== 'complete') {
        return;
      }
      
      for (var i = 0, il = funcs.length; i < il; i++) {
        funcs[i].call(document);
      }
      
      ready = true;
      funcs = null;
    }
    
    if (document.addEventListener) {
      document.addEventListener('DOMContentLoaded', handler, false);
      document.addEventListener('readystatechange', handler, false);
      window.addEventListener('load', handler, false);
    } else if (document.attachEvent) {
      document.attachEvent('onreadystatechange', handler);
      window.attachEvent('onload', handler);
    }
    
    return function whenReady(f) {
      if (ready) f.call(document);
      else funcs.push(f);
    }
  })();
  ```
  
* 在 IE8 和 IE7 下，通过相邻选择符（+）指定样式的元素，并不能和动态的添加 class 或者动态插入元素等很好合作，比如下面例子：

  ```html
  <span id='span1'>span1</span>
  <span>span2</span>
  <button id='btn'>select span1</button>
  
  #span1.selected + span {
      background-color:red;
  }
  
  $('#btn').click(function() {
      $('#span1').addClass('selected');
  });
  ```
  
  在 IE8 和 IE7 下，点击按钮 btn 之后，第二个 span 标签的背景色并不会变为红色，此时可以通过在父元素上切换 class 使其重绘，从而正常显示颜色。
  
*   ie8 splice() 下有问题，只会改变 length ，并设置元素索引，但不会删除元素：
  
  ```js
  var t = {0:'a', 1: 'b', 2:'c', 3:'d', length: 4};
  [].splice.call(t, 3, 1);
  alert(t.length)
  for(var k in t) {
      alert(k+ ':' + t[k])
  }
  ```

* IE6/IE7 不支持中括号形式获取指定位置的字符（str[0]）。

* chrome 清除 DNS cache ： chrome://net-internals/#dns 。

* 通过 CSSOM API 获取带前缀的样式值的时候，有坑：比如要获取 transform 的值，在较新的浏览器中，可以使用 `element.style['-webkit-transform']` 或者 `element.style.transform` 或者 `element.style.webkitTransform`，但是在较老版本浏览器中，就只能用 `element.style.webkitTransform` ，而老火狐更奇怪，要使用 `element.style.MozTransform` 。
