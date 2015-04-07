## 一组用于给表单控件添加样式的伪元素选择器

在开发 web 应用的时候，给表单元素添加样式是非常痛苦的。由于历史的原因， web 开发者不得不接受浏览器提供的表单控件外表，顶多只能做一小点的改动。但是， web 渲染引擎开始提供一些伪元素选择器用于控制表单控件的外观。

所有这些伪元素都是特定于渲染引擎的（因此带有特定的前缀），但是仍然可以很方便在相应渲染引擎下面使用。下面是我尝试过的最好的完整的可以运行于 Trident 、Gecko 和 WebKit 渲染引擎的组合。

几点注意：

* 此处罗列的所有的 Trident 伪元素都在 IE10 中引入，将不会在老版本的 IE 浏览器中生效。
* 在 WebKit 引擎中，为了设置某些伪元素的样式，你必须先将基础元素的 `-webkit-appearance` 伪类设置为 `none` 。例如，为了给 `::-webkit-progress-bar` 设置样式，你必须给相应的 `<progress>` 元素设置 `-webkit-appearance: none;` 。

内容导航：

* &lt;input&gt; 元素

  - button
  - checkbox / radio
  - color
  - date
  - file
  - number
  - password
  - placeholder attribute
  - range
  - reset
  - search
  - submit
  - text

* 其它元素

  - button
  - keygen
  - meter
  - progress
  - select
  - textarea

* 乱七八糟的

  - 表单验证提示信息

#### input[type=button]
  
  **Gecko**
  
  参考 [&lt;button&gt;](#)
  
#### input[type=checkbox] / input[type=radio]

  **Trident**
  
  Trident 引擎为复选框和单选框按钮控件提供了 `::-ms-check` 伪元素。例如：
  
  ```html
  <input type="checkbox">
  <input type="radio">
  ```
  
  ```css
  ::-ms-check {
      color: red;
      background: black;
      padding: 1em;
  }
  ```
  
  上述在 Windows 8 的 IE10 下面显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-radio-checkbox.png)
  
#### input[type=color]

  **WebKit**
  
  Webkit 为颜色选择器提供了两个伪元素， `::-webkit-color-swatch-wrapper` 和 `::-webkit-color-swatch` 。你可以把大量规则应用到这些元素上面，但是我还没想出任何有用的应用场景。这里有一个示例，仅仅展示了能达到改变外观的目的：
  
  ```html
  <input type="color">
  ```
  
  ```css
  ::-webkit-color-swatch-wrapper { border: 2px solid red; }
  ::-webkit-color-swatch { opacity: 0.5; }
  ```
  
  上述内容在 OS X 的 Chrome 26 上显示成这个样子：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-input-color.png)
  
#### input[type=date]

  **WebKit**
  
  下列的 8 个伪元素在 Webkit 中用于自定义日历控件的文本框外表：
  
  * ::-webkit-datetime-edit
  * ::-webkit-datetime-edit-fields-wrapper
  * ::-webkit-datetime-edit-text
  * ::-webkit-datetime-edit-month-field
  * ::-webkit-datetime-edit-day-field
  * ::-webkit-datetime-edit-year-field
  * ::-webkit-inner-spin-button
  * ::-webkit-calendar-picker-indicator

  下面是这些元素的内部结构：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-input-date-shadow.png)
  
  所以，如果你觉得日历控件应该占用更多的空间，并且带有一个奇怪的颜色板，你可以使用如下代码：
  
  ```html
  <input type="date">
  ```
  
  ```css
  ::-webkit-datetime-edit { padding: 1em; }
  ::-webkit-datetime-edit-fields-wrapper { background: silver; }
  ::-webkit-datetime-edit-text { color: red; padding: 0 0.3em; }
  ::-webkit-datetime-edit-month-field { color: blue; }
  ::-webkit-datetime-edit-day-field { color: green; }
  ::-webkit-datetime-edit-year-field { color: purple; }
  ::-webkit-inner-spin-button { display: none; }
  ::-webkit-calendar-picker-indicator { background: orange; }
  ```
  
  上述代码在 OS X 的 Chrome 26 上显示成这个样子：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-input-date.png)
  
  
