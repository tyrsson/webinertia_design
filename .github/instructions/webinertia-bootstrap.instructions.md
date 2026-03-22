---
description: "Use when creating, editing, or extending any page or stylesheet in the webinertia_bootstrap project. Covers design tokens, component patterns, Bootstrap 5.3 conventions, and CSS class naming rules for the Webinertia dark design system."
applyTo: "webinertia_bootstrap/**"
---

# Webinertia Bootstrap — Design System Reference

## Project Overview

A Bootstrap 5.3 implementation of the Webinertia dark design system. The aesthetic is **dark glassmorphism** with a purple / cyan / magenta palette, Space Grotesk typography, and a fixed 80px side navigation rail. Pico CSS is not used — Bootstrap 5.3 provides the grid and JS components; all visual styling is custom.

---

## Framework & CDN

Always use these exact CDN links. Do not upgrade without explicit instruction.

```html
<!-- Head -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css">

<!-- Before </body> -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

---

## Typography

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700;800&display=swap" rel="stylesheet">
```

- **Primary font:** Space Grotesk (400, 600, 700, 800)
- **Fallback stack:** `Inter, system-ui, sans-serif`
- All text inherits `font-family` from body; never override with Bootstrap utility classes.

---

## CSS Custom Properties (Design Tokens)

All tokens are defined in `assets/css/style.css` `:root`. Always reference tokens rather than hard-coding hex values.

```css
/* Colours */
--primary-purple:  #8B5CF6
--primary-cyan:    #06B6D4
--primary-magenta: #EC4899
--accent-yellow:   #FBBF24

/* Backgrounds */
--dark-bg:         #0F0F1E   /* page sections */
--darker-bg:       #070710   /* body / deepest bg */
--card-bg:         #1A1A2E   /* cards, modals, nav */

/* Text */
--text-primary:    #FFFFFF
--text-secondary:  #A0AEC0

/* Gradients */
--gradient-1:  linear-gradient(135deg, #8B5CF6 0%, #EC4899 100%)  /* purple → magenta */
--gradient-2:  linear-gradient(135deg, #06B6D4 0%, #8B5CF6 100%)  /* cyan → purple   */
--gradient-3:  linear-gradient(135deg, #EC4899 0%, #FBBF24 100%)  /* magenta → yellow */
```

---

## Page Shell Template

Every page must follow this exact structure. Do not add a Bootstrap navbar — navigation is the side rail only.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Name | Webinertia</title>
    <meta name="description" content="…">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>

    <nav class="side-nav">
        <div class="side-nav-logo">Webinertia</div>
        <ul class="side-nav-items">
            <li class="side-nav-item"><a href="index.html"      data-label="Home">🏠</a></li>
            <li class="side-nav-item"><a href="services.html"   data-label="Services">⚡</a></li>
            <li class="side-nav-item"><a href="about.html"      data-label="About">💡</a></li>
            <li class="side-nav-item"><a href="portfolio.html"  data-label="Portfolio">🎨</a></li>
            <li class="side-nav-item"><a href="contact.html"    data-label="Contact">📧</a></li>
            <li class="side-nav-item"><a href="components.html" data-label="Components">🧩</a></li>
        </ul>
    </nav>

    <main class="main-content">
        <!-- page content here -->
    </main>

    <footer>
        <div class="footer-content">
            <p>© 2026 <span class="footer-brand">Webinertia</span> <span class="accent-dot"></span> Shaping Digital Futures</p>
        </div>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

## Layout Rules

| Rule | Detail |
|---|---|
| Side nav width | Fixed `80px` left — **never** modify this value |
| Main content offset | `.main-content { margin-left: 80px }` |
| Footer offset | `footer { margin-left: 80px }` |
| Responsive breakpoint | At `≤ 1024px` the side nav collapses to `width: 0` and both offsets drop to `0` |
| Max content width | `1400px` centred with `margin: 0 auto` inside grid containers |
| Section padding | `padding: 6rem 4rem` for standard sections; `padding: 8rem 4rem` for CTA sections |

Do **not** use Bootstrap's `.container`, `.container-fluid`, or `.row`/`.col-*` grid inside `.main-content` — the custom CSS grids (`bento-grid`, `portfolio-grid`, `form-grid`) are used instead.

---

## Component Classes

### Buttons

