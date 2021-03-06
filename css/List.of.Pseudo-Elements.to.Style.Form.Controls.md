## 一组用于给表单控件添加样式的伪元素选择器

在开发 web 应用的时候，给表单元素添加样式是非常痛苦的。由于历史的原因， web 开发者不得不接受浏览器提供的表单控件外表，顶多只能做一小点的改动。但是， web 渲染引擎开始提供一些伪元素选择器用于控制表单控件的外观。

所有这些伪元素都是特定于渲染引擎的（因此带有特定的前缀），但是仍然可以很方便在相应渲染引擎下面使用。下面是我尝试过的最好的完整的可以运行于 Trident 、Gecko 和 WebKit 渲染引擎的组合。

几点注意：

* 此处罗列的所有的 Trident 伪元素都在 IE10 中引入，将不会在老版本的 IE 浏览器中生效。
* 在 WebKit 引擎中，为了设置某些伪元素的样式，你必须先将基础元素的 `-webkit-appearance` 伪类设置为 `none` 。例如，为了给 `::-webkit-progress-bar` 设置样式，你必须给相应的 `<progress>` 元素设置 `-webkit-appearance: none;` 。

内容导航：

* &lt;input&gt; 元素

  - [button](#inputtypebutton)
  - [checkbox / radio](#inputtypecheckbox--inputtyperadio)
  - [color](#inputtypecolor)
  - [date](#inputtypedate)
  - [file](#inputtypefile)
  - [number](#inputtypenumber)
  - [password](#inputtypepassword)
  - [placeholder attribute](#placeholder-%E5%B1%9E%E6%80%A7)
  - [range](#inputtyperange)
  - [reset](#inputtypereset)
  - [search](#inputtypesearch)
  - [submit](#inputtypesubmit)
  - [text](#inputtypetext)

* 其它元素

  - [button](#button-%E5%85%83%E7%B4%A0)
  - [keygen](#keygen-%E5%85%83%E7%B4%A0)
  - [meter](#meter-%E5%85%83%E7%B4%A0)
  - [progress](#progress-%E5%85%83%E7%B4%A0)
  - [select](#select-%E5%85%83%E7%B4%A0)
  - [textarea](#textarea-%E5%85%83%E7%B4%A0)

#### input[type=button]

  **Gecko**

  参考 [&lt;button&gt;](#button-%E5%85%83%E7%B4%A0)

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
  
  参考 [&lt;button&gt;](#button-%E5%85%83%E7%B4%A0)

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
  
  参考 [&lt;button&gt;](#button-%E5%85%83%E7%B4%A0)
  
#### input[type=text]

  **Trident**

  在 IE10 的 Trident 引擎中，提供了 `::-ms-value` 伪元素来给文本输入框（ `input[type=text]` ， `input[type=password]` ， 等等）和 `<select>` 的值部分添加样式。例如：

  ```html
  <input type="text" value="value">
  <input type="password" value="value">
  <select><option selected>option</option></select>
  ```

  ```css
  ::-ms-value {
      color: red;
      background: black;
      padding: 1em;
  }
  ```

  这在 Windows 8 的 IE10 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-value.png)

  **清除控件（ Clear Control ）**

  在 IE10 中，当一个文本输入框获取到了焦点并且不为空的时候，一个小 X 控件出现在输入框的右侧。当点击的时候，控件将会清除文本框的内容。可以用 `::-ms-clear` 伪元素来给它添加样式。因此你可以隐藏这个 X 控件：

  ```html
  <input type="text">
  ```

  ```css
  ::-ms-clear { display: none; }
  ```

  这在 Windows 8 的 IE10 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-input-clear.png)

  `::-ms-clear` 接受很多样式规则，因此你也可以给 X 控件添加样式主题：

  ```html
  <input type="text" value="Lorem Ipsum">
  ```

  ```css
  ::-ms-clear {
      color: red;
      background: black;
      padding: 1em;
  }
  ```

  这会显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-input-clear-fancy.png)

#### &lt;button&gt; 元素

  **Gecko**

  Gecko 给类型为 `button` ， `reset` ， 和 `submit` 的输入元素提供了 `::-moz-focus-outer` 和 `::-moz-focus-inner` 伪元素，同时也为 `&lt;button&gt;` 元素提供了。

  用这些伪元素并不能做太多的事情，但是有一件重要的事情必须要清楚。 Gecko 默认情况下给 `::-moz-focus-inner` 添加了 `padding` 和 `border` ：

  ```html
  button::-moz-focus-inner,
  input[type="reset"]::-moz-focus-inner,
  input[type="button"]::-moz-focus-inner,
  input[type="submit"]::-moz-focus-inner,
  input[type="file"] > input[type="button"]::-moz-focus-inner {
      border: 1px dotted transparent;
      padding: 0 2px;
  }
  ```

  这些规则可以轻易使控件的外观在 Gecko 中看起来和其它渲染引擎中不一样。这使人很困惑，实际上[有一种方法来移除它](https://bugzilla.mozilla.org/show_bug.cgi?id=140562)。

  默认的 `padding` 和 `border` 可以重置为 0：

  ```css
  button::-moz-focus-inner,
  input::-moz-focus-inner {
      border: 0;
      padding: 0;
  }
  ```

  在 OS X 的 FireFox 19 中，重置之前和重置之后的样子如下：

  ![](http://tjvantoll.com/images/posts/2013-04-15/gecko-buttons.png)

#### &lt;keygen&gt; 元素

  **WebKit**

  WebKit 提供 `::-webkit-keygen-select` 伪元素用于自定义 keygen 元素使用的下拉框。例如：

  ```html
  <keygen>
  ```

  ```css
  ::-webkit-keygen-select {
      background: black;
      color: red;
  }
  ```

  这在 OS X 的 Chrome 26 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-keygen.png)

#### &lt;meter&gt; 元素

  **WebKit**

  WebKit 提供了 `::-webkit-meter-bar` ， `::-webkit-meter-even-less-good-value` ， `::-webkit-meter-optimum-value` ， 和 `::-webkit-meter-suboptimal-value` 伪元素来自定义 meter 元素的外观。

  为了给伪元素添加样式，必须要在 meter 元素上设置 `-webkit-appearance` 为 `none` 。

  在某个时间点，根据 meter 的值， `::-webkit-meter-even-less-good-value` ， `::-webkit-meter-optimum-value` ， 和 `::-webkit-meter-suboptimal-value` 中只有一个生效。

  如下所示：

  ```html
  <meter low="69" high="80" max="100" optimum="100" value="92">A</meter>
  <meter low="69" high="80" max="100" optimum="100" value="72">C</meter>
  <meter low="69" high="80" max="100" optimum="100" value="52">E</meter>
  ```

  ```css
  meter { -webkit-appearance: none; }
  ::-webkit-meter-bar {
      height: 50px;
      background: white;
      border: 2px solid black;
  }
  ::-webkit-meter-optimum-value { background: green; }
  ::-webkit-meter-suboptimum-value { background: orange; }
  ::-webkit-meter-even-less-good-value { background: blue; }
  ```

  这在 OS X 中的 Chrome 26 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-meter.png)

#### &lt;progress&gt; 元素

  **WebKit**

  WebKit 提供 `::-webkit-progress-inner-element` ， `::-webkit-progress-bar` ， 和 `::-webkit-progress-value` 给进度元素添加样式，层级结构如下：

  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-progress-shadow.png)

  像 meter 一样，为了给这些元素应用样式，必须在进度元素上设置 `-webkit-appearance: none;` 。这里有个例子：

  ```html
  <progress max="100" value="50"></progress>
  ```

  ```css
  progress { -webkit-appearance: none; }
  ::-webkit-progress-inner-element { }
  ::-webkit-progress-bar { border: 2px solid black; }
  ::-webkit-progress-value { background: red; }
  ```

  这在 OS X 的 Chrome 26 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-progress.png)

  **Gecko**

  Gecko 提供 ::-moz-progress-bar 伪元素来给进度条本身添加样式。例如：

  ```html
  <progress max="100" value="50"></progress>
  ```

  ```css
  ::-moz-progress-bar { background: red; }
  ```

  这在 OS X 的 FireFox 19 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/gecko-progress.png)

  **Trident**

  像 Gecko 一样， Trident 提供了一个伪元素来给进度条添加样式， `::-ms-fill` 。例如：

  ```html
  <progress max="100" value="50"></progress>
  ```

  ```css
  ::-ms-fill { background: red; }
  ```

  这在 Windows 8 的 IE10 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-progress.png)

#### &lt;select&gt; 元素

  **Trident**

  在 IE10 中， Trident 提供了 `::-ms-expand` 来给 select 下拉框中的箭头添加样式，例如：

  ```html
  <select>
      <option selected>One</option>
  </select>
  ```

  ```css
  ::-ms-expand {
      padding: 2em;
      color: red;
      background: black;
  }
  ```

  这在 Windows 8 的 IE10 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/trident-select.png)

#### &lt;textarea&gt; 元素

  **WebKit**

  WebKit 提供 `::-webkit-resizer` 伪元素来给自动添加到 textarea 元素右下角的控制输入框大小的控件设置样式。

  可以用 `display: none` 或者 `-webkit-appearance: none` 来隐藏它：

  ```html
  <textarea></textarea>
  ```

  ```css
  ::-webkit-resizer {
      display: none;
  }
  ```

  这在 OS X 的 Chrome 26 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-textarea-hide.png)

  注意：给 `::-webkit-resizer` 添加 `display: none` 并不能阻止用户改变 textarea 的大小，仅仅是隐藏改变大小的按钮而已。如果想禁止改变大小，设置[改变大小的 CSS 属性](https://developer.mozilla.org/en-US/docs/CSS/resize)为 `none` 。这同样也可以隐藏改变大小的按钮，同时在支持 textarea 改变大小的浏览器中都有效果。

  `::-webkit-resizer` 伪元素也接受一些基本的样式。如果你觉得改变大小的控件应该显示更有意义的颜色，你可以添加如下代码：

  ```html
  <textarea></textarea>
  ```

  ```css
  ::-webkit-resizer {
      border: 2px solid black;
      background: red;
      box-shadow: 0 0 5px 5px blue;
      outline: 2px solid yellow;
  }
  ```

  这在 OS X 的 Chrome 26 中显示成这样：

  ![](http://tjvantoll.com/images/posts/2013-04-15/webkit-textarea-style.png)

