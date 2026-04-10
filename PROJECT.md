# MacDonald Law Office — Website Project

**Live URL:** https://macdonaldlaw.ca
**Repository:** https://github.com/macdonlw/macdonaldlaw-website
**Hosting:** GitHub Pages (branch: `main`, root `/`)
**HTTPS:** Not enforced (should be enabled)
**Domain:** macdonaldlaw.ca (configured via `CNAME` file)

---

## Overview

Static HTML website for MacDonald Law Office, a solo practice in Smiths Falls, Ontario. Mark MacDonald has practised criminal defence, real estate law, and wills & powers of attorney since 2002. The site serves as the firm's public presence, with a contact form for potential client inquiries.

---

## Tech Stack

| Component        | Technology                           | Version  | Notes                                    |
|------------------|--------------------------------------|----------|------------------------------------------|
| CSS Framework    | Tailwind CSS (CDN)                   | 3.4.17   | Runtime config in each HTML file         |
| Icons            | Lucide Icons (CDN)                   | 1.8.0    | Full UMD bundle via unpkg               |
| Fonts            | Google Fonts                         | —        | Cormorant Garamond (serif), DM Sans (sans) |
| Contact Form     | Formspree                            | —        | Endpoint: `mnjoyoza`                     |
| Hosting          | GitHub Pages                         | —        | Deploys from `main` branch               |
| Build Tooling    | None                                 | —        | No Node.js, no build step                |
| Version Control  | Git / GitHub                         | —        | Account: `macdonlw`                      |

**No CMS, no build pipeline.** All changes are direct HTML edits pushed to `main`.

---

## File Structure

```
macdonaldlaw-website/
├── CNAME                    # GitHub Pages custom domain (macdonaldlaw.ca)
├── index.html               # Homepage — hero, trust bar, intro, practice areas, FAQ
├── about.html               # About Mark MacDonald — bio, values, office details
├── practice-areas.html      # Detailed practice area pages with anchor sections
├── real-estate.html         # Dedicated real estate page — closing cost calculator, quote form, FAQs
├── contact.html             # Contact form (Formspree), office info, Google Maps
├── 404.html                 # Custom 404 error page
├── faq.html                 # Standalone FAQ page (legacy — uses css/style.css)
├── testimonials.html        # Testimonials page (legacy — uses css/style.css)
├── style-guide.html         # Internal style guide / design reference
├── css/
│   └── style.css            # Legacy stylesheet (used by faq.html, testimonials.html)
└── PROJECT.md               # This file
```

### Page Status

| Page                  | Design System    | SEO Meta | OG Tags | Schema.org     | Canonical | CSP | Contrast Fix |
|-----------------------|------------------|----------|---------|----------------|-----------|-----|--------------|
| `index.html`          | Tailwind + custom| Yes      | Yes     | LegalService, WebSite, FAQPage | Yes | Yes | Yes |
| `about.html`          | Tailwind + custom| Yes      | Yes     | Person         | Yes       | Yes | Yes          |
| `practice-areas.html` | Tailwind + custom| Yes      | Yes     | LegalService + Services | Yes | Yes | Yes     |
| `real-estate.html`    | Tailwind + custom| Yes      | Yes     | LegalService, FAQPage | Yes | Yes | Yes    |
| `contact.html`        | Tailwind + custom| Yes      | Yes     | ContactPage    | Yes       | Yes | Yes          |
| `404.html`            | Tailwind + custom| noindex  | —       | —              | —         | —   | —            |
| `faq.html`            | Legacy (css/style.css) | Basic | No | No            | No        | No  | No           |
| `testimonials.html`   | Legacy (css/style.css) | Basic | No | No            | No        | No  | No           |
| `style-guide.html`    | Tailwind (internal)    | No   | No | No            | No        | No  | No           |

---

## Design System

### Colors

| Name           | Hex       | Usage                                      |
|----------------|-----------|---------------------------------------------|
| Primary (Navy) | `#1B2A4A` | Headings, nav, footer, dark sections        |
| Primary Light  | `#2A3D66` | Hover states, borders                       |
| Primary Dark   | `#111D35` | Top bar, mobile menu bg                     |
| Accent (Gold)  | `#B8942D` | CTAs, links, dividers, icons on dark bg     |
| Accent Hover   | `#9A7B22` | Button hover states                         |
| Accent Dark    | `#866812` | Accessible accent text on light backgrounds |
| Cream          | `#FAF9F6` | Page background                             |
| Cream Dark     | `#F2F0EB` | Alternating section backgrounds             |
| Charcoal       | `#1A1A1A` | Body text                                   |
| Warm 100–500   | `#F7F5F0` → `#7A7267` | Borders, muted text, subtle bg     |

