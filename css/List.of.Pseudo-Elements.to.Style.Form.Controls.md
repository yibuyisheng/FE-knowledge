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
  
#### input[type=file]

  所有的渲染引擎在 `<input type="file">` 创建的时候都会生成一个按钮。由于历史的原因，这个按钮完全不能自定义样式。但是，最近 Trident 和 WebKit 通过伪元素提供了修改样式的手段。
  
  **Trident**
  
  在 IE10 中，文件输入按钮可以通过使用 `::-ms-browse` 伪类来添加样式。基本上可以应用在普通按钮上的 CSS 规则都可以应用到这个伪类上面。例如：
  
  ```html
  <input type="file">
  ```
  
  ```css
  ::-ms-browse {
      background: black;
      color: red;
      padding: 1em;
  }
  ```
  
  这在 Windows 8 的 IE10 浏览器中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-input-file.png)
  
  **WebKit**
  
  Webkit 提供了 `::-webkit-file-upload-button` 伪类。也可以应用相当多的 CSS 规则，因此上述 Trident 中的示例此时也有效：
  
  ```html
  <input type="file">
  ```
  
  ```css
  ::-webkit-file-upload-button {
      background: black;
      color: red;
      padding: 1em;
  }
  ```
  
  这在 OS X 的 Chrome 26 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-input-file.png)
  
#### input[type=number]

  **WebKit**
  
  WebKit 默认情况下给数字输入框提供了一个增加减少小控件。伪元素 ::-webkit-textfield-decoration-container ， ::-webkit-inner-spin-button 和 ::-webkit-outer-spin-button 用于自定义样式。由于你不能用这些伪元素做很多默认样式修改，所以把增加减少控件隐藏起来的做法是很有用的。
  
  ```html
  <input type="number">
  ```
  
  ```css
  ::-webkit-textfield-decoration-container { }
  ::-webkit-inner-spin-button {
      -webkit-appearance: none;
  }
  ::-webkit-outer-spin-button {
      -webkit-appearance: none;
  }
  ```
  
  这在 OS X 的 Chrome 26 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-input-number.png)
  
  
#### input[type=password]

  **Trident**
  
  Trident 给密码输入框提供了一个按钮控件，点击该按钮后可以看到密码的明文形式。这个控件可通过 `::-ms-reveal` 伪元素来自定义外观。你可以改变很多该控件的样式，包括 `color` ， `background` ，或者用 `display` 来隐藏控件。下列代码就可以隐藏控件：
  
  ```html
  <input type="password">
  ```
  
  ```css
  ::-ms-reveal { display: none; }
  ```
  
  这在 Windows 8 的 IE10 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-input-password.png)
  
  
#### placeholder 属性

  **Gecko**
  
  Gecko 提供了 `::-moz-placeholder` 伪元素来给 placeholder 文本添加样式。你可以用它来改变 placeholder 文本的颜色或者字体属性。例如：
  
  ```html
  <input placeholder="placeholder">
  ```
  
  ```css
  ::-moz-placeholder {
      color: blue;
      font-family: 'Comic Sans MS';
  }
  ```
  
  这在 OS X 的 FireFox 20 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/gecko-placeholder.png)
  
  _注意： Gecko 在 FireFox 19 中将伪类 `:-moz-placeholder` 改成了伪元素 ::-moz-placeholder_
  
  **Trident**
  
  Trident 通过伪类而不是伪元素来给 placeholder 文本添加样式。但是这个伪类， `:-ms-input-placeholder` ，可以像其它渲染引擎中伪元素的一样使用：
  
  ```html
  <input placeholder="placeholder">
  ```
  
  ```css
  :-ms-input-placeholder {
      color: blue;
      font-family: 'Comic Sans MS';
  }
  ```
  
  这在 Windows 8 的 IE10 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-placeholder.png)
  
  **WebKit**
  
  WebKit 使用 `::-webkit-input-placeholder` 伪元素。同样也可以改变 placeholder 文本的颜色和字体：
  
  ```html
  <input placeholder="placeholder">
  ```
  
  ```css
  ::-webkit-input-placeholder {
      color: blue;
      font-family: 'Comic Sans MS';
  }
  ```
  
  这在 OS X 的 Chrome 26 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-placeholder.png)
  
