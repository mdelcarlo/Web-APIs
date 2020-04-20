# Canvas
The Canvas API provides a means for drawing graphics via JavaScript and the HTML `<canvas>` element. Among other things, it can be used for animation, game graphics, data visualization, photo manipulation, and real-time video processing.

The Canvas API largely focuses on 2D graphics. The WebGL API, which also uses the `<canvas>` element, draws hardware-accelerated 2D and 3D graphics.

## Examples
#### HTML
This code snippet adds a canvas element to your HTML document. A fallback text is provided if a browser is unable to render the canvas, or if can't read a canvas.
```html
<canvas id="canvas" width="300" height="300"> 
  An alternative text describing what your canvas displays. 
</canvas> 
```
#### JavaScript
Then in the JavaScript code, call HTMLCanvasElement.getContext() to get a drawing context and start drawing onto the canvas:
```js
var canvas = document.getElementById('canvas'); 
var ctx = canvas.getContext('2d'); 
ctx.fillStyle = 'green'; 
ctx.fillRect(10, 10, 100, 100);
```