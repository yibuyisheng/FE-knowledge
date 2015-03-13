* IE6/7 下，navigator 对象在父窗口和 iframe 之间是共享的。
* 可以利用 iframe 来避免当前页面的原生内容污染。比如有人修改了 Array.prototype.slice 方法，为了使用到纯正的 slice 方法，则可以新建一个 iframe，从这个 iframe 中获取 slice 方法。
* [Comet：基于 HTTP 长连接的“服务器推”技术](http://www.ibm.com/developerworks/cn/web/wa-lo-comet/)。
* [JavaScript 跨域总结与解决办法](http://www.cnblogs.com/rainman/archive/2011/02/20/1959325.html)。
* 纯前端的utf8和gbk编码互转。比如在utf8页面需要生成一个gbk的encodeURIComponent字符串，可以通过页面加载一个gbk的iframe，然后主页面与子页面通信的方式实现转换，这样就不用在页面上插入一个非常巨大的编码映射表文件了，其中子页面内容：
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
  把这个iframe部署到父页面的同源服务上，就能在父页面直接调用iframe中的encoding接口了。
