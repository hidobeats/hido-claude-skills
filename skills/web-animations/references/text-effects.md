# Text Animations

| Effect | Technique | Pattern |
|--------|-----------|---------|
| **Split/Stagger Reveal** | GSAP or Framer Motion | Split text to `<span>` per char, animate with stagger delay |
| **Blur Reveal** | CSS + IntersectionObserver | `filter: blur(10px)` → `blur(0)` on scroll into view |
| **Gradient Text** | CSS keyframes | `background: linear-gradient` + `background-clip: text` + animate `background-position` |
| **Shiny Sweep** | CSS keyframes | Moving `linear-gradient` highlight via `background-position` animation |
| **Glitch/Scramble** | DOM + setInterval | Replace chars with random glyphs, resolve to target over time |
| **Decrypt Reveal** | DOM + setInterval | Characters cycle through random set before settling |
| **Fuzzy/Vibrate** | Canvas 2D | Render text to canvas, displace pixels randomly per frame |
| **Typewriter** | DOM + setTimeout | Append characters sequentially with cursor blink |
| **Rotating/Cycling** | Framer Motion | AnimatePresence with 3D rotateX exit/enter per word |
| **Scroll Float** | GSAP ScrollTrigger | Per-char `yPercent` + `scaleY` scrubbed to scroll position |
| **Scroll Velocity** | GSAP ScrollTrigger | Marquee speed tied to scroll velocity |
| **Pressure/Variable** | rAF + variable font | `fontVariationSettings` per-char, axes mapped from cursor distance |
| **Circular Text** | CSS transform | Each char absolutely positioned with `rotate()` around circle |
| **Counter/CountUp** | requestAnimationFrame | Interpolate number from 0 to target over duration |
| **ASCII Art** | Canvas → text mapping | Sample canvas pixels, map brightness to character set |
| **Morphing Text** | Framer Motion | Character interpolation morphing between strings |
| **Sparkles Text** | Particle overlay | Continuous sparkle particles spawned on text surface |
| **Box Reveal** | Framer Motion | Colored box slides across to reveal text beneath |
| **Cursor Particles Typography** | Canvas 2D | `getImageData()` maps text pixels to particles that scatter on cursor proximity |
