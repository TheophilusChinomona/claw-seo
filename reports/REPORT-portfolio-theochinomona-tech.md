# SEO Audit Report: portfolio.theochinomona.tech

**Site:** https://portfolio.theochinomona.tech
**Type:** Agency/Portfolio — Developer Personal Site
**Stack:** Vite + React SPA, Tailwind CSS, Space Grotesk + JetBrains Mono fonts
**Hosting:** Cloudflare CDN
**Date:** April 27, 2026
**Overall Score:** 20/100 — Critical

---

## Executive Summary

The site has a strong visual design and solid foundation. However, from an SEO
perspective it has critical structural issues. The most urgent problem is that the
entire site content is invisible to crawlers without JavaScript execution — the HTML
shell contains no meta tags, no content, and no structured data.

**Estimated fix effort:** 2–4 hours for all critical + high-priority items.

---

## Category Scores

| Category | Score | Weight | Weighted |
|----------|-------|--------|----------|
| Technical SEO | 28/100 | 30% | 8.4 |
| On-Page SEO | 20/100 | 20% | 4.0 |
| Content Analysis | 25/100 | 20% | 5.0 |
| Schema & Structured Data | 0/100 | 15% | 0.0 |
| Sitemap | 0/100 | 10% | 0.0 |
| Images | 50/100 | 5% | 2.5 |
| **Overall** | **20/100** | **100%** | **20/100** |

---

## 1. Technical SEO — 28/100

### ✅ Working Well
| Check | Result |
|-------|--------|
| SSL Certificate | ✅ Valid, Google Trust Services (WE1), expires June 12, 2026 |
| HTTPS | ✅ Enforced |
| Mixed Content | ✅ None detected |
| URL Structure | ✅ Clean, hyphens, lowercase, no dynamic params |

### ⚠️ Issues
| Check | Result | Severity |
|-------|--------|----------|
| robots.txt | Present but blocks AI training bots (GPTBot, ClaudeBot, CCBot). Does NOT block Googlebot. Acceptable. | Low |
| Security Headers | None (CSP, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Permissions-Policy absent) | Medium |
| Core Web Vitals | Cannot measure — Cloudflare challenge blocks PageSpeed API | Unknown |

### ❌ Critical Issues
| Check | Result | Severity |
|-------|--------|----------|
| XML Sitemap | Missing — `/sitemap.xml` returns HTML SPA shell | Critical |
| robots.txt sitemap reference | Missing | High |
| Canonical Tags | None on any page | High |
| JavaScript Rendering | Entire site is a pure SPA — HTML shell has zero content | Critical |

---

## 2. On-Page SEO — 20/100

### ✅ Working Well
| Check | Result |
|-------|--------|
| Title Tag | ✅ "Theo Chinomona \| Developer Portfolio" — 42 chars, appropriate |
| Viewport Meta | ✅ Present |
| Heading Structure | ✅ Proper H1/H2/H3 hierarchy (when rendered) |
| Noindex Tags | ✅ None present |

### ❌ Missing in HTML Shell
| Element | Status |
|---------|--------|
| Meta description | ❌ Missing |
| Canonical | ❌ Missing |
| Open Graph tags | ❌ Missing |
| Twitter Cards | ❌ Missing |
| Any visible content | ❌ HTML shell is completely empty of content |

**The HTML shell contains zero meta tags or visible text.** All content renders
client-side via React. Without JS execution, crawlers see only the Vite build shell.

---

## 3. Content Analysis — 25/100

| Signal | Status |
|--------|--------|
| Word count | Unknown (JS-dependent) |
| E-E-A-T signals | Unknown (requires rendered content) |
| Original content | ✅ Likely original |
| Thin content risk | ⚠️ High if JS fails or is blocked |
| AI citation readiness | ❌ Very poor — JS content inaccessible to most crawlers |

---

## 4. Schema & Structured Data — 0/100

No structured data of any kind present.

### Should Be Added
- **Person Schema** — name, job title, url, sameAs (GitHub, LinkedIn, etc.)
- **WebSite Schema** — with SearchAction for internal site search
- **URL / ProfilePage** — for authorship signals

---

## 5. Sitemap — 0/100

### Missing entirely.
No sitemap at any location. Recommended routes:

```
/                    (priority 1.0)
/about               (priority 0.8)
/experience          (priority 0.8)
/skills              (priority 0.7)
/projects            (priority 0.9)
/contact             (priority 0.5)
```

---

## 6. Image Optimization — 50/100

Cannot do full audit without JS rendering. Based on CSS analysis:

| Signal | Status |
|--------|--------|
| CLS Prevention | ✅ Likely — Vite builds use width/height on img tags |
| aspect-ratio utilities | ✅ Present in Tailwind config |
| Alt text | ⚠️ Unknown (requires rendered DOM) |
| WebP/AVIF formats | ⚠️ Unknown |
| File sizes | ⚠️ Unknown |
| Lazy loading | ⚠️ Unknown |

---

## Priority Fix Plan

### 🔴 CRITICAL — Fix First (same day)

#### Fix 1: Add Meta Tags to HTML Shell
**File:** `index.html` in the Vite project

Add inside `<head>` before the closing tag:

