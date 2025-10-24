# Horizon Theme Design System

A practical, documented guide for visual consistency across your store and theme customizations.

## Brand Identity
- Aesthetic: Explorer/Sage — earthy, natural, grounded
- Tone: Direct, business-oriented, trustworthy (B2B focus)

## Color Palette Analysis (estimated from page context)
Primary and supporting colors tuned for clarity and commerce-first messaging.

- Primary: `#2c2c2c` (Charcoal Black) — used for text and navigation; professional and clear
- Accent: `#f5a623` (Warm Amber) — CTAs like “Shop now” and promotional highlights
- Background: `#ffffff` (Pure White) — clean backdrop for product listings and content
- Surface/Sections: `#f9f9f9` (Light Gray) — subtle contrast for testimonials/education/category blocks
- Text (default): `#2c2c2c`
- Text (muted): `#666666`
- Border/Subtle: `#eaeaea`

### CSS Variables
Use these as a single source of truth. Apply in your global stylesheet (e.g., `assets/base.css` or `assets/theme.css`).

```css
:root {
  --primary: #2c2c2c;          /* Charcoal Black */
  --accent:  #f5a623;          /* Warm Amber */
  --background: #ffffff;       /* Pure White */
  --surface: #f9f9f9;          /* Light Gray */

  --text: #2c2c2c;             /* Default text */
  --text-muted: #666666;       /* Secondary text */
  --border: #eaeaea;           /* Subtle borders/dividers */
}

html, body {
  background: var(--background);
  color: var(--text);
}
```

### Usage Guidelines
- Background vs Surface: Use `--background` for page body and `--surface` for cards/sections.
- Primary: Brand-heavy areas (header, CTAs, badges). Combine with white text for contrast.
- Accent: Secondary CTAs, links hovers, highlights. Use sparingly to maintain impact.
- Borders: Use `--border` for subtle dividers and card outlines.

### Accessibility Notes
- Charcoal `#2c2c2c` on white `#ffffff` exceeds AA for body text and navigation.
- Ensure Warm Amber `#f5a623` has sufficient contrast for text on buttons; default to white text and test hover states.
- Verify any additional grays meet WCAG AA (4.5:1 for body, 3:1 for large text/UI).

---

## Typography System
Modern sans-serif (Shopify default/Horizon’s clean type) with a clear, bold hierarchy.

### Recommended Font Stacks
- System-first (no external requests):
  ```css
  :root {
    --font-sans: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  }
  ```
- Or hosted (example): Inter or Source Sans 3 via Shopify assets or a performance-optimized provider.

### Scale and Weights
- Base: 16px
- Headings: h1 36–44px, h2 28–32px, h3 22–24px; bold for products and section titles
- Body: 16–18px (400–500); small text 14px

```css
body { font-family: var(--font-sans); line-height: 1.55; }
.h1, h1 { font-size: clamp(2.25rem, 2.5vw + 1.5rem, 2.75rem); font-weight: 800; }
.h2, h2 { font-size: clamp(1.75rem, 1.8vw + 1rem, 2rem); font-weight: 800; }
.h3, h3 { font-size: 1.375rem; font-weight: 700; }
.muted { color: var(--text-muted); }
```

---

## Layout Patterns
- Hero Section: prominent welcome with tagline “Outstanding service | Exclusive pricing | Industry expertise”, clear primary CTA
- Product Grid: consistent product tiles and pricing (e.g., $19.99 USD) for scale and scanning
- Category Blocks: “Shop our top categories” and “New arrivals” as horizontal scrollers or responsive grids
- Testimonials & Education: repeated modular sections for social proof and tips/content
- Navigation: minimal top nav with “Log in” and “Cart”; footer with standard Shopify links
- Mobile Optimization: responsive by default; stacked sections and touch-friendly buttons

```css
.container { max-width: 1100px; margin-inline: auto; padding-inline: 16px; }
.grid { display: grid; gap: 16px; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); }
.sticky-nav { position: sticky; top: 0; z-index: 50; background: var(--primary); color: #fff; }
.section { background: var(--surface); border: 1px solid var(--border); border-radius: 10px; padding: 16px; }
```

---

## Components

### Buttons
```css
.btn { display: inline-block; padding: 10px 16px; border-radius: 8px; text-decoration: none; font-weight: 600; }
.btn-primary { background: var(--primary); color: #fff; }
.btn-primary:hover { filter: brightness(1.05); }
.btn-accent { background: var(--accent); color: #fff; }
.btn-ghost { background: transparent; border: 1px solid var(--border); color: var(--text); }
```

### Links
```css
a { color: var(--accent); text-decoration: none; }
a:hover { text-decoration: underline; }
```

### Cards
```css
.card { background: #fff; border: 1px solid var(--border); border-radius: 10px; box-shadow: 0 6px 18px rgba(0,0,0,0.06); overflow: hidden; }
.card__body { padding: 12px 14px; }
.card__title { margin: 0 0 8px; font-weight: 700; }
.card__text { margin: 0; color: var(--text); }
```

---

## Spacing & Elevation
- Spacing scale (8px rhythm): 4, 8, 12, 16, 24, 32, 48
- Elevation:
  - Level 0: no shadow (flat)
  - Level 1: `0 2px 6px rgba(0,0,0,.04)` (inputs, chips)
  - Level 2: `0 6px 18px rgba(0,0,0,.08)` (cards)

---

## Motion
- Durations: 120–200ms for UI, 250–350ms for modals/large elements
- Easing: `cubic-bezier(.2,.7,.2,1)`; keep motion subtle and purposeful

---

## Applying in Shopify
- Add the CSS variables to your main stylesheet (e.g., `assets/base.css`), or create a dedicated `assets/design-tokens.css` and import it.
- Map settings in `config/settings_schema.json` to expose color pickers (optional), defaulting to the values above.
- Use section blocks to apply `.section`, `.grid`, and button classes for consistent layouts.

### Example settings_schema (optional snippet)
```json
[
  {
    "name": "Theme colors",
    "settings": [
      { "type": "color", "id": "color_primary", "label": "Primary", "default": "#2c2c2c" },
      { "type": "color", "id": "color_accent", "label": "Accent", "default": "#f5a623" },
      { "type": "color", "id": "color_background", "label": "Background", "default": "#ffffff" },
      { "type": "color", "id": "color_surface", "label": "Surface", "default": "#f9f9f9" }
    ]
  }
]
```

---

## Quick Start (optional)
If you prefer the shell one-liner to create this file:

```bash
mkdir -p docs
cat > docs/style_guide.md << 'EOF'
# Horizon Theme Design System

## Brand Identity
- Aesthetic: Explorer/Sage — earthy, natural, grounded
- Tone: Direct, business-oriented, trustworthy (B2B focus)

## Color Palette Analysis
- Primary: #2c2c2c (Charcoal Black)
- Accent: #f5a623 (Warm Amber)
- Background: #ffffff (Pure White)
- Surface: #f9f9f9 (Light Gray)

## Color System (CSS)
```css
:root {
  --primary: #2c2c2c;
  --accent: #f5a623;
  --background: #ffffff;
  --surface: #f9f9f9;
}
```
EOF
```
