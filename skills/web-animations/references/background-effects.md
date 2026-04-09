# Background Effects

| Effect | Technique | Pattern |
|--------|-----------|---------|
| **Aurora / Soft Glow** | CSS gradients + keyframes | Animated `radial-gradient` blobs with blur and movement |
| **Animated Dots/Grid** | Canvas 2D | Draw dot grid, animate based on mouse proximity |
| **Particles** | Canvas 2D | Particle class with position/velocity/acceleration per frame |
| **Waveform Bars** | Canvas 2D | Sin-wave bar heights in `requestAnimationFrame` loop |
| **Silk/Fabric** | WebGL (Three.js) | Custom GLSL fragment shader with cosine wave patterns |
| **Liquid Chrome** | WebGL (OGL) | Cosine-loop distortion shader + mouse-reactive ripple |
| **Iridescence** | WebGL (OGL) | Wave algorithm in fragment shader with color-shift math |
| **Noise/Grain** | CSS or Canvas | CSS: animated `background-position` of noise SVG. Canvas: random pixel overlay |
| **Ribbons** | WebGL (OGL) | OGL Polyline per ribbon, spring-friction physics driving point chain, custom vertex shader for thickness tapering |
| **Flow Field** | Canvas 2D | Perlin-noise-inspired vector field driving particles; trail via alpha compositing |
| **Isometric Wave Grid** | Canvas 2D | Grid rendered with `lineTo()`, distorted by sin/cos waves + mouse-proximity repulsion |
| **Glowy Waves** | Canvas 2D | 5 layered sine waves with varying amplitudes/frequencies, mouse-reactive distortion, shadow blur |
| **Hyperspeed** | WebGL (Three.js) | EffectComposer + bloom + instanced tube geometry |
| **Ballpit / Physics** | WebGL (Three.js) | Float32Array physics sim + InstancedMesh rendering |
| **Grid Scan** | CSS keyframes | Moving highlight line across grid via `translateX` animation |
| **Gradient Bends** | CSS | Multiple `conic-gradient` layers with animation |
