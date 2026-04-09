# CLAUDE.md

## Project

- **Name:** [Project Name]
- **Stack:** React, TypeScript, Next.js (App Router), Tailwind CSS
- **Deploy:** Vercel / Netlify
- **Node:** v20+

## Architecture

```
src/
├── app/           # Next.js app router pages
├── components/    # Reusable UI components
│   ├── ui/        # Base components (Button, Input, Card)
│   └── sections/  # Page sections (Hero, Features, CTA)
├── lib/           # Utilities, helpers, constants
├── hooks/         # Custom React hooks
├── types/         # TypeScript interfaces and types
└── styles/        # Global styles
```

## Rules

- TypeScript strict mode — no `any`, no `@ts-ignore`
- Components under 300 lines — split if larger
- Use named exports, not default exports
- Tailwind only — no inline styles, no CSS modules
- All text content in constants, not hardcoded in JSX
- Mobile-first responsive design
- Images: WebP format, lazy loading, explicit width/height
- Imports: group by external → internal → types → styles

## Git

- Branch naming: `feature/description`, `fix/description`
- Conventional commits: `feat:`, `fix:`, `refactor:`, `chore:`
- Never commit `.env`, `node_modules`, `.next`
- One logical change per commit

## Performance

- PageSpeed target: 95+ mobile, 99+ desktop
- Lazy load anything below the fold
- Dynamic import for heavy libraries (Three.js, GSAP, Framer Motion)
- No layout shift — always set dimensions on images/videos
- Prefer CSS animations over JS when possible

## Do NOT

- Do not install new dependencies without asking
- Do not modify `.env` files
- Do not remove existing comments without reason
- Do not use `var` — only `const` and `let`
- Do not push directly to `main`

## Context

<!-- Add project-specific notes here -->
<!-- Example: -->
<!-- Client: Company Name -->
<!-- Design: Dark theme, neon accents -->
<!-- EmailJS for contact form — keys in .env.local -->
