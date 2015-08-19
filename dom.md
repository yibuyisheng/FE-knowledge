* 实现 outerHTML

    ```js
    (function () {
        if (document.createElement('div').outerHTML) return;

        function outerHTMLGetter() {
            var container = document.createElement('div');
            container.appendChild(this.cloneNode(true));
            return container.innerHTML;
        }

        function outerHTMLSetter(value) {
            var container = document.createElement('div');
            container.innerHTML = value;

            while(container.firstChild) {
                this.parentNode.insertBefore(container.firstChild, this);
            }

            this.parentNode.removeChild(this);
        }

        if (Object.defineProperty) {
            Object.defineProperty(
                Element.prototype,
                'outerHTML',
                { get: outerHTMLGetter, set: outerHTMLSetter, enumerable: false, configurable: true }
            );
        } else {
            Element.prototype.__defineGetter__('outerHTML', outerHTMLGetter);
            Element.prototype.__defineSetter__('outerHTML', outerHTMLSetter);
        }
    })();
    ```

* 在除 IE8 及更早浏览器版本外，可以使用 Window 对象的 pageXOffset 和 pageYOffset 来判断浏览器窗口的滚动条位置。正常情况下通过查询文档根节点（ document.documentElement ）来获取这些属性值，但在怪异模式下，必须在 document.body 上查询它们。

* getBoundingClientRect() 获取元素的尺寸和位置：返回元素在视口坐标中的位置，尺寸包含元素的边框和内边距。如果在内联元素上调用，则返回“边界矩形”。

* getClientRects() 获取内联元素每个独立的矩形。

* elementFromPoint()

* scrollIntoView()

* offsetWidth 、 offsetHeight 包含边框和内边距。

* offsetLeft 、 offsetTop 对于一般元素返回文档坐标，对于已定位元素的后代元素和表格单元，返回相对于祖先元素的坐标。 offsetParent 可以获取相应元素的祖先元素。

* clientWidth 、 clientHeight 包含内容和内边距。如果内边距和边框之间有滚动条，这两个值不会包含滚动条。对于内联元素，返回0。

* clientLeft 、 clientTop 返回元素的内边距的外边缘和它的边框的外边缘之间的水平距离和垂直距离，通常这些值就等于左边和上边的边框宽度。但是如果元素有滚动条，并且浏览器将这些滚动条放置在左侧或者顶部， clientWidth 和 clientHeight 也包含滚动条的宽度。对于内联元素，返回0。

* scrollWidth 和 scrollHeight 是元素的内容区加上它的内边距再加上任何溢出内容的尺寸。

* scrollLeft 、 scrollTop 指定元素滚动条位置。

* 浏览器不保证调用 form 的 submit() 方法的时候出发 submit 事件，然而，可以通过触发表单中的提交按钮来间接触发 submit 事件。

* cloneNode() 方法不会复制添加到 DOM 节点中的 JavaScript 属性，例如事件处理程序等。这个方法只复制特性、（在明确指定的情况下也复制）子节点，其他一切都不会复制。 IE 在此存在一个 bug ，即它会复制事件处理程序，所以建议在复制之前最好先移除事件处理程序。

* replaceChild() 、 appendChild() 、 insertBefore() 等将一个已经在 DOM 树中的节点对象移动到另外一个地方的过程中，会移动走一切与该对象相关的内容，比如事件属性、各种自定义属性等等。

* 浏览器对 document.doctype 的支持差别很大，可以给出如下总结：

    - IE8 及之前版本：如果存在文档类型声明，会将其错误地解释为一个注释并把它当做 Comment 节点；而 document.doctype 的值始终为 null 。
    - IE9+ 及 Firefox ： 如果存在文档类型声明，则将其作为文档的第一个子节点； document.doctype 是一个 DocumentType 节点，也可以通过 document.firstChild 或 document.childNodes[0] 访问同一个节点。
    - Safari 、 Chrome 和 Opera ： 如果存在文档类型声明，则将其解析，但不作为文档的子节点。 document.doctype 是一个 DocumentType 节点，但该节点不会出现在 document.childNodes 中。

* IE8 及较低版本不区分 ID 的大小写。

* getElementsByName() 是 HTMLDocument 类型才有的方法。

* document.anchors 文档中所有带 name 属性的 <a> 元素； document.links 文档中所有带 href 属性的 <a> 元素。
 
* 每当将事件处理程序指定给元素时，运行中的浏览器代码与支持页面交互的 JavaScript 代码之间就会建立一个连接。这种连接越多，页面执行起来就越慢。

  通过 removeChild() 、 replaceChild() 和 innerHTML 等方式从文档中移除带有事件处理程序程序的元素时，就会造成“空事件处理程序”的问题，这些无用的事件处理程序会拖慢页面运行速度，甚至造成内存泄露。比如：
  
  ```js
  var btn = document.getElementById('myBtn');
  btn.onclick = function() {
    btn.parentNode.innerHTML = 'Processing ...';
  };
  ```
  
  有的浏览器（尤其是 IE ）在这种情况下不会作出恰当地处理，它们很可能会将对元素和对事件处理程序的引用都保存在内存中。
  
  因此，如果知道某个元素即将被移除，那么最好手工移除事件处理程序。

* 如果想让 input 元素在获得焦点的时候，里面的文字全部选中，直接像下面这样干是不行的：

 ```js
 input.onfocus = function () {
   input.select(); // Chrome 出现一瞬间全选中状态，然后变为未选中；firefox 是选中和选不中交替出现。
 };
 ```
 
 可以使用下面的方法解决这个问题：
 
 ```js
 input.onfocus = function () {
   setTimeout(function () {
     input.select();
   }, 50);
 };
 ```
 
 或者：
 
 ```js
 input.onfocus = function () { this.select(); };
 input.onmouseup = function () { return false; };
 ```
