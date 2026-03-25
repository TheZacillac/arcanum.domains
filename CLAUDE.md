# CLAUDE.md - Arcanum Domains

arcanum.domains is the marketing and documentation website for the Arcanum Suite. Built with Astro, it's a static site deployed to GitHub Pages.

---

## Structure

```
arcanum.domains/
├── astro.config.mjs         # Site URL: https://arcanum.domains
├── package.json             # Astro 5.7.10 (sole dependency)
├── tsconfig.json            # TypeScript strict mode
├── .github/workflows/
│   └── deploy.yml           # GitHub Pages auto-deploy on push to main
├── public/
│   └── CNAME                # Custom domain: arcanum.domains
└── src/
    ├── pages/
    │   └── index.astro      # Homepage (assembles all components)
    ├── layouts/
    │   └── Layout.astro     # Root HTML, intersection observer, smooth scrolling
    ├── components/
    │   ├── Hero.astro       # Landing: animated SVG sigil, CTAs, synthwave grid
    │   ├── Projects.astro   # Six project cards with features and links
    │   ├── Architecture.astro  # Three-layer dependency diagram (SVG)
    │   ├── TechStack.astro  # Technology highlights grid + badge cloud
    │   └── Footer.astro     # Navigation and branding
    └── styles/
        └── global.css       # Design tokens, fonts, animations, CRT effects
```

---

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Dev server (localhost:4321, hot reload)
npm run build     # Production build to dist/
npm run preview   # Preview built site
```

---

## Design System

### Fonts (Google Fonts CDN)
- **Display:** Cinzel Decorative (decorative headings)
- **Heading:** Cinzel (structured headings)
- **Body:** Spectral (readable serif)
- **Mono:** VT323 (retro monospace)

### Color Palette (CSS custom properties in global.css)

**Backgrounds:** `--void` (#080010), `--abyss` (#0e0520), `--deep` (#160a30), `--surface` (#1e1040)

**Neon accents:** `--gold` (#ffd700), `--neon-pink` (#ff2d95), `--neon-cyan` (#00e5ff), `--neon-purple` (#c77dff)

**Per-tool colors:** `--seer` (cyan), `--tome` (gold), `--tower` (purple), `--scrolls` (neon green), `--familiar` (pink), `--oracle` (amber)

### Visual Effects
- **CRT scanlines** — repeating 2px horizontal lines over entire page
- **Starfield** — 15 radial gradients with twinkle animation
- **Scroll-reveal** — intersection observer adds `.visible` class, CSS transitions handle fade + slide
- **Staggered delays** — `.reveal-delay-1` through `.reveal-delay-6`
- **Neon glows** — box-shadow and text-shadow with accent colors

---

## Page Sections

1. **Hero** — synthwave perspective grid, animated SVG sigil (multi-stage stroke draw + slow rotation), chrome gradient title, two CTAs
2. **Projects** — data-driven cards for Seer, Tome, Tower, Scrolls, Familiar, Oracle with SVG icons, feature badges, interface lists, tech stack badges, repo links
3. **Architecture** — SVG connection diagram showing three layers (Core → Integration → Interface)
4. **TechStack** — 6 technology categories (Rust, Python, MCP, Tokio, LangGraph, SQLite) + badge cloud
5. **Footer** — mini sigil, navigation links, branding

---

## Deployment

GitHub Actions workflow (`.github/workflows/deploy.yml`):
- **Trigger:** push to `main` or manual dispatch
- **Build:** Node 22, `npm ci`, `npx astro build`
- **Deploy:** GitHub Pages via `actions/deploy-pages@v4`
- **Domain:** `arcanum.domains` (CNAME in `public/`)
- **Concurrency:** prevents simultaneous deploys

---

## Key Technical Notes

- **Zero client JS by default** — Astro ships pure HTML/CSS; only the intersection observer and smooth scroll are client-side
- **Component scoping** — each component has `<style>` blocks scoped to that component
- **Data-driven cards** — project data defined as arrays in component frontmatter
- **Responsive** — `clamp()` for typography, CSS Grid with `auto-fit`, mobile breakpoints at 640px/720px
- **No client frameworks** — no React/Vue/Svelte; pure Astro components
- **Animations** — all CSS-based (hardware-accelerated transforms, keyframes)

---

## Conventions

- Components are self-contained with colocated styles
- Colors use CSS custom properties from `global.css` — don't hardcode
- New sections should include `.reveal` class for scroll animation
- Project data (names, descriptions, features, links) is maintained in `Projects.astro` frontmatter
- GitHub repo links follow `https://github.com/TheZacillac/{project}` pattern
