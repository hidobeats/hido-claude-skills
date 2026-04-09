# SVG Animations

| Effect | Technique | Pattern |
|--------|-----------|---------|
| **Path Drawing** | CSS `stroke-dashoffset` | Set `dasharray` to path length, animate `dashoffset` from full to 0 |
| **Path Drawing (exact)** | JS + `getTotalLength()` | Cache path length, set as `dasharray`/`dashoffset`, transition to 0 |
| **Shape Morph (CSS)** | CSS `d` property transition | Both paths must share same command structure; `transition: d 0.6s` |
| **Shape Morph (JS)** | flubber `interpolate` | Returns `t => d` function for mismatched paths; drive t 0→1 |
| **Liquid Distortion** | SVG `feTurbulence` + `feDisplacementMap` | Animate `seed` on turbulence filter; displacement distorts source |
| **Glow Pulse** | SVG `feGaussianBlur` animate | Oscillate `stdDeviation` on blur behind source graphic |
| **Checkmark Draw** | SVG stroke animation | Single path with draw-on `dashoffset` triggered by class toggle |
| **Hamburger to X** | SVG `transform` + `opacity` | Three lines; top/bottom rotate +-45deg, middle fades |
| **Loading Spinner** | SVG `stroke-dasharray` + rotate | Layered spin (container) + dash grow/shrink (arc) |