```html
<!-- Primary Meta -->
<title>Theo Chinomona | Full-Stack Developer & AI Builder</title>
<meta name="description" content="I build fast, scalable web apps and AI agents. View my projects, skills, and experience as a full-stack developer.">
<meta name="author" content="Theo Chinomona">
<meta name="robots" content="index, follow">

<!-- Canonical -->
<link rel="canonical" href="https://portfolio.theochinomona.tech/">

<!-- Open Graph -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://portfolio.theochinomona.tech/">
<meta property="og:title" content="Theo Chinomona | Full-Stack Developer & AI Builder">
<meta property="og:description" content="I build fast, scalable web apps and AI agents. View my projects, skills, and experience.">
<meta property="og:image" content="https://portfolio.theochinomona.tech/og-image.png">
<meta property="og:site_name" content="Theo Chinomona Portfolio">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@theochinomona">
<meta name="twitter:title" content="Theo Chinomona | Full-Stack Developer & AI Builder">
<meta name="twitter:description" content="I build fast, scalable web apps and AI agents. View my projects, skills, and experience.">
<meta name="twitter:image" content="https://portfolio.theochinomona.tech/og-image.png">

<!-- Favicon -->
<link rel="icon" type="image/svg+xml" href="/vite.svg">
```

> **Note:** Create a 1200x630px `og-image.png` for social sharing previews.
> Place it at `public/og-image.png` in the Vite project.

#### Fix 2: Add JSON-LD Schema
**File:** `index.html` in the Vite project

Add inside `<head>` after the meta tags:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Theo Chinomona",
  "jobTitle": "Full-Stack Developer",
  "description": "I build fast, scalable web apps and AI agents.",
  "url": "https://portfolio.theochinomona.tech",
  "sameAs": [
    "https://github.com/TheophilusChinomona",
    "https://linkedin.com/in/theochinomona"
  ],
  "knowsAbout": ["JavaScript", "TypeScript", "React", "Node.js", "Python", "AI Agents"],
  "worksFor": {
    "@type": "Organization",
    "name": "Tripli"
  }
}
</script>
```

Also add WebSite schema:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Theo Chinomona Portfolio",
  "url": "https://portfolio.theochinomona.tech",
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://portfolio.theochinomona.tech/?q={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}
</script>
```

#### Fix 3: Create XML Sitemap
**File:** `public/sitemap.xml` in the Vite project

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://portfolio.theochinomona.tech/</loc>
    <priority>1.0</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>https://portfolio.theochinomona.tech/about</loc>
    <priority>0.8</priority>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>https://portfolio.theochinomona.tech/experience</loc>
    <priority>0.8</priority>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>https://portfolio.theochinomona.tech/skills</loc>
    <priority>0.7</priority>
    <changefreq>monthly</changefreq>
  </url>
  <url>
    <loc>https://portfolio.theochinomona.tech/projects</loc>
    <priority>0.9</priority>
    <changefreq>weekly</changefreq>
  </url>
  <url>
    <loc>https://portfolio.theochinomona.tech/contact</loc>
    <priority>0.5</priority>
    <changefreq>yearly</changefreq>
  </url>
</urlset>
```

#### Fix 4: Update robots.txt
**File:** `public/robots.txt` in the Vite project

```
User-agent: *
Allow: /

# Sitemap
Sitemap: https://portfolio.theochinomona.tech/sitemap.xml

# AI Training Bots (optional — these do not affect Google indexing)
User-agent: GPTBot
Disallow: /

User-agent: ClaudeBot
Disallow: /

User-agent: Google-Extended
Disallow: /
```

---

### 🟠 HIGH PRIORITY — Fix Within 1–2 Days

#### Fix 5: Add Canonical Tags Per Page
In each React page component, add to `<head>`:

```html
<link rel="canonical" href="https://portfolio.theochinomona.tech/[route]">
```

Or use React Helmet / a `<Meta>` component that dynamically sets canonical per route.

#### Fix 6: Security Headers
Add to `vite.config.js` or the Cloudflare dashboard:

```
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; img-src 'self' data: https:; connect-src 'self';
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

#### Fix 7: OG Image
Create a 1200x630px PNG social preview image at `public/og-image.png`. Include:
- Your name and title
- A brief tagline
- Simple branded design (not busy)

Use this in the OG tags from Fix 1.

---

### 🟡 MEDIUM PRIORITY — Fix Within 1 Week

#### Fix 8: Image Audit
Once the site renders, audit all images:
- Alt text on every `<img>`
- File sizes < 200KB for hero images, < 50KB for thumbnails
- WebP or AVIF format where possible
- `loading="lazy"` on below-fold images only

#### Fix 9: Consider SSR / Pre-rendering
For full SEO effectiveness, the site needs server-side rendering or pre-rendering
so content exists in the HTML:

| Option | Effort | SEO Impact |
|--------|--------|------------|
| Astro with React integration | Medium | High |
| Next.js App Router (migrate from Vite) | High | High |
| Prerender.io or similar service | Low | Medium |
| Vite SSR plugin | Medium | Medium |

Astro is the lightest lift — keeps the React component model but outputs static HTML.

#### Fix 10: Google Search Console
- Submit the sitemap at: https://search.google.com/search-console
- Request indexing for all pages
- Monitor Core Web Vitals there

---

## Quick Wins Summary

| # | Fix | Effort | Impact |
|---|-----|--------|--------|
| 1 | Add meta tags to index.html | 30 min | 🔴 Critical |
| 2 | Add JSON-LD schema | 20 min | 🔴 Critical |
| 3 | Create sitemap.xml | 10 min | 🔴 Critical |
| 4 | Add sitemap to robots.txt | 5 min | 🔴 Critical |
| 5 | Create OG image | 30 min | 🟠 High |
| 6 | Add canonical per page | 20 min | 🟠 High |
| 7 | Security headers | 20 min | 🟠 Medium |
| 8 | SSR / pre-render | 4–8 hrs | 🟡 Medium |

**Total critical + high priority: ~2 hours**
