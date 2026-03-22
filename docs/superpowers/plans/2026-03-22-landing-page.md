# colmo.tech Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a bilingual static landing page for Colmo, hosted on GitHub Pages at colmo.tech.

**Architecture:** Single-page HTML/CSS site with inline JS for language switching. Stacked vertical layout with header, hero, two service sections, contact, and footer. Separate legal mentions page. No build tooling.

**Tech Stack:** HTML5, CSS3, vanilla JavaScript, Bunny Fonts (Inter), GitHub Pages

**Spec:** `docs/superpowers/specs/2026-03-22-landing-page-design.md`

---

### Task 1: Create stylesheet (style.css)

**Files:**
- Create: `style.css`

- [ ] **Step 1: Create style.css with CSS variables, reset, and base styles**

```css
@import url(https://fonts.bunny.net/css?family=inter:400,600);

:root {
  --color-primary: #4A90C4;
  --color-dark: #3D3D3D;
  --color-bg-light: #F5F7FA;
  --color-white: #FFFFFF;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Inter", sans-serif;
  font-weight: 400;
  color: var(--color-dark);
  background-color: var(--color-white);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  line-height: 1.6;
}

h1, h2, h3 {
  font-weight: 600;
  line-height: 1.3;
}

a {
  color: var(--color-primary);
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

img {
  max-width: 100%;
  height: auto;
}
```

- [ ] **Step 2: Add layout and header styles**

Append to `style.css`:

```css
/* Layout */
.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 24px;
}

/* Header */
.site-header {
  border-bottom: 1px solid #e0e0e0;
  padding: 16px 0;
}

.site-header .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-link {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  color: var(--color-dark);
}

.logo-link:hover {
  text-decoration: none;
}

.logo-img {
  height: 36px;
  width: auto;
}

.logo-text {
  font-size: 1.25rem;
  font-weight: 600;
  letter-spacing: 0.05em;
}

.lang-toggle {
  display: flex;
  gap: 8px;
  font-size: 0.875rem;
}

.lang-btn {
  background: none;
  border: none;
  cursor: pointer;
  font-family: "Inter", sans-serif;
  font-size: 0.875rem;
  color: var(--color-dark);
  padding: 4px 8px;
  border-radius: 3px;
}

.lang-btn:hover {
  background-color: var(--color-bg-light);
}

.lang-btn.active {
  font-weight: 600;
  border-bottom: 2px solid var(--color-primary);
}
```

- [ ] **Step 3: Add hero, services, contact, and footer styles**

Append to `style.css`:

```css
/* Hero */
.hero {
  text-align: center;
  padding: 80px 24px;
  background-color: var(--color-bg-light);
}

.hero h1 {
  font-size: 2rem;
  color: var(--color-dark);
  margin-bottom: 12px;
}

.hero p {
  font-size: 1.125rem;
  color: #666;
}

/* Services */
.services {
  padding: 48px 0;
  border-bottom: 1px solid #e0e0e0;
}

.services h2 {
  font-size: 1.375rem;
  color: var(--color-primary);
  margin-bottom: 20px;
}

.services ul {
  list-style: none;
  padding: 0;
}

.services li {
  padding: 8px 0 8px 20px;
  position: relative;
  line-height: 1.5;
}

.services li::before {
  content: "—";
  position: absolute;
  left: 0;
  color: var(--color-primary);
}

/* Contact */
.contact {
  padding: 48px 0;
  border-bottom: 1px solid #e0e0e0;
}

.contact h2 {
  font-size: 1.375rem;
  color: var(--color-primary);
  margin-bottom: 20px;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.contact-links a {
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

/* Footer */
.site-footer {
  padding: 24px 0;
  font-size: 0.875rem;
  color: #666;
}

.site-footer .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.site-footer a {
  color: #666;
}

.site-footer a:hover {
  color: var(--color-dark);
}

/* Responsive */
@media (max-width: 768px) {
  .hero {
    padding: 48px 24px;
  }

  .hero h1 {
    font-size: 1.5rem;
  }

  .site-footer .container {
    flex-direction: column;
    gap: 8px;
    text-align: center;
  }
}
```

- [ ] **Step 4: Verify by opening style.css and checking it parses**

