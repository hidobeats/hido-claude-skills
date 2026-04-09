---
name: web-animations
description: Animation technique selection and implementation patterns for web. Covers CSS, GSAP, Framer Motion, Canvas, WebGL, SVG, scroll effects, and cursor interactions. GPU-optimized.
---

# Web Animations

Reference for choosing and implementing website animations. Detailed effect catalogs and code patterns are in `references/` — load only what you need.

## Technique Selection

Pick the lightest technique that achieves the effect:

```
CSS keyframes/transitions
  ↓ not enough control?
IntersectionObserver + CSS classes
  ↓ need scroll-linked progress?
GSAP + ScrollTrigger
  ↓ need physics or enter/exit orchestration?
Framer Motion (React) or Web Animations API (vanilla)
  ↓ need per-pixel control?
Canvas 2D + requestAnimationFrame
  ↓ need GPU shaders or 3D?
WebGL (Three.js / OGL / raw)
```

| Technique | Best For | Dependencies | Perf Cost |
|-----------|----------|-------------|-----------|
| CSS keyframes | Loops, hovers, simple transitions | None | Lowest |
| CSS transitions + JS class toggle | Scroll reveals, state changes | None | Low |
| IntersectionObserver | Viewport-triggered animations | None | Low |
| CSS Scroll-Driven | Scroll progress, viewport reveals (no JS) | None | Lowest |
| View Transitions API | Page/route transitions, cross-view morphs | None | Low |
| WAAPI (element.animate) | JS-controlled transitions, sequencing | None | Low |
| SVG stroke/morph | Path drawing, icon animations, shape morphing | None or flubber ~5kb | Low |
| GSAP + ScrollTrigger | Scroll-scrubbed, staggered, timeline | gsap ~30kb | Medium |
| Framer Motion / motion | React enter/exit, spring physics, layout | motion ~50kb | Medium |
| Lottie | Pre-made illustration animations, loaders | lottie-web ~50kb | Medium |
| Rive | Interactive state-machine animations | @rive-app ~50kb | Medium |
| Canvas 2D | Particle systems, text distortion, trails | None | Medium-High |
| WebGL (OGL) | Lightweight shaders, iridescence, chrome | ogl ~30kb | Medium-High |
| WebGL (Three.js) | 3D scenes, heavy shader effects | three ~150kb | High |

## When NOT to Activate

- Task is backend/API only (no UI)
- User asks for static layout without motion
- Simple CSS hover that Claude already knows

## Effect References

Load per category as needed:

- `references/text-effects.md` — split reveal, blur, glitch, typewriter, gradient, morphing, sparkles
- `references/scroll-effects.md` — fade up, parallax, stagger, scroll stack, pixel transition
- `references/background-effects.md` — aurora, particles, waveform, liquid chrome, flow field, ribbons
- `references/cursor-effects.md` — spotlight card, tilt, magnet, blob cursor, splash, dock
- `references/svg-effects.md` — path drawing, shape morph, liquid distortion, glow, hamburger
- `references/micro-interactions.md` — button ripple, toggle, skeleton shimmer, toast, accordion
- `references/easing-reference.md` — CSS beziers, GSAP easing, spring physics presets
- `references/code-patterns.md` — FLIP, WAAPI, GSAP cleanup, AnimatePresence, useReducedMotion

## Performance Rules

1. **Only animate compositor properties**: `transform`, `opacity`, `clip-path`, `filter`
2. **Use `will-change` sparingly** — add before animation, remove after
3. **Canvas/WebGL cleanup** — always `cancelAnimationFrame` and remove listeners in cleanup
4. **Throttle mouse events** — use `requestAnimationFrame` guard for mousemove handlers
5. **Respect `prefers-reduced-motion`**:
   ```css
   @media (prefers-reduced-motion: reduce) {
     *, *::before, *::after {
       animation-duration: 0.01ms !important;
       transition-duration: 0.01ms !important;
     }
   }
   ```
6. **Lazy-load heavy effects** — dynamically import GSAP, Three.js, OGL only when section is near viewport
7. **Limit simultaneous Canvas/WebGL contexts** — browsers cap at ~8-16 active contexts
8. **SVG filters are CPU-only** — constrain filtered area, keep `scale` < 30 and `numOctaves` <= 3
9. **Commit WAAPI final styles** — `await anim.finished` + set final styles + `cancel()` over `fill: 'forwards'`
10. **Progressive-enhance modern APIs** — wrap `startViewTransition` and `animation-timeline` in feature checks
11. **Mobile-first strategy** — disable or simplify heavy effects (Canvas, WebGL, particles) on screens < 768px
