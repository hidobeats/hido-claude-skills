# Cursor & Interaction Effects

| Effect | Technique | Pattern |
|--------|-----------|---------|
| **Spotlight Card** | CSS + mousemove | Radial gradient follows cursor via `--x`/`--y` custom properties |
| **Tilt Card** | JS + CSS transform | `mousemove` → calculate `rotateX/Y` from cursor offset to center |
| **Magnet** | JS + CSS transform | Element pulls toward cursor within proximity threshold |
| **Blob Cursor** | Canvas or SVG | Smooth circle follows cursor with spring easing |
| **Click Spark** | Canvas or DOM | Burst of particles from click point, fade and scatter |
| **Image Trail** | GSAP + DOM | Show/position images at cursor with staggered fade-out |
| **Splash Cursor** | WebGL | Fluid simulation reacting to pointer movement |
| **Star Border** | CSS keyframes | Animated gradient orbit around element border |
| **Dock (macOS)** | Framer Motion | `useMotionValue` + `useTransform(mouseDistance, [-dist,0,dist], [base,mag,base])` + `useSpring` for proximity magnification |
| **Scratch to Reveal** | Canvas 2D | Canvas overlay with `globalCompositeOperation: 'destination-out'` on pointer drag |
| **Liquid Metal Button** | WebGL shader | `@paper-design/shaders` fragment shader, speed multiplier: 0.6x idle → 1x hover → 2.4x click |