| Class | Gradient / Style | Use |
|---|---|---|
| `.btn-primary` / `a.btn-primary` | `--gradient-1`, pill `border-radius: 50px` | Full-size primary CTA |
| `.btn-outline` / `a.btn-outline` | Transparent, `2px solid --primary-purple`, pill | Full-size secondary CTA |
| `.btn-sm-primary` | `--gradient-1`, pill | Small primary — modal/toast footers |
| `.btn-sm-cyan` | `--gradient-2`, pill | Small cyan action |
| `.btn-sm-success` | green→cyan gradient, pill | Small success action |
| `.btn-sm-danger` | red→magenta gradient, pill | Small destructive action |
| `.btn-ghost` | Transparent, `1px solid rgba(purple, 0.3)`, pill | Cancel / dismiss |

**Important:** Never use Bootstrap's built-in `.btn`, `.btn-primary`, `.btn-secondary` etc. — they are overridden by the custom button classes above.

### Cards / Bento Grid

```html
<div class="bento-grid">
    <div class="bento-card">…</div>           <!-- standard card -->
    <div class="bento-card large">…</div>     <!-- spans 2 columns -->
</div>
```

- Glassmorphic: `backdrop-filter: blur(20px)`, dark bg, `1px solid rgba(purple, 0.2)` border
- Hover: lifts `translateY(-10px)`, glows purple, top accent bar slides in via `::before`
- `.bento-grid` uses `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))`

### Section Headers

```html
<div class="section-header">
    <h2 class="section-title"><span class="gradient-text">Title Here</span></h2>
    <div class="divider"></div>
    <p class="section-subtitle">Supporting copy</p>
</div>
```

- `.gradient-text` applies `--gradient-2` as a clipped background — always wrap gradient headings in a `<span>` inside `.section-title`
- `.divider` — 2px high, `--gradient-1`, max-width `100px`, centred

### Diagonal Section

```html
<section class="diagonal-section">…</section>
```

Uses `clip-path: polygon(0 5%, 100% 0, 100% 95%, 0 100%)` on `--card-bg` background. Add `margin: 4rem 0`.

### Tech Pills

```html
<div class="tech-stack">
    <div class="tech-pill">Laravel</div>
</div>
```

Glassmorphic, `border-radius: 50px`. Hover applies `--gradient-2` background.

### Hero Split (index page only)

```html
<section class="hero-split">
    <div class="hero-left">…</div>   <!-- title, subtitle, CTA buttons -->
    <div class="hero-right">…</div>  <!-- floating cards visual -->
</section>
```

`grid-template-columns: 1fr 1fr`, `min-height: 100vh`. `.hero-right` hidden on mobile.

---

## Modal Variants

Apply the modifier class to the **`.modal`** element (not `.modal-dialog`).

| Class | Accent | Glow colour |
|---|---|---|
| *(none)* | `--gradient-1` purple→magenta | purple |
| `.modal-cyan` | `--gradient-2` cyan→purple | cyan |
| `.modal-magenta` | `--gradient-3` magenta→yellow | magenta |
| `.modal-danger` | red→magenta | red |
| `.modal-success` | green→cyan | green |

Footer buttons: use `.btn-ghost` for cancel/dismiss, `.btn-sm-*` for confirm actions.  
Icon-centred modals: add `.modal-icon-header` to `.modal-header` and remove `border-bottom`, then place a `.modal-icon-circle[.cyan|.danger|.success]` div inside.

---

## Toast Variants

Apply variant class directly to the **`.toast`** element.

| Class | Accent bar | Use |
|---|---|---|
| *(none)* | `--gradient-1` | General notifications |
| `.toast-cyan` | `--gradient-2` | Informational / new features |
| `.toast-success` | green→cyan | Confirmed actions |
| `.toast-danger` | red→magenta | Errors |
| `.toast-warning` | yellow→magenta | Cautions |
| `.toast-simple` | matches another variant | Header-less compact toast |

Always place toasts inside `.toast-container.position-fixed.bottom-0.end-0.p-4` with `z-index: 1100`.

Initialise / re-show with:
```js
function showToast(id) {
    const el = document.getElementById(id);
    const existing = bootstrap.Toast.getInstance(el);
    if (existing) existing.dispose();
    new bootstrap.Toast(el).show();
}
```

---

## Tooltip Variants