Run: `cat style.css | head -5`
Expected: the `@import` line and `:root` block

- [ ] **Step 5: Commit**

```bash
git add style.css
git commit -m "feat: add stylesheet with layout, typography, and responsive styles"
```

---

### Task 2: Create main page (index.html)

**Files:**
- Create: `index.html`
- Depends on: Task 1 (style.css must exist)

- [ ] **Step 1: Create index.html with head and header**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" data-fr="Colmo — Conseil en stratégie de données et ingénierie, spécialiste de la commande publique" data-en="Colmo — Data strategy consulting and engineering, public procurement specialist">
  <title data-fr="Colmo — Stratégie, ingénierie et analyse de données" data-en="Colmo — Data strategy, engineering and analytics">Colmo — Stratégie, ingénierie et analyse de données</title>
  <link rel="icon" href="assets/logoCM.png">
  <link rel="apple-touch-icon" href="assets/logoCM.png">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header class="site-header">
    <div class="container">
      <a href="/" class="logo-link">
        <img src="assets/logoCM.png" alt="Colmo" class="logo-img">
        <span class="logo-text">COLMO</span>
      </a>
      <nav class="lang-toggle" aria-label="Language selection">
        <button class="lang-btn active" onclick="setLang('fr')" aria-label="Français">FR</button>
        <span aria-hidden="true">|</span>
        <button class="lang-btn" onclick="setLang('en')" aria-label="English">EN</button>
      </nav>
    </div>
  </header>
```

- [ ] **Step 2: Add hero and services sections**

Continue `index.html` after the header:

```html
  <main>
    <section class="hero">
      <div class="container">
        <h1 data-fr="Stratégie, ingénierie et analyse de données" data-en="Data strategy, engineering and analytics">Stratégie, ingénierie et analyse de données</h1>
        <p data-fr="Spécialiste de la commande publique" data-en="Public procurement specialist">Spécialiste de la commande publique</p>
      </div>
    </section>

    <section class="services">
      <div class="container">
        <h2 data-fr="Conseil et développement" data-en="Consulting and development">Conseil et développement</h2>
        <ul>
          <li data-fr="Conseil et accompagnement dans votre stratégie Open Data" data-en="Open Data strategy consulting and support">Conseil et accompagnement dans votre stratégie Open Data</li>
          <li data-fr="Cartographie et valorisation de vos données" data-en="Data mapping and enhancement">Cartographie et valorisation de vos données</li>
          <li data-fr="Conception et développement de traitements de données et d'API" data-en="Data processing and API design and development">Conception et développement de traitements de données et d'API</li>
        </ul>
      </div>
    </section>

    <section class="services">
      <div class="container">
        <h2 data-fr="Données de la commande publique" data-en="Public procurement data">Données de la commande publique</h2>
        <ul>
          <li data-fr="Exploitation des données de la commande publique pour un objectif d'impact économique, sociale ou environnemental" data-en="Leveraging public procurement data for economic, social, or environmental impact">Exploitation des données de la commande publique pour un objectif d'impact économique, sociale ou environnemental</li>
          <li data-fr="Agrégation de données" data-en="Data aggregation">Agrégation de données</li>
          <li data-fr="Conception et développement de tableaux de bord et d'alertes sur mesure" data-en="Custom dashboard and alert design and development">Conception et développement de tableaux de bord et d'alertes sur mesure</li>
        </ul>
      </div>
    </section>
```

- [ ] **Step 3: Add contact section, footer, and closing tags**

Continue `index.html`:

```html
    <section class="contact">
      <div class="container">
        <h2 data-fr="Contact" data-en="Contact">Contact</h2>
        <div class="contact-links">
          <a href="mailto:colin@colmo.tech">colin@colmo.tech</a>
          <a href="https://www.linkedin.com/in/colinmaudry/" target="_blank" rel="noopener" aria-label="LinkedIn — Colin Maudry">LinkedIn</a>
        </div>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container">
      <span>© 2026 SAS Colmo</span>
      <a href="mentions-legales.html" data-fr="Mentions légales" data-en="Legal notice">Mentions légales</a>
    </div>
  </footer>
