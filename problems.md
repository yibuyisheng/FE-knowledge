* mac + chrome + hover + overflow 似乎有 bug，鼠标 hover 上去之后，有些东西会无故隐藏，具体原因等待查。
* 在移动端实现头像的手势缩放、拖动操作的时候，相对于本地代码，有明显的卡顿感，此时考虑是否是浏览器事件触发频率不够高（如果有输入事件控制的动画，大概率是因为事件触发频率不够吧）。

  
  > 经测试，在 iPhone 6 plus + safari （ Mozilla/5.0 (iPhone; CPU iPhone OS 8_2 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Version/8.0 Mobile/12D508 Safari/600.1.4 ） 下， touchmove 触发时间间隔至少是 16ms，以 16ms 和 17ms 居多，偶尔还会出现一两百毫秒的情况，因此，此时是不可能实现较为流畅的拖拽动画的。
  
* win 的 chrome 下，在出现滚动条的情况，只要有 canvas 绘图内存就收不回去【待验证】。
