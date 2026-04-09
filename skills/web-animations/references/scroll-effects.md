# Scroll & Reveal Animations

| Effect | Technique | Pattern |
|--------|-----------|---------|
| **Fade Up** | IntersectionObserver + CSS | `.reveal` class adds `opacity: 1; transform: translateY(0)` |
| **Staggered Grid** | GSAP stagger | `stagger: { each: 0.05, from: 'start' }` on child elements |
| **Scroll Stack** | GSAP ScrollTrigger | Cards pin and stack with `scrub: true` |
| **Parallax Layers** | scroll event or ScrollTrigger | Different `translateY` speeds per layer |
| **Pixel Transition** | GSAP + DOM grid | Create NxN pixel divs, stagger `display: block` from random positions |
| **Infinite Scroll** | IntersectionObserver | Sentinel element triggers data append |
| **Blur Fade** | Framer Motion | Content fades in from `blur(10px)` + opacity 0 on viewport entry |
| **Cinematic Scroll Hero** | GSAP ScrollTrigger | Multi-thousand-px scroll sequence orchestrating blur/scale text, 3D device rotation, progress ring, counters |
