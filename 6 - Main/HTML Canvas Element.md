 	2025-03-06 13:41

Status:

Tags: [[Web Development]]

---
##### ***Creating the Canvas Element***

`<canvas id="myCanvas" width="800" height="500"></canvas>`

Create the canvas element in html and with a script, you can connect to it via

```js
document.addEventListener('DOMContentLoaded', function () {
	const myCanavs = document.getElementById('myCanvas');
	const ctx = myCanvas.getContext('2d');
});
```

`ctx` or the Canvas Rendering Context 2D is what's mostly used for drawing shapes, text, images, and other objects.

##### ***Creating a Shape and line***

```js
//Creating Circle

ctx.beginPath();
ctx.arc(shape.x, shape.y, shape.radius, 0, 2 * Math.PI);
ctx.fillStyle = 'red';
ctx.fill();

//Creating Square

ctx.fillStyle = 'blue';
ctx.fillRect(shape.x, shape.y, shape.width, shape.height);

//Creating Line
ctx.beginPath();
ctx.moveTo(shape.x1, shape.y1);
ctx.lineTo(shape.x2, shape.y2);
ctx.strokeStyle = 'green';
ctx.lineWidth = 3;
ctx.stroke();
```

##### ***Panning and zooming Into Canvas***

Need 2 things:
- *Position and Scale Variables* to store the zoom, scale and position of each object so when rendering again, it uses those offsets and changes
- *Events* in order to recognise scrolling and Dragging as well as defining how that effects those variables

```js
let offsetX = 0; // Horizontal panning offset
let offsetY = 0; // Vertical panning offset
let scale = 1;   // Zoom scale
let isDragging = false; // Track mouse drag status
let lastX = 0, lastY = 0; // Store last mouse position for dragging
```

Used along side `ctx.setTransform(scale, 0, 0, scale, offsetX, offsetY);` which is called before each rendering step, with scale representing scale and offset representing translation.

##### Events for Panning

```js
canvas.addEventListener('mousedown', (e) => {
            isDragging = true;
            lastX = e.offsetX;
            lastY = e.offsetY;
            canvas.style.cursor = 'grabbing';
        });

        canvas.addEventListener('mousemove', (e) => {
            if (isDragging) {
                const dx = e.offsetX - lastX;
                const dy = e.offsetY - lastY;
                offsetX += dx;
                offsetY += dy;
                lastX = e.offsetX;
                lastY = e.offsetY;
                drawShapes();
            }
        });

        canvas.addEventListener('mouseup', () => {
            isDragging = false;
            canvas.style.cursor = 'grab';
        });

        canvas.addEventListener('mouseleave', () => {
            isDragging = false;
            canvas.style.cursor = 'grab';
        });

```

All `lastX` and `lastY` do is used to calculate the changes caused by panning.

##### Events for Zooming

``` js
canvas.addEventListener('wheel', (e) => {
    e.preventDefault();
    const zoomFactor = 0.1;
    const mouseX = e.offsetX;
    const mouseY = e.offsetY;
    
    if (e.deltaY < 0) {
        scale += zoomFactor;
    } else {
        scale -= zoomFactor;
        if (scale < 0.1) scale = 0.1; 
    }

    offsetX = mouseX - (mouseX - offsetX) * (scale / (scale + zoomFactor));
    offsetY = mouseY - (mouseY - offsetY) * (scale / (scale + zoomFactor));

    drawShapes();
});
```

`e.preventDefault();` Prevents the default action of the event that comes from scrolling (e.g. Scrolling down the page)

##### Reset

Add an event for the home button to reset each variable to 0.



##### ***Converting the Z index of a shape***

No natural Z - index so each object will need to have a  z value and before rendering each object, sort by z index so lowest values are done first so values with the highest index appear on top.
```js
// Sort shapes by z-value (lower z-value is drawn first)
shapes.sort((a, b) => a.z - b.z);
```


##### ***Selecting a shape or node on the Canvas***

Need to first get the position of the mouse in relation to the page:

```js
const rect = canvas.getBoundingClientRect();
const x = e.clientX - rect.left;
const y = e.clientY - rect.top;
```

To check if it's within  node depends on shape, but typically circle or rectangle

```js
function isMouseInNode(x, y, node) {
	const dx = x - node.x;
	const dy = y - node.y;
	return (dx * dx + dy * dy) <= (node.radius * node.radius);
}
```

Again though doing it in order of z access so you only get the highest value selected on if that's what you need.



##### ***Resizing Canvas element in scale with container***

##### ***How to create a shape via a list of vertices***

For creating a triangle

```js
ctx.moveTo(node.x, node.y - halfSize); // top point
ctx.lineTo(node.x - halfSize, node.y + halfSize); // bottom left
ctx.lineTo(node.x + halfSize, node.y + halfSize); // bottom right
ctx.closePath();
```

For another example shape

##### ***Creating a tool tip for the Canvas element***

Create a div element `<div id="tooltip"></div>` that is initially set to `display:none` but set to `block` once it is found to be over a node. 

```css
#tooltip {
	position: absolute;
	background-color: rgba(0, 0, 0, 0.7);
	color: white;
	padding: 5px;
	border-radius: 5px;
	pointer-events: none;
	display: none;
}
```

if hovering over a node

```js
canvas.addEventListener('mousemove', (e) => {
....
	if(withinNode){
		tooltip.style.display = 'block';
		tooltip.style.left = (e.clientX + 10) + 'px';
		tooltip.style.top = (e.clientY + 10) + 'px';
		tooltip.textContent = node.info;
	}
...
})
```


##### References
----
