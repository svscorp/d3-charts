# A collection of useful D3 chart implementations

## 1. Simple Token Bubble Chart
File: simple-bubble-chart-tokens.html

Preview:

<img width="629" alt="image" src="https://github.com/user-attachments/assets/4ec4a709-89da-49d0-af80-9fb68115f0e8" />

If you want a simple transparent gradient - easy:
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