```

- [ ] **Step 4: Add inline bilingual JavaScript and close the document**

Continue `index.html`:

```html
  <script>
    function detectLang() {
      var saved = localStorage.getItem('lang');
      if (saved) return saved;
      var langs = navigator.languages || [navigator.language];
      for (var i = 0; i < langs.length; i++) {
        if (langs[i].toLowerCase().startsWith('fr')) return 'fr';
      }
      return 'en';
    }

    function setLang(lang) {
      document.documentElement.lang = lang;
      localStorage.setItem('lang', lang);

      document.querySelectorAll('[data-fr]').forEach(function(el) {
        var text = el.getAttribute('data-' + lang);
        if (el.tagName === 'META') {
          el.setAttribute('content', text);
        } else if (el.tagName === 'TITLE') {
          document.title = text;
        } else {
          el.textContent = text;
        }
      });

      document.querySelectorAll('.lang-btn').forEach(function(btn) {
        btn.classList.toggle('active', btn.textContent.toLowerCase() === lang);
      });
    }

    setLang(detectLang());
  </script>
</body>
</html>
```

- [ ] **Step 5: Open in browser and verify**

Run: `python3 -m http.server 8000 &` from project root, open `http://localhost:8000` in browser. Verify:
- Logo and "COLMO" text appear in header
- FR/EN toggle works (click EN, text switches; click FR, switches back)
- All 6 sections render (header, hero, 2 services, contact, footer)
- Page is responsive (resize browser window)

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: add bilingual landing page with language detection and toggle"
```

---

### Task 3: Create legal mentions page (mentions-legales.html)

**Files:**
- Create: `mentions-legales.html`
- Depends on: Task 1 (style.css must exist)

- [ ] **Step 1: Create mentions-legales.html**

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Mentions légales — SAS Colmo">
  <title>Mentions légales — Colmo</title>
  <link rel="icon" href="assets/logoCM.png">
  <link rel="apple-touch-icon" href="assets/logoCM.png">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header class="site-header">
    <div class="container">
      <a href="/" class="logo-link">
        <img src="assets/logoCM.png" alt="Colmo" class="logo-img">
        <span class="logo-text">COLMO</span>
      </a>
    </div>
  </header>

  <main>
    <section class="services">
      <div class="container">
        <h2>Mentions légales</h2>
        <p>Site Web développé et édité par SAS Colmo, 989 393 350 RCS Rennes au capital de 3 000 euros.</p>
        <p style="margin-top: 12px;">Siège social : 1 carrefour Jouaust, 35000 Rennes</p>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container">
      <span>© 2026 SAS Colmo</span>
      <a href="/">Accueil</a>
    </div>
  </footer>
</body>
</html>
```

- [ ] **Step 2: Verify links work**

Open `http://localhost:8000`, click "Mentions légales" in footer → legal page loads.
On legal page, click "Accueil" in footer → returns to index.
Verify: no language toggle in header on legal page.

- [ ] **Step 3: Commit**

```bash
git add mentions-legales.html
git commit -m "feat: add legal mentions page"
```

---

### Task 4: Create CNAME and add .gitignore entry

**Files:**
- Create: `CNAME`
- Create or modify: `.gitignore`

- [ ] **Step 1: Create CNAME file**

```
colmo.tech
```

- [ ] **Step 2: Add .superpowers/ to .gitignore**

```
.superpowers/
```

- [ ] **Step 3: Commit**

```bash
git add CNAME .gitignore
git commit -m "feat: add CNAME for GitHub Pages and .gitignore"
```

---

### Task 5: Visual review and polish

**Files:**
- Modify: `style.css` (if adjustments needed)
- Modify: `index.html` (if adjustments needed)

- [ ] **Step 1: Open the site in a browser and review**

Run: `python3 -m http.server 8000` (if not already running)
Open `http://localhost:8000`

Check:
- Classic professional tone achieved
- Section spacing feels right
- Mobile view works (use browser devtools responsive mode)
- Language toggle works in both directions
- localStorage persists choice across page reload
- Footer link to mentions-legales works and back
- All French text matches CLAUDE.md exactly
- No console errors

- [ ] **Step 2: Fix any issues found**

Adjust CSS spacing, colors, or text as needed based on review.

- [ ] **Step 3: Commit any fixes**

```bash
git add -A
git commit -m "fix: polish styles after visual review"
```