### Typography

| Role     | Font              | Weights          |
|----------|-------------------|------------------|
| Headings | Cormorant Garamond| 400, 500, 600, 700 |
| Body     | DM Sans           | 400, 500, 600, 700 |

### Key CSS Classes

- `.btn-transition` — smooth 0.25s ease transition on all properties
- `.card-lift` — hover: translateY(-6px) with shadow
- `.fade-in` / `.visible` — IntersectionObserver scroll animation
- `.nav-link::after` — gold underline on hover/active
- `.divider` — 48px x 2px gold accent bar
- `.skip-link` — accessible skip-to-content link

---

## Contact Form

**Endpoint:** `https://formspree.io/f/mnjoyoza`
**Emails to:** `reception@smithsfallslawyer.com`
**Formspree Account:** Mark MacDonald
**Free Tier Limit:** 50 submissions/month

### Fields

| Field          | Type     | Name             | Required | Notes           |
|----------------|----------|------------------|----------|-----------------|
| Full Name      | text     | `full-name`      | Yes      |                 |
| Email          | email    | `email`          | Yes      | Validated       |
| Phone          | tel      | `phone`          | Yes      |                 |
| Practice Area  | select   | `practice-area`  | Yes      | 4 options       |
| Message        | textarea | `message`        | Yes      |                 |
| Honeypot       | text     | `website`        | No       | Hidden, anti-spam |

### Behavior

- Client-side validation (required fields, email format)
- Honeypot field hidden via absolute positioning — bots that fill it are silently rejected
- On success: form hides, green success message shown
- On error: red error message with phone/email fallback
- Submit button shows "Sending..." while request is in flight

---

## Real Estate Page (real-estate.html)

Dedicated landing page for real estate law services, designed to drive SEO traffic.

- Free quote request form submits to same Formspree endpoint (`mnjoyoza`)
- 10 FAQ items targeting long-tail real estate keywords
- Service area content: Smiths Falls, Perth, Carleton Place, Almonte, Merrickville, Kemptville
- Step-by-step closing process explainer
- "What We Handle for You" service breakdown

---

## SEO & Structured Data

### Meta Tags (all 5 main pages)

- `<meta name="description">` — unique per page
- `<meta name="robots" content="index, follow">`
- `<link rel="canonical">` — absolute URL per page
- `<meta property="og:title|description|type|url">` — Open Graph

### Schema.org (JSON-LD)

| Page              | Schema Types                        |
|-------------------|-------------------------------------|
| `index.html`      | LegalService, WebSite, FAQPage (3 questions) |
| `about.html`      | Person (Mark MacDonald, jobTitle: Lawyer) |
| `practice-areas`  | LegalService with OfferCatalog (3 services) |
| `real-estate.html`| LegalService, FAQPage (10 questions) |
| `contact.html`    | ContactPage with LegalService entity |

---

## Security

### Content Security Policy (all 4 main pages)

```
default-src 'self';
script-src 'self' 'unsafe-inline' 'unsafe-eval' cdn.tailwindcss.com unpkg.com;
style-src 'self' 'unsafe-inline' fonts.googleapis.com;
font-src fonts.gstatic.com;
img-src 'self' data:;
connect-src 'self';
```

Contact page additionally allows:
- `frame-src www.google.com` (Maps embed)
- `connect-src formspree.io` (form submission)

### Notes

- `'unsafe-inline'` and `'unsafe-eval'` required by Tailwind CDN runtime — can be removed if Tailwind is compiled at build time
- No analytics scripts currently active (placeholders only)

---

## Accessibility

- Skip-to-main-content link on all pages
- ARIA attributes on mobile menu toggle (`aria-label`, `aria-expanded`)
- Semantic HTML (`<nav>`, `<main>`, `<footer>`, `<section>`)
- Color contrast fix: accent gold darkened to `#866812` on light backgrounds (WCAG AA 4.5:1)
- `<details>`/`<summary>` for FAQ accordion (native keyboard support)
- `loading="lazy"` on Google Maps iframe

### Known Issues

