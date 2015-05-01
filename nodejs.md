* [HOW TO SELF DETECT A MEMORY LEAK IN NODE](http://www.nearform.com/nodecrunch/self-detect-memory-leak-node/)

* V8 限制了堆内存的大小，原因是：按照官方的说法，以1.5GB的垃圾回收堆内存为例，V8做一次小的垃圾回收需要50ms以上，做一次非增量式的垃圾回收甚至要1s以上。

  这个限制也可以打开。 Node 在启动时可以传递 `--max-old-space-size` 或 `--max-new-space-size`   来调整内存限制的大小，示例如下：

  ```
  node --max-old-space-size=1700 test.js // 单位为MB
  // 或者
  node --max-new-space-size=1024 test.js // 单位为KB
  ```

  上述参数在 V8 初始化时生效，一旦生效就不能动态改变。