Tooltips must be **manually initialised** on DOMContentLoaded:
```js
document.querySelectorAll('[data-bs-toggle="tooltip"]').forEach(el => {
    new bootstrap.Tooltip(el);
});
```

Use `data-bs-custom-class` to apply accent variants:

| Custom class | Border / arrow colour |
|---|---|
| *(none)* | purple |
| `tooltip-cyan` | cyan |
| `tooltip-success` | green |
| `tooltip-danger` | red |

---

## Accordion Variants

- **Standard** (one panel open): bind `data-bs-parent="#accordionId"` on each `.accordion-collapse`
- **Flush / multi-open**: add `.accordion-flush` to `.accordion`; omit `data-bs-parent`

The `.accordion` element uses CSS custom properties for theming — do not override individual `.accordion-button` background with inline styles.

---

## Colour Usage Guidelines

| Use | Token |
|---|---|
| Page/body background | `var(--darker-bg)` |
| Section alternate bg | `var(--dark-bg)` |
| Cards, modals, nav | `var(--card-bg)` |
| Primary heading text | `var(--text-primary)` |
| Body / secondary text | `var(--text-secondary)` |
| Links, tech stack text | `var(--primary-cyan)` |
| Primary accent / buttons | `var(--gradient-1)` |
| Info / discovery | `var(--gradient-2)` |

Never use Bootstrap colour utilities (`bg-primary`, `text-success`, etc.) — they conflict with the dark palette.

---

## Mobile Navigation

At `≤1024px` the desktop side rail collapses to `width: 0`. A hamburger button and offcanvas drawer replace it.

**Hamburger button** — add immediately after the closing `</nav>` of `.side-nav`, before `<!-- Main Content -->`:

```html
<!-- Mobile Navigation Toggle (visible ≤1024px) -->
<button class="mobile-nav-toggle"
        type="button"
        data-bs-toggle="offcanvas"
        data-bs-target="#mobileNav"
        aria-controls="mobileNav"
        aria-label="Open navigation">
    <span></span>
</button>
```

**Offcanvas drawer** — add after `</footer>` and before the Bootstrap JS `<script>` tag:

```html
<!-- Mobile Navigation Offcanvas Drawer -->
<div class="offcanvas offcanvas-start"
     tabindex="-1"
     id="mobileNav"
     aria-labelledby="mobileNavLabel">
    <div class="offcanvas-header">
        <span class="offcanvas-title" id="mobileNavLabel">Webinertia</span>
        <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
    </div>
    <div class="offcanvas-body">
        <a href="index.html"      class="mobile-nav-link" data-bs-dismiss="offcanvas"><span class="nav-icon">🏠</span><span class="nav-label">Home</span></a>
        <a href="services.html"   class="mobile-nav-link" data-bs-dismiss="offcanvas"><span class="nav-icon">⚡</span><span class="nav-label">Services</span></a>
        <a href="about.html"      class="mobile-nav-link" data-bs-dismiss="offcanvas"><span class="nav-icon">💡</span><span class="nav-label">About</span></a>
        <a href="portfolio.html"  class="mobile-nav-link" data-bs-dismiss="offcanvas"><span class="nav-icon">🎨</span><span class="nav-label">Portfolio</span></a>
        <a href="contact.html"    class="mobile-nav-link" data-bs-dismiss="offcanvas"><span class="nav-icon">📧</span><span class="nav-label">Contact</span></a>
        <a href="components.html" class="mobile-nav-link" data-bs-dismiss="offcanvas"><span class="nav-icon">🧩</span><span class="nav-label">Components</span></a>
        <div class="mobile-nav-divider"></div>
        <div class="mobile-nav-cta">
            <a href="contact.html" class="btn-primary" data-bs-dismiss="offcanvas">Start a Project</a>
        </div>
    </div>
</div>
```

CSS classes: `.mobile-nav-toggle`, `#mobileNav.offcanvas`, `.mobile-nav-link`, `.mobile-nav-divider`, `.mobile-nav-cta` — all defined in `style.css`. Do not add inline styles to these elements.

---

## CSS File Notes

- Single stylesheet: `assets/css/style.css`
- Structure order: tokens → base reset → side-nav → main-content → hero → sections → buttons → bento cards → portfolio grid → contact form → footer → responsive → tech pills → accents/divider → modals → toasts → tooltips → accordions
- When adding new component styles, append to the bottom in a clearly commented block
- Never modify `:root` token values without explicit instruction