- Gold accent (`#B8942D`) on white backgrounds only passes WCAG AA at the overridden `#866812` — the CSS selector-based override may not catch every instance
- No `alt` text on images (site currently has no `<img>` elements)
- Mobile menu `max-height: 400px` on index/about could clip if content grows

---

## Analytics

**Status:** Not active. Commented-out snippets are in all 4 main pages.

Two options ready to uncomment:
1. **Plausible** (recommended) — privacy-friendly, no cookies, GDPR-compliant
2. **Google Analytics 4** — requires a `G-XXXXXXXXXX` measurement ID

---

## Git History

| Commit   | Description                                                  |
|----------|--------------------------------------------------------------|
| `6602e0a`| Update bio: born and raised in Smiths Falls                  |
| `e1d5e8b`| SEO, contact form, security, accessibility improvements      |
| `806874c`| Add files via upload                                         |
| `6a51da8`| Add files via upload                                         |
| `60ba8ca`| Initial MacDonald Law Office website                         |

---

## Known Issues & Technical Debt

### High Priority

1. **HTTPS not enforced** — GitHub Pages has HTTPS available but `https_enforced` is `false`. Should be enabled in repo Settings > Pages.
2. **Legacy pages (faq.html, testimonials.html)** use the old `css/style.css` design system with completely different styling, nav, and layout from the main 4 pages. These need to be rebuilt in the current Tailwind design or removed/redirected.
3. **Tailwind CDN in production** — the full Tailwind framework (~300KB) is sent to every visitor. A build step with purging would reduce this to ~5-10KB. Requires Node.js.
4. **Lucide full library loaded** — the entire icon library is loaded for ~15 icons. Inline SVGs would eliminate this dependency entirely.

### Medium Priority

5. **No `og:image`** — Open Graph tags exist but no image is specified. Social shares won't have a preview image. Need to create a 1200x630px branded image.
6. **Google Maps embed uses generic coordinates** — the iframe URL uses lat/long but not a Place ID. Getting a proper Google Maps embed with the business pin would be more accurate.
7. **style-guide.html is publicly accessible** — this is an internal design reference and probably shouldn't be deployed/indexed. Add `noindex` or remove from production.
8. **No favicon** — no `<link rel="icon">` on any page. Browser tabs show the default icon.
9. **No sitemap.xml or robots.txt** — would help search engine crawling.
10. **Copyright footer inconsistency** — some pages had 2024, now fixed to 2025, but should ideally be dynamic or updated annually.

### Low Priority

11. **Duplicate Tailwind config** — the same `tailwind.config` block is copy-pasted in every HTML file. If one color changes, all files must be updated manually.
12. **No print stylesheet** — users printing practice area or contact info get the screen layout.
13. **No service worker / offline support** — not critical for a law office site.
14. **Form rate limiting** — Formspree handles some of this, but no client-side rate limiting exists.

---

## Deployment

### How to Deploy Changes

1. Edit HTML files locally
2. `git add <files>`
3. `git commit -m "description"`
4. `git push origin main`
5. GitHub Pages rebuilds automatically (typically 30-60 seconds)

### How to Verify

- Check https://macdonaldlaw.ca after push
- Check deployment status: `gh api repos/macdonlw/macdonaldlaw-website/pages --jq '.status'`

---

## Accounts & Services

| Service     | Account         | Purpose                          |
|-------------|-----------------|----------------------------------|
| GitHub      | `macdonlw`      | Code hosting, GitHub Pages       |
| Formspree   | Mark MacDonald  | Contact form submissions         |
| Google Fonts| Public CDN      | Typography (no account needed)   |

---

## Roadmap / Future Improvements

- [ ] Enable HTTPS enforcement in GitHub Pages settings
- [ ] Rebuild `faq.html` and `testimonials.html` in current design system
- [ ] Create `og:image` for social sharing
- [ ] Add `favicon.ico` and Apple touch icons
- [ ] Add `sitemap.xml` and `robots.txt`
- [ ] Add `noindex` to `style-guide.html` or remove from production
- [ ] Set up Plausible or GA4 analytics
- [ ] Install Node.js and compile Tailwind CSS with purging
- [ ] Replace Lucide CDN with inline SVGs for used icons only
- [ ] Add proper Google Maps Place ID embed
- [ ] Consider adding a blog or news section for SEO content
- [ ] Annual review: update copyright year, review Schema.org data

---

*Last updated: 2026-04-09*
*Maintained by: Mark MacDonald with Claude Code assistance*
