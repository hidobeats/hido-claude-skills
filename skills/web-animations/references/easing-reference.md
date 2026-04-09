# Easing Reference

## CSS Cubic Bezier

| Name | CSS Value | Use Case |
|------|-----------|----------|
| ease-out-expo | `cubic-bezier(0.16, 1, 0.3, 1)` | Snappy UI: modals, slides, enters |
| ease-out-quart | `cubic-bezier(0.25, 1, 0.5, 1)` | Smooth content reveals |
| ease-out-back | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Playful overshoot: popovers, tooltips |
| ease-in-out-quart | `cubic-bezier(0.76, 0, 0.24, 1)` | Page transitions, hero animations |
| ease-in-expo | `cubic-bezier(0.7, 0, 0.84, 0)` | Exit animations |
| spring-smooth | `cubic-bezier(0.22, 1, 0.36, 1)` | Damped spring approximation |

Store as CSS custom properties: `--ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);`

## GSAP Easing

| GSAP | Character |
|------|-----------|
| `"power1.out"` | Gentle decel |
| `"power3.out"` | Strong decel |
| `"expo.out"` | Snappy (most popular for UI) |
| `"back.out(1.7)"` | Overshoot |
| `"elastic.out(1,0.3)"` | Springy bounce |
| `"bounce.out"` | Ball-drop |

Suffix: `.in` = slow start, `.out` = slow end, `.inOut` = both.

## Spring Physics (Framer Motion)

| Param | Effect | Default |
|-------|--------|---------|
| `stiffness` | Snap speed (higher = faster) | 100 |
| `damping` | Friction (higher = less bounce) | 10 |
| `mass` | Weight (higher = sluggish) | 1 |

Presets:

- **Snappy:** `{ stiffness: 700, damping: 30 }`
- **Bouncy:** `{ stiffness: 300, damping: 10 }`
- **Smooth:** `{ stiffness: 100, damping: 20 }`
- **Heavy:** `{ stiffness: 200, damping: 20, mass: 2 }`