#### input[type=range]

  **Gecko**
  
  在 FireFox 22 中， Gecko 提供了 `::-moz-range-track` 伪类和 `::-moz-range-thumb` 伪类来给范围输入框添加样式。可以给这些伪元素添加大多数的 CSS 样式规则，例如：
  
  ```html
  <input type="range">
  ```
  
  ```css
  ::-moz-range-track {
      border: 2px solid red;
      height: 20px;
      background: orange;
  }
  ::-moz-range-thumb {
      background: blue;
      height: 30px;
  }
  ```
  
  这在 OS X 的 FireFox 22 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/gecko-input-range.png)
  
  **Trident**
  
  Trident 提供了很多的伪元素来控制范围选择器的样式。
  
  * `::-ms-fill-lower` ： The track portion underneath / before the handle.
  * `::-ms-fill-upper` ： The track portion above / after the handle.
  * `::-ms-ticks-before` ： An area above / before the range track with tick marks.
  * `::-ms-ticks-after` ： An area below / after the range track with tick marks.
  * `::-ms-thumb` ： The handle.
  * `::-ms-track` ： The range track itself.
  * `::ms-tooltip` ： The tooltip that appears when the user is selecting a value with the range selector. Note that this element cannot be styled, only hidden using `display: none`.
  
  用例子来展示这些显得更加简单生动。有如下代码：
  
  ```html
  <input type="range">
  ```
  
  ```css
  ::-ms-fill-lower { background: orange; }
  ::-ms-fill-upper { background: green; }
  ::-ms-thumb { background: red; }
  ::-ms-ticks-after { display: block; color: blue; }
  ::-ms-ticks-before { display: block; color: black; }
  ::-ms-track { padding: 20px 0; }
  ::-ms-tooltip { display: none; /* display and visibility only */ }
  ```
  
  
  这在 Windows 8 的 IE10 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-input-range.png)
  
  **WebKit**
  
  WebKit 提供 `::-webkit-slider-runnable-track` 伪元素给滑道， `::-webkit-slider-thumb` 给范围控制块。虽然不能用这些伪元素做太多的事情，但是还是可以添加一些颜色和内边距：
  
  ```html
  <input type="range">
  ```
  
  ```css
  ::-webkit-slider-runnable-track {
      border: 2px solid red;
      background: green;
      padding: 2em 0;
  }
  ::-webkit-slider-thumb {
      outline: 2px solid blue;
  }
  ```
  
  这在 OS X 的 Chrome 26 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-input-range.png)
  
  最后一点关于范围输入框的注意点是， Trident 和 Webkit 允许给小滑块伪元素添加 hover 样式（分别用 ::-webkit-slider-thumb:hover 和 ::-ms-thumb:hover ），但是 Gecko 目前还不支持。
  
#### input[type=reset]

  **Gecko**
  
  参考 [&lt;button&gt;](#)

#### input[type=search]

  **WebKit**
  
  默认情况下 WebKit 给 search 输入框提供了取消和搜索按钮。两个伪元素， `::-webkit-search-cancel-button` 和 `::-webkit-search-results-button` 用于自定义样式，虽然不能用它们做太多的事情，除了像下面一样隐藏它们：
  
  ```html
  <input type="search">
  ```
  
  ```css
  /* Remove the rounded corners */
  input[type=search] { -webkit-appearance: none; }
  
  /* Hide the cancel button */
  ::-webkit-search-cancel-button { -webkit-appearance: none; }
  
  /* Hide the magnifying glass */
  ::-webkit-search-results-button { -webkit-appearance: none; }
  ```
  
  这在 OS X 的 Chrome 26 中显示成这样：
  
  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-input-search.png)
  
#### input[type=submit]

  **Gecko**
  
  参考 [&gt;button&lt;](#)
  
#### input[type=text]
  
  
  
  
  
  
