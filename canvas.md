* 如果对 canvas 指定样式宽度和高度（例如 style="width:50px;height:50px" ），很可能会造成所绘制图像的缩放（在 canvas 标签的 width 、 height 属性和 css width 、 height 属性不一致的时候）。例如：
  ```html
  <canvas id="canvas" width="300" height="600" style="width:50px;height:50px"></canvas>
  <script>
  var canvas = document.getElementById('canvas');
  var context = canvas.getContext('2d');
  
  context.beginPath();
  context.arc(20, 20, 10, 0, Math.PI * 2, true);
  context.closePath();
  context.fillStyle = 'rgba(255, 0, 0, 0.25)';
  context.fill();
  </script>
  ```
