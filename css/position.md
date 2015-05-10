### 包含块（定位上下文）

* 在 HTML 中，根元素就是 html 元素，不过有些浏览器会用 body 作为根元素。

* 对于一个非根元素，如果 position 为 relative 或 static ，包含块则由最近的块级框、表单元格或行内块祖先框的内容边界构成。比如有如下代码：
  
  ```html
  <style>
    p span {
      position: relative;
      top: 10px;
      left: 20px;
    }
  </style>
  <p>
    Hello <span>world!</span>
  </p>
  ```

* 对于一个非根元素，如果 position 为 absolute ，包含块设置为最近的 position 不是 static 的祖先元素（可以是任何类型）。

  这个过程如下：

  - 如果这个祖先元素是块级元素，包含块则设为该元素的内边距边界；
  - 如果这个元素是行内元素，包含块则设置为该祖先元素中的内容边界；
  - 如果没有祖先，元素的包含块定义为初始包含块。

* 对 position 为 relative 、 absolue 和 fixed 的元素设置 top 、 right 、 bottom 、left 为百分数的时候， top 、 bottom 是相对于包含块的高度的， right 、 left 是相对于包含块的宽度的。
* 对于绝对定位元素，如果 top 设置为 auto ，则该定位元素的顶端要相对于其未定位前本来的顶端位置对齐。left 、 right 也是这样。
  
  - 当设置 left 为 auto 时，元素的左边界会相对于包含块的左边界放置；
  - 当设置 top 为 auto 时，

* position 为 absolute 的元素，其 height 设置为百分数的时候，具体高度是相对于包含块来计算的，而 fixed 是相对于根元素计算的，例如：[https://jsfiddle.net/yibuyisheng/hrL23vct/](https://jsfiddle.net/yibuyisheng/hrL23vct/)。但是如果直接设置 height 为 inherit 的话，就直接从父元素继承高度了，而不再是包含块。
