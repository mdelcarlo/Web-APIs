# CanvasRenderingContext2D
The CanvasRenderingContext2D interface, part of the Canvas API, provides the 2D rendering context for the drawing surface of a `<canvas>` element. It is used for drawing shapes, text, images, and other objects.

See the interface's properties and methods in the sidebar and below. The Canvas tutorial has more explanation, examples, and resources, as well.

## Examples
#### Draw a house with canvas

[<img width="413" alt="Captura de Pantalla 2020-04-20 a la(s) 07 30 41" src="https://user-images.githubusercontent.com/20034230/79697826-0c0e4f80-82d9-11ea-86bd-f650878f499e.png">](https://jsfiddle.net/tvabLc8n/6/)

##### Code

```js
const canvas = document.getElementById('my-house');
const ctx = canvas.getContext('2d');

// Set line width
ctx.lineWidth = 5;

// Wall
ctx.strokeRect(75, 140, 150, 110);
ctx.lineWidth = 5;
// Door
ctx.fillStyle = "brown";
ctx.fillRect(130, 190, 40, 60);

// Roof
ctx.strokeStyle = "orangered";
ctx.lineWidth = 5;
ctx.beginPath();ctx.lineWidth = 5;
ctx.moveTo(50, 140);
ctx.lineTo(150, 60);ctx.lineWidth = 5;
ctx.lineTo(250, 140);
ctx.closePath();
ctx.stroke();
ctx.lineWidth = 5;
ctx.beginPath();
ctx.moveTo(80, 115);
ctx.lineTo(80, 50);
ctx.lineTo(100, 50);
ctx.lineTo(100, 100);
ctx.closePath();
ctx.strokeStyle = "black";

ctx.stroke();
```

## Reference
### Drawing rectangles
There are three methods that immediately draw rectangles to the canvas.

#### CanvasRenderingContext2D.clearRect()
Sets all pixels in the rectangle defined by starting point (x, y) and size (width, height) to transparent black, erasing any previously drawn content.
#### CanvasRenderingContext2D.fillRect()
Draws a filled rectangle at (x, y) position whose size is determined by width and height.
#### CanvasRenderingContext2D.strokeRect()
Paints a rectangle which has a starting point at (x, y) and has a w width and an h height onto the canvas, using the current stroke style.
Drawing text
The following methods draw text. See also the TextMetrics object for text properties.

#### CanvasRenderingContext2D.fillText()
Draws (fills) a given text at the given (x, y) position.
#### CanvasRenderingContext2D.strokeText()
Draws (strokes) a given text at the given (x, y) position.
#### CanvasRenderingContext2D.measureText()
Returns a TextMetrics object.

### Line styles
The following methods and properties control how lines are drawn.

#### CanvasRenderingContext2D.lineWidth
Width of lines. Default 1.0.
#### CanvasRenderingContext2D.lineCap
Type of endings on the end of lines. Possible values: butt (default), round, square.
#### CanvasRenderingContext2D.lineJoin
Defines the type of corners where two lines meet. Possible values: round, bevel, miter (default).
#### CanvasRenderingContext2D.miterLimit
Miter limit ratio. Default 10.
#### CanvasRenderingContext2D.getLineDash()
Returns the current line dash pattern array containing an even number of non-negative numbers.
#### CanvasRenderingContext2D.setLineDash()
Sets the current line dash pattern.
#### CanvasRenderingContext2D.lineDashOffset
Specifies where to start a dash array on a line.

### Text styles
The following properties control how text is laid out.

#### CanvasRenderingContext2D.font
Font setting. Default value 10px sans-serif.
#### CanvasRenderingContext2D.textAlign
Text alignment setting. Possible values: start (default), end, left, right, center.
#### CanvasRenderingContext2D.textBaseline
Baseline alignment setting. Possible values: top, hanging, middle, alphabetic (default), ideographic, bottom.
#### CanvasRenderingContext2D.direction
Directionality. Possible values: ltr, rtl, inherit (default).
### Fill and stroke styles
Fill styling is used for colors and styles inside shapes and stroke styling is used for the lines around shapes.

#### CanvasRenderingContext2D.fillStyle
Color or style to use inside shapes. Default #000 (black).
#### CanvasRenderingContext2D.strokeStyle
Color or style to use for the lines around shapes. Default #000 (black).
Gradients and patterns
#### CanvasRenderingContext2D.createLinearGradient()
Creates a linear gradient along the line given by the coordinates represented by the parameters.
#### CanvasRenderingContext2D.createRadialGradient()
Creates a radial gradient given by the coordinates of the two circles represented by the parameters.
#### CanvasRenderingContext2D.createPattern()
Creates a pattern using the specified image (a CanvasImageSource). It repeats the source in the directions specified by the repetition argument. This method returns a CanvasPattern.
### Shadows
#### CanvasRenderingContext2D.shadowBlur
Specifies the blurring effect. Default: 0
#### CanvasRenderingContext2D.shadowColor
Color of the shadow. Default: fully-transparent black.
#### CanvasRenderingContext2D.shadowOffsetX
Horizontal distance the shadow will be offset. Default: 0.
#### CanvasRenderingContext2D.shadowOffsetY
Vertical distance the shadow will be offset. Default: 0.
Paths
The following methods can be used to manipulate paths of objects.

#### CanvasRenderingContext2D.beginPath()
Starts a new path by emptying the list of sub-paths. Call this method when you want to create a new path.
#### CanvasRenderingContext2D.closePath()
Causes the point of the pen to move back to the start of the current sub-path. It tries to draw a straight line from the current point to the start. If the shape has already been closed or has only one point, this function does nothing.
#### CanvasRenderingContext2D.moveTo()
Moves the starting point of a new sub-path to the (x, y) coordinates.
#### CanvasRenderingContext2D.lineTo()
Connects the last point in the current sub-path to the specified (x, y) coordinates with a straight line.
#### CanvasRenderingContext2D.bezierCurveTo()
Adds a cubic Bézier curve to the current path.
#### CanvasRenderingContext2D.quadraticCurveTo()
Adds a quadratic Bézier curve to the current path.
#### CanvasRenderingContext2D.arc()
Adds a circular arc to the current path.
#### CanvasRenderingContext2D.arcTo()
Adds an arc to the current path with the given control points and radius, connected to the previous point by a straight line.
#### CanvasRenderingContext2D.ellipse()
Adds an elliptical arc to the current path.
#### CanvasRenderingContext2D.rect()
Creates a path for a rectangle at position (x, y) with a size that is determined by width and height.
Drawing paths
#### CanvasRenderingContext2D.fill()
Fills the current sub-paths with the current fill style.
#### CanvasRenderingContext2D.stroke()
Strokes the current sub-paths with the current stroke style.
#### CanvasRenderingContext2D.drawFocusIfNeeded()
If a given element is focused, this method draws a focus ring around the current path.
#### CanvasRenderingContext2D.scrollPathIntoView()
Scrolls the current path or a given path into the view.
#### CanvasRenderingContext2D.clip()
Creates a clipping path from the current sub-paths. Everything drawn after clip() is called appears inside the clipping path only. For an example, see Clipping paths in the Canvas tutorial.
#### CanvasRenderingContext2D.isPointInPath()
Reports whether or not the specified point is contained in the current path.
#### CanvasRenderingContext2D.isPointInStroke()
Reports whether or not the specified point is inside the area contained by the stroking of a path.

### Transformations
Objects in the CanvasRenderingContext2D rendering context have a current transformation matrix and methods to manipulate it. The transformation matrix is applied when creating the current default path, painting text, shapes and Path2D objects. The methods listed below remain for historical and compatibility reasons as SVGMatrix objects are used in most parts of the API nowadays and will be used in the future instead.

#### CanvasRenderingContext2D.currentTransform 
Current transformation matrix (SVGMatrix object).
#### CanvasRenderingContext2D.getTransform
Retrieves the current transformation matrix being applied to the context.
#### CanvasRenderingContext2D.rotate()
Adds a rotation to the transformation matrix. The angle argument represents a clockwise rotation angle and is expressed in radians.
#### CanvasRenderingContext2D.scale()
Adds a scaling transformation to the canvas units by x horizontally and by y vertically.
#### CanvasRenderingContext2D.translate()
Adds a translation transformation by moving the canvas and its origin x horzontally and y vertically on the grid.
#### CanvasRenderingContext2D.transform()
Multiplies the current transformation matrix with the matrix described by its arguments.
#### CanvasRenderingContext2D.setTransform()
Resets the current transform to the identity matrix, and then invokes the transform() method with the same arguments.
#### CanvasRenderingContext2D.resetTransform() 
Resets the current transform by the identity matrix.
Compositing
#### CanvasRenderingContext2D.globalAlpha
Alpha value that is applied to shapes and images before they are composited onto the canvas. Default 1.0 (opaque).
#### CanvasRenderingContext2D.globalCompositeOperation
With globalAlpha applied this sets how shapes and images are drawn onto the existing bitmap.
Drawing images
#### CanvasRenderingContext2D.drawImage()
Draws the specified image. This method is available in multiple formats, providing a great deal of flexibility in its use.

### Pixel manipulation
See also the ImageData object.

#### CanvasRenderingContext2D.createImageData()
Creates a new, blank ImageData object with the specified dimensions. All of the pixels in the new object are transparent black.
#### CanvasRenderingContext2D.getImageData()
Returns an ImageData object representing the underlying pixel data for the area of the canvas denoted by the rectangle which starts at (sx, sy) and has an sw width and sh height.
#### CanvasRenderingContext2D.putImageData()
Paints data from the given ImageData object onto the bitmap. If a dirty rectangle is provided, only the pixels from that rectangle are painted.
### Image smoothing
#### CanvasRenderingContext2D.imageSmoothingEnabled 
Image smoothing mode; if disabled, images will not be smoothed if scaled.#### 
CanvasRenderingContext2D.imageSmoothingQuality 
Allows you to set the quality of image smoothing.
The canvas state
The CanvasRenderingContext2D rendering context contains a variety of drawing style states (attributes for line styles, fill styles, shadow styles, text styles). The following methods help you to work with that state:

#### CanvasRenderingContext2D.save()
Saves the current drawing style state using a stack so you can revert any change you make to it using restore().
#### CanvasRenderingContext2D.restore()
Restores the drawing style state to the last element on the 'state stack' saved by save().
#### CanvasRenderingContext2D.canvas
A read-only back-reference to the HTMLCanvasElement. Might be null if it is not associated with a `<canvas>` element.
Hit regions
#### CanvasRenderingContext2D.addHitRegion() 
Adds a hit region to the canvas.
#### CanvasRenderingContext2D.removeHitRegion() 
Removes the hit region with the specified id from the canvas.
#### CanvasRenderingContext2D.clearHitRegions() 
Removes all hit regions from the canvas.
Filters
 #### CanvasRenderingContext2D.filter
Applies a CSS or SVG filter to the canvas, e.g., to change its brightness or bluriness.