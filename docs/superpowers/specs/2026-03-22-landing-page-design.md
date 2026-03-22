# colmo.tech Landing Page — Design Spec

## Overview

A static HTML/CSS landing page for Colmo, a French data consultancy specializing in public contracting. The page establishes web presence with bilingual support (FR/EN), a classic professional tone, and a stacked vertical layout. Hosted on GitHub Pages at `colmo.tech`.

## Files

```
index.html            # Main landing page (bilingual)
mentions-legales.html # Legal mentions page (French only)
style.css             # Shared stylesheet
assets/logoCM.png     # Existing logo
CNAME                 # GitHub Pages custom domain
```

## HTML Head

- `<meta charset="UTF-8">`
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- `<meta name="description">` — bilingual, updated by JS along with other text
- `<html lang="fr">` — dynamically updated to match active language
- `<title>` — "Colmo — Stratégie, ingénierie et analyse de données" (FR) / "Colmo — Data strategy, engineering and analytics" (EN), updated by JS
- Bunny Fonts CSS import via `<link>` or `@import` in stylesheet
- Favicon and apple-touch-icon links

## Accessibility

- Use semantic HTML: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- Logo `<img>` has `alt="Colmo"`
- External links (LinkedIn) have `aria-label` and `target="_blank"` with `rel="noopener"`
- Color contrast: `#3D3D3D` on `#FFFFFF` is 10.3:1 (AAA); `#4A90C4` on `#FFFFFF` is 3.6:1 (AA for large text only — use blue for headings/accents, not body text)

## Page Structure: index.html

Single-page layout with stacked full-width sections, anchor navigation not needed for this minimal first version.

### 1. Header
- Left: logo (`assets/logoCM.png`) + "COLMO" text
- Right: language toggle — two text links "FR | EN", active language visually distinct (bold or underlined)
- Sticky or static (static for v1, simpler)

### 2. Hero Section
- Centered tagline:
  - FR: "Stratégie, ingénierie et analyse de données"
  - EN: "Data strategy, engineering and analytics"
- Subtitle:
  - FR: "Spécialiste de la commande publique"
  - EN: "Public procurement specialist"
- Light background, generous vertical padding

### 3. Services: Conseil et développement
- Section heading:
  - FR: "Conseil et développement"
  - EN: "Consulting and development"
- Three bullet points (translated):
  - Conseil et accompagnement dans votre stratégie Open Data / Open Data strategy consulting and support
  - Cartographie et valorisation de vos données / Data mapping and enhancement
  - Conception et développement de traitements de données et d'API / Data processing and API design and development

### 4. Services: Données de la commande publique
- Section heading:
  - FR: "Données de la commande publique"
  - EN: "Public procurement data"
- Three bullet points (translated):
  - Exploitation des données de la commande publique pour un objectif d'impact économique, sociale ou environnemental / Leveraging public procurement data for economic, social, or environmental impact
  - Agrégation de données / Data aggregation
  - Conception et développement de tableaux de bord et d'alertes sur mesure / Custom dashboard and alert design and development

### 5. Contact Section
- Email link: `colin@colmo.tech` (mailto link)
- LinkedIn link: `https://www.linkedin.com/in/colinmaudry/` (opens in new tab)
- No contact form

### 6. Footer
- Copyright: "© 2026 SAS Colmo"
- Link to `mentions-legales.html`

## Page Structure: mentions-legales.html

Minimal page with same header/footer as index.html but without the language toggle (content is French only, legal requirement). Contains:

- "Site Web développé et édité par SAS Colmo, 989 393 350 RCS Rennes au capital de 3 000 euros."
- "Siège social : 1 carrefour Jouaust, 35000 Rennes"

## Bilingual Implementation

CLAUDE.md specifies language detection via the `Accept-Language` HTTP header. Since GitHub Pages serves static files with no server-side logic, we use `navigator.languages` as the client-side equivalent — it returns the user's preferred languages in priority order, closely mirroring `Accept-Language`.

- All translatable text elements use data attributes: `data-fr="..." data-en="..."`
- Text content is set via JavaScript; the element's initial `textContent` can be empty or default to FR
- On page load:
  1. Check `localStorage` for saved preference
  2. If none, iterate `navigator.languages` — if any entry starts with `"fr"`, use FR; otherwise EN
  3. Apply language to all `[data-fr]` elements
- Language toggle:
  - Clicking FR/EN updates all text, saves choice to `localStorage`
  - Active language styled distinctly (e.g., bold)
- JavaScript is inline in `index.html` (small enough, avoids an extra file)

## Style (style.css)

### Font
```css
@import url(https://fonts.bunny.net/css?family=inter:400,600);
```
Font family: `"Inter", sans-serif`

### Colors
Approximated from the logo (`assets/logoCM.png`); refine if official brand colors are provided:
- Primary blue: `#4A90C4`
- Dark gray: `#3D3D3D`
- Light background: `#F5F7FA`
- White: `#FFFFFF`
- Text: `#3D3D3D` (dark gray, same as logo)

### Tone: Classic & Professional
- Subtle section borders or light background alternation to separate sections
- No animations or flashy effects
- Structured, formal layout
- Generous but not excessive whitespace

### Responsive
- Max content width ~900px, centered
- On mobile (<768px): sections stack naturally (already vertical), padding adjusts
- Logo + language toggle remain in header on mobile

## Favicon
- Use `assets/logoCM.png` directly as `apple-touch-icon`
- Reference via `<link rel="icon" href="assets/logoCM.png">`
- No separate favicon file needed for v1

## GitHub Pages
- `CNAME` file containing `colmo.tech`
- No build step — static files served directly
- User must configure DNS (A records or CNAME) on their domain registrar side

### Font Privacy
Bunny Fonts (`fonts.bunny.net`) is used intentionally as a GDPR-compliant alternative to Google Fonts — it does not track users. Do not replace with Google Fonts.

## Out of Scope (future phases)
- Detailed service descriptions
- Portfolio / case studies
- Contact form
- Blog
- Analytics
- Custom 404 page
