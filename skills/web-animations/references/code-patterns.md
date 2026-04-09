# Code Patterns

## FLIP Animation (First, Last, Invert, Play)

```js
function flip(el, duration = 400) {
  const first = el.getBoundingClientRect();
  // ... apply DOM change ...
  const last = el.getBoundingClientRect();
  const dx = first.left - last.left;
  const dy = first.top - last.top;
  const sw = first.width / last.width;
  const sh = first.height / last.height;
  el.animate([
    { transform: `translate(${dx}px,${dy}px) scale(${sw},${sh})` },
    { transform: 'none' }
  ], { duration, easing: 'cubic-bezier(0.2,0,0,1)' });
}
```

React: Framer Motion `<motion.div layout layoutId="card" />` handles FLIP automatically.

## Web Animations API (WAAPI)

```js
const anim = element.animate(
  [{ opacity: 0, transform: 'translateY(1.5rem)' },
   { opacity: 1, transform: 'translateY(0)' }],
  { duration: 400, easing: 'cubic-bezier(0.16,1,0.3,1)', fill: 'forwards' }
);
await anim.finished;
element.style.opacity = '1'; // commit final state
anim.cancel();               // remove fill to free resources
```

Advantages over CSS: dynamic values, `pause()`/`reverse()`/`playbackRate`, promise-based sequencing.

## React: GSAP with Cleanup

```tsx
useEffect(() => {
  const ctx = gsap.context(() => {
    gsap.from(el.current, { opacity: 0, y: 40, duration: 0.8, ease: 'power3.out' });
  }, containerRef); // scopes selectors to container
  return () => ctx.revert(); // kills all animations + ScrollTriggers
}, []);
```

## React: AnimatePresence + Layout

```tsx
// Exit animations
<AnimatePresence mode="popLayout">
  {items.map(item => (
    <motion.div key={item.id}
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      exit={{ opacity: 0, x: -100 }} />
  ))}
</AnimatePresence>

// Shared layout animation (tab indicator, expanding cards)
<motion.div layoutId="indicator"
  transition={{ type: 'spring', stiffness: 500, damping: 30 }} />
```

## useReducedMotion Hook

```tsx
function useReducedMotion() {
  const [reduced, setReduced] = useState(false);
  useEffect(() => {
    const mq = window.matchMedia('(prefers-reduced-motion: reduce)');
    setReduced(mq.matches);
    const h = (e: MediaQueryListEvent) => setReduced(e.matches);
    mq.addEventListener('change', h);
    return () => mq.removeEventListener('change', h);
  }, []);
  return reduced;
}
```

## IntersectionObserver Reveal Pattern

```tsx
useEffect(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed');
          observer.unobserve(entry.target); // one-shot
        }
      });
    },
    { threshold: 0.15 }
  );
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
  return () => observer.disconnect();
}, []);
```

CSS companion:
```css
.reveal { opacity: 0; transform: translateY(2rem); transition: all 0.6s cubic-bezier(0.16, 1, 0.3, 1); }
.reveal.revealed { opacity: 1; transform: translateY(0); }
```
