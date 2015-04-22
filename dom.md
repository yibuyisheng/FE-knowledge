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

* clientWidth 、 clientHeight 包含内容和内边距。如果内边距和边框之间有滚动条，这两个值不会包含滚动条。对于内联元素，返回0.

* clientLeft 、 clientTop 返回元素的内边距的外边缘和它的边框的外边缘之间的水平距离和垂直距离，通常这些值就等于左边和上边的边框宽度。但是如果元素有滚动条，并且浏览器将这些滚动条放置在左侧或者顶部， clientWidth 和 clientHeight 也包含滚动条的宽度。对于内联元素，返回0。

* scrollWidth 和 scrollHeight 是元素的内容区加上它的内边距再加上任何溢出内容的尺寸。

* scrollLeft 、 scrollTop 指定元素滚动条位置。

* 浏览器不保证调用 form 的 submit() 方法的时候出发 submit 事件，然而，可以通过触发表单中的提交按钮来间接触发 submit 事件。