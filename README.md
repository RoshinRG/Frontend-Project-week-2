# Frontend-Project-week-2
Responsive Web Layout
# DigitalCreative — Responsive Web Layout

> **DecodeLabs · Project 2 — Mobile-First Responsive Design**

A production-ready, fully responsive agency website built from the ground up with a mobile-first philosophy, zero layout-breaking bugs from 320 px to 1440 px+.

---

## 📁 File Structure

```
digitalcreative/
├── index.html   ← Semantic HTML5, Popover API nav, ARIA landmarks
└── style.css    ← Mobile-first CSS, 4 breakpoints, fluid everything
```

---

## ✅ Requirements Checklist

| # | Requirement | Status |
|---|-------------|--------|
| 1 | `<meta name="viewport" content="width=device-width, initial-scale=1">` — **no** `user-scalable=no` | ✅ |
| 2 | Mobile-first CSS — base styles for 320 px+, enhanced with `min-width` queries | ✅ |
| 3 | **Three breakpoints** — base, 600 px, 1024 px (+ bonus 1440 px) | ✅ |
| 4 | Fluid CSS Grid — `repeat(auto-fit, minmax(min(100%, 250px), 1fr))` on all card grids | ✅ |
| 5 | Fluid typography — `clamp()` on every heading (`h1`–`h3`) and body copy | ✅ |
| 6 | Responsive nav — HTML **Popover API** slide-in panel on mobile, horizontal bar on desktop | ✅ |
| 7 | Touch targets — all `<button>` and `<a>` elements: `min-height: 44px; min-width: 44px` | ✅ |
| 8 | Accessibility — user zoom up to 500 %, WCAG 2.1 AA colour contrast, focus rings, skip link | ✅ |
| 9 | Images — `max-width: 100%; height: auto` on every `<img>` | ✅ |

---

## 🎯 Breakpoints

All breakpoints are based on **content breakage**, not device names:

| Breakpoint | Width | Purpose |
|-----------|-------|---------|
| **Mobile core** | Base CSS (no media query) | Single-column stacks, hamburger nav, large touch targets |
| **Tablet** | `@media (min-width: 600px)` | Desktop nav appears, hero goes 2-column, grids expand to 2 columns |
| **Desktop** | `@media (min-width: 1024px)` | Max-width container, services → 3-col, team → 4-col, footer → 4-col |
| **Wide** | `@media (min-width: 1440px)` | Portfolio → 4-col, expanded spacing, max-width grows to 1400 px |

---

## 🧩 Key Techniques

### Fluid Typography (clamp)
```css
h1 { font-size: clamp(2rem,   7vw, 4rem);    }
h2 { font-size: clamp(1.5rem, 5vw, 2.75rem); }
h3 { font-size: clamp(1.1rem, 3vw, 1.5rem);  }
```
Headings scale smoothly between mobile and desktop — no breakpoint jumps.

### Fluid CSS Grid
```css
.services__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 250px), 1fr));
  gap: var(--sp-lg);
}
```
`min(100%, 250px)` prevents a single card from overflowing on very narrow viewports.

### HTML Popover API — Zero JS for Open/Close
```html
<button popovertarget="mobile-nav">☰</button>
<nav id="mobile-nav" popover="auto">…</nav>
```
The browser handles toggling natively. CSS `@starting-style` provides a smooth slide-in animation.

### Dark Mode — Dual Strategy
- **Auto**: `@media (prefers-color-scheme: dark)` for system preference
- **Manual**: `[data-theme="dark"]` attribute toggled by the 🌙/☀️ button, persisted in `localStorage`

### Scroll Reveal (Progressive Enhancement)
```js
const io = new IntersectionObserver(…);
document.querySelectorAll('.reveal').forEach(el => io.observe(el));
```
Falls back gracefully: without JS, all elements are visible. `prefers-reduced-motion` disables transitions entirely.

---

## ♿ Accessibility

- **Skip link** — `Skip to main content` link as first focusable element
- **ARIA landmarks** — `role="banner"`, `role="contentinfo"`, `aria-label` on all `<nav>` elements
- **Focus rings** — `:focus-visible` with 3 px offset ring on all interactive elements
- **`aria-pressed`** on theme toggle, **`aria-expanded`** on hamburger (updated via Popover toggle event)
- **Alt text** — descriptive on all content images
- **No `user-scalable=no`** — user zoom up to 500 % is always respected
- **Reduced motion** — all transitions/animations cancelled via `prefers-reduced-motion: reduce`
- **Colour contrast** — primary blue `#2563eb` on white passes WCAG AA at all text sizes

---

## 🖥️ How to Test

```bash
# Option A: VS Code Live Server
# Right-click index.html → "Open with Live Server"

# Option B: Node http-server
npx http-server . -p 3000
# Open http://localhost:3000
```

**Resize the browser from 320 px to 1440 px** — check:
- [ ] Navigation collapses to hamburger below 600 px
- [ ] No horizontal scroll at any width
- [ ] Typography scales smoothly without jumping
- [ ] All card grids reflow gracefully
- [ ] Dark mode toggle works and persists on refresh
- [ ] Tab navigation hits every interactive element

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| Markup | Semantic HTML5, ARIA, HTML Popover API |
| Styling | Vanilla CSS — Custom Properties, Grid, Flexbox, `clamp()` |
| JS | ~25 lines — theme toggle + IntersectionObserver reveal |
| Images | Unsplash (lazy-loaded, explicit `width`/`height`) |
| Fonts | System font stack — zero network requests |
| Build | None — single HTML + CSS, no bundler required |

---

## 📐 Design Decisions

1. **`min(100%, Npx)` in `minmax()`** — prevents grid blowout on 320 px screens where the minimum would exceed the viewport.
2. **`color-mix()` for glassmorphism header** — instead of a fixed rgba, the header tint inherits from `--color-bg`, so it works in both light and dark mode automatically.
3. **CSS Custom Properties for theming** — a single `:root` → `[data-theme="dark"]` swap changes the entire palette with zero specificity wars.
4. **`@starting-style` for popover animation** — native CSS entry animation for the mobile nav panel, no JS required.
5. **`aspect-ratio` on images** — eliminates layout shift (CLS) since the browser reserves space before the image loads.

---

*Built at DecodeLabs · June 2025*
