* IE6/7 下，navigator 对象在父窗口和 iframe 之间是共享的。
* 可以利用 iframe 来避免当前页面的原生内容污染。比如有人修改了 Array.prototype.slice 方法，为了使用到纯正的 slice 方法，则可以新建一个 iframe，从这个 iframe 中获取 slice 方法。
