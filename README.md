# After Effects Backface Culling Expression

## Overview
This repository contains a JavaScript expression designed for Adobe After Effects to implement backface culling on 3D layers. This specific expression is unique as it inversely culls the front face of layers, making a layer invisible when its front faces the camera, and visible when its back does. This is particularly useful in animation and motion graphics projects where controlling layer visibility based on orientation can enhance visual effects.

## Usage
To use this expression in your After Effects project, follow these steps:

1. **Ensure your layer is set to 3D:**
   - Toggle the 3D layer switch on your target layer in After Effects.

2. **Add the Expression to Opacity:**
   - Alt-click (Option-click on Mac) the stopwatch icon next to the Opacity property of your layer to enable expressions.
   - Copy and paste the expression from below into the expression field.

3. **Adjust as Necessary:**
   - If you need the opposite effect (visible when the front faces the camera), swap the values in the conditional operator from `(dotProduct > 0) ? 0 : 100` to `(dotProduct > 0) ? 100 : 0`.

## Expression Code
Here is the complete expression for adding to the Opacity property of your 3D layer in After Effects:

```javascript
// Calculate the dot product
var cam = thisComp.activeCamera; // Access the active camera
var toCam = normalize(cam.toWorld([0,0,0]) - thisLayer.toWorld([0,0,0])); // Vector from layer to camera
var myRotation = toWorldVec([0,0,1]); // Forward vector of the layer in world space
var dotProduct = dot(toCam, myRotation); // Dot product to determine orientation relative to camera

// Set opacity based on the dot product for inverted backface culling
thisLayer.opacity = (dotProduct > 0) ? 0 : 100; // Opacity is 0 if front face is towards the camera, 100 if back face is
// Swap the values (0 and 100) in the line above if the opposite visibility effect is desired
```
