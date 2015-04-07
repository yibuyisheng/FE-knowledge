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
