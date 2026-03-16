# Fiesta Artesanal Colibrí

Landing page for Fiesta Artesanal Colibrí - cultural artisan experiences for luxury hotels in the Riviera Maya, Mexico.

**Live site:** https://fiesta-artesanal-colibri.vercel.app/

---

## Tech Stack

- **HTML5** - Single-page, no build tools required
- **Tailwind CSS v3.4.17** - Via CDN
- **Vanilla JavaScript** - No frameworks or dependencies
- **Google Fonts** - Anton + Quicksand

### Why This Stack?

Zero dependencies = zero maintenance. The entire site is a single HTML file that runs anywhere. No npm, no build steps, no breaking updates.

---

## File Structure

```
fiesta-artesanal-colibri/
├── index.html          # Main (and only) page - contains all HTML, CSS, JS
├── favicon.svg         # SVG favicon with gradient
├── sitemap.xml         # SEO sitemap
├── robots.txt          # Search engine crawl rules
├── llms.txt            # LLM-readable business info
├── README.md           # This file
├── logo/
│   ├── fiesta-artesanal.png   # Main logo (transparent PNG)
│   ├── logo-color.jpg         # Color logo
│   └── logo-bw.png            # Black & white logo (footer)
├── images/
│   └── photos/                # All artisan/event photos (43 images)
└── copy/
    ├── content.txt            # Extracted text content from original PDF
    └── image-descriptions.txt # Image descriptions
```

---

## Design System

### Colors

Defined in Tailwind config (inside `index.html`):

| Name | Hex | Usage |
|------|-----|-------|
| `brand-dark` | `#0f1715` | Dark backgrounds, text |
| `brand-light` | `#f7f5f0` | Light backgrounds |
| `brand-accent` | `#c04a33` | CTAs, highlights, links |
| `brand-sage` | `#738678` | Eyebrows, subtle text |
| `brand-sand` | `#e8e4d9` | Section backgrounds |

### Typography

| Font | Usage | CSS Class |
|------|-------|-----------|
| **Anton** | Headlines, display text | `font-serif` |
| **Quicksand** | Body text, UI | `font-sans` |

**Anton guidelines:**
- Always uppercase
- Use `headline-spacing` class for tighter letter-spacing (-0.02em)
- Sizes: `text-4xl` to `text-9xl`

**Quicksand guidelines:**
- Regular weight (400) for body
- Bold (700) for emphasis, buttons, labels
- Sizes: `text-sm` to `text-xl`

### Spacing

- Section padding: `py-24 lg:py-32`
- Container: `max-w-7xl mx-auto px-6 lg:px-12`
- Component gaps: `gap-4`, `gap-6`, `gap-8`, `gap-12`

### Components

**Buttons:**
```html
<!-- Primary (accent) -->
<a class="bg-brand-accent text-white px-8 py-4 rounded-full text-xs uppercase tracking-widest font-bold hover:brightness-110 transition-all">

<!-- Secondary (outline) -->
<a class="border-2 border-white text-white px-8 py-3.5 rounded-full text-xs uppercase tracking-widest font-bold hover:bg-white hover:text-brand-dark transition-colors">
```

**Section eyebrow:**
```html
<p class="text-brand-sage uppercase tracking-[0.3em] font-bold text-xs mb-4">
```

**Accent border:**
```html
<div class="border-l-4 border-brand-accent pl-6">
```

---

## Internationalization (i18n)

The site is bilingual (Spanish/English) with a custom vanilla JS implementation.

### How It Works

1. **Text elements** have `data-i18n` or `data-i18n-html` attributes:
```html
<p data-i18n="hero.tagline">Spanish text here</p>
<h2 data-i18n-html="about.title">HTML with <span>tags</span></h2>
```

2. **Translations object** in JavaScript (bottom of `index.html`):
```javascript
const translations = {
    es: {
        'hero.tagline': 'Spanish text...',
        // ...
    },
    en: {
        'hero.tagline': 'English text...',
        // ...
    }
};
```

3. **Language toggle** calls `setLanguage('es')` or `setLanguage('en')`
4. **Persistence** via `localStorage.getItem('lang')`

### Adding New Translatable Text

1. Add the `data-i18n="key.name"` attribute to your HTML element
2. Add the key to both `es` and `en` objects in `translations`
3. For HTML content (with tags), use `data-i18n-html` instead

---

## Animations

### Scroll Reveal

Elements with class `reveal` fade in and slide up when they enter the viewport.

```html
<div class="reveal">Animates in</div>
<div class="reveal reveal-delay-1">Delayed 0.1s</div>
<div class="reveal reveal-delay-2">Delayed 0.2s</div>
```

**Available delays:** `reveal-delay-1` through `reveal-delay-4`

### Implementation

Uses Intersection Observer (performant, no scroll listeners):

```javascript
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('visible');
        }
    });
}, { threshold: 0.1 });
```

---

## Page Sections

| ID | Name | Background |
|----|------|------------|
| `#hero` | Hero | Dark with image overlay |
| `#nosotros` | About | Light |
| `#pilares` | Pillars/Values | Sand |
| `#servicios` | Services | Dark |
| `#talleres` | Workshops | Light |
| `#galeria` | Gallery | Sand |
| `#contacto` | Contact | Dark with image overlay |

---

## Common Changes

### Change Brand Colors

Edit the Tailwind config in `<script>` tag (around line 24):

```javascript
colors: {
    brand: {
        dark: '#0f1715',    // Change this
        accent: '#c04a33',  // Or this
        // ...
    }
}
```

### Add a New Section

1. Create section HTML following existing patterns
2. Add `id="section-name"` for navigation
3. Add nav link in both desktop and mobile menus
4. Add translations for any text

### Add New Photos to Gallery

1. Add images to `images/photos/`
2. Add `<div>` elements in the gallery grid:
```html
<div class="rounded-2xl overflow-hidden reveal">
    <img src="images/photos/new-image.jpg" alt="Description"
         class="w-full h-full object-cover aspect-square hover:scale-105 transition-transform duration-700">
</div>
```

### Update Contact Info

Search for phone numbers (`998 139 3285`, `998 539 1748`) and WhatsApp link (`wa.me/529981393285`).

---

## SEO Files

- **sitemap.xml** - Update `<lastmod>` date when making changes
- **robots.txt** - Allows all crawlers, points to sitemap
- **llms.txt** - Structured business info for AI assistants
- **Open Graph tags** - In `<head>` for social sharing

---

## Deployment

### Vercel (Recommended)

1. Push to GitHub
2. Import repo in Vercel
3. Deploy (no config needed - it's static HTML)

### Any Static Host

Just upload the files. No build step required.

---

## Performance Notes

- Images are not optimized - consider running through ImageOptim or similar
- Tailwind CSS is loaded via CDN (could be purged for smaller size)
- Fonts loaded from Google Fonts (consider self-hosting for speed)

---

## Credits

- **Design & Development:** [lowcode.agency](https://lowcode.agency)
- **Client:** Fiesta Artesanal Colibrí
- **Location:** Riviera Maya, Quintana Roo, Mexico
