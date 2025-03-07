# A collection of useful D3 chart implementations

## 1. Simple Token Bubble Chart
File: simple-bubble-chart-tokens.html

Preview:

<img width="629" alt="image" src="https://github.com/user-attachments/assets/4ec4a709-89da-49d0-af80-9fb68115f0e8" />

### 1.1 If you want a simple transparent gradient - easy:
1. Replace posGradient & negGradient code with this: 
```
const bubbleGrad = defs.append("radialGradient")
    .attr("id", "bubbleGrad")
    // center the highlight slightly toward the top
    .attr("cx", "50%")
    .attr("cy", "25%")
    .attr("r", "80%");
  bubbleGrad.append("stop")
    .attr("offset", "0%")
    .attr("stop-color", "rgba(255, 255, 255, 0.25)");  // a lighter highlight
  bubbleGrad.append("stop")
    .attr("offset", "100%")
    .attr("stop-color", "rgba(102, 118, 159, 0.1)");
```

2. Replace the `node.append("circle")` with the code below:
```
node.append("circle")
    .attr("r", d => getRadius(d))
    .attr("fill", "url(#bubbleGrad)")
    .attr("stroke", "#66769f")
    .attr("stroke-width", 1.5)
    .attr("opacity", 0.9);
```

3. Enjoy the result

<img width="548" alt="image" src="https://github.com/user-attachments/assets/bf15f893-651e-4493-9d66-f5ace5ab2865" />

### 1.2 If you want draggable bubbles - easy:

1. Add functions that describe dragging:
```
function dragStarted(event, d) {
  if (!event.active) simulation.alphaTarget(0.3).restart();
  // Fix the node’s position so it follows the mouse
  d.fx = d.x;
  d.fy = d.y;
}

function dragged(event, d) {
  // Update the node’s fixed position to the current mouse
  d.fx = event.x;
  d.fy = event.y;
}

function dragEnded(event, d) {
  if (!event.active) simulation.alphaTarget(0);
  // Release the node to float again
  d.fx = null;
  d.fy = null;
}
```

2. Add dragging call to d3:

```
node.call(
  d3.drag()
    .on("start", dragStarted)
    .on("drag", dragged)
    .on("end", dragEnded)
);
```
3. Enjoy the result

<img width="433" alt="image" src="https://github.com/user-attachments/assets/2ce65f2a-6aa6-4e2b-b2c8-ae11cada0f43" />

### 1.3 If you want stickiness

Add `.force("charge", d3.forceManyBody().strength(150))` to the d3 simulation call. And enjoy the result.
