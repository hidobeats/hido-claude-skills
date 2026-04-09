# Micro-interactions

| Effect | Technique | Pattern |
|--------|-----------|---------|
| **Button Ripple** | CSS `::after` + JS coords | Pseudo-element scales from click point with opacity fade |
| **Button Press** | CSS `:active` | `transform: scale(0.96)` on active, 150ms ease-out |
| **Toggle/Switch** | CSS `translateX` transition | Thumb slides via `translateX(var(--offset))`, track color transitions |
| **Skeleton Shimmer** | CSS `@keyframes` gradient | `background-size: 200%`, animated `translateX` gradient sweep |
| **Success Check** | SVG `stroke-dashoffset` | Draw-on checkmark triggered by state change |
| **Error Shake** | CSS `@keyframes` | Quick `translateX(+-8px)` oscillation, 400ms, 4-6 stops |
| **Toast Notification** | Framer Motion | Slide in from edge + auto-dismiss with exit animation |
| **Accordion** | CSS `grid-template-rows` | Transition `grid-template-rows: 0fr` → `1fr` for smooth collapse |
| **Modal Enter/Exit** | Framer Motion | `AnimatePresence` with scale + opacity + backdrop blur |
| **Tab Indicator** | Framer Motion `layoutId` | Shared layout animation for active tab underline |
| **Tooltip** | CSS + JS positioning | Fade + translateY with proper viewport-aware positioning |
| **Progress Bar** | CSS `scaleX` transition | `transform: scaleX(progress)` with `transform-origin: left` |
| **Confetti** | Canvas 2D | Particle burst with gravity, rotation, and color variety |
| **Pull to Refresh** | Touch events + CSS | Overscroll indicator with spring-back animation |

## Lottie vs Rive

| Dimension | Lottie | Rive |
|-----------|--------|------|
| Source | After Effects → Bodymovin → JSON | Rive Editor → .riv binary |
| File size | 10-200 KB | 5-50 KB |
| Interactivity | Play/pause/seek | State machines, inputs, blend |
| React | `lottie-react` | `@rive-app/react-canvas` |
| Performance | Good (SVG/Canvas) | Excellent (GPU Canvas) |
| Assets | Huge (LottieFiles) | Growing |
| Best for | Illustrations, loaders, marketing | Interactive icons, gamified UI |
