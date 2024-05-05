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

## Contributing
If you have ideas for improvements or find a bug, please feel free to fork this repository, make changes, and submit a pull request! We appreciate any contributions that improve the functionality and usability of this expression.

## License
This project is licensed under the MIT License. Below is a summary and the full text can be found in the LICENSE file in this repository:

```
MIT License

Copyright (c) [year] [your name or organization]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
