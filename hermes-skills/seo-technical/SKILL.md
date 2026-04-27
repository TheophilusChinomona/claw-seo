---
name: seo-technical
description: >
  Technical SEO audit across 9 categories: crawlability, indexability, security,
  URL structure, mobile, Core Web Vitals, structured data, JavaScript rendering,
  and IndexNow protocol. Use when user says technical SEO, crawl issues, robots.txt,
  Core Web Vitals, site speed, or security headers.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Technical SEO Audit

## 9 Audit Categories

### 1. Crawlability
- robots.txt: exists, valid, not blocking important resources
- XML sitemap: exists, referenced in robots.txt, valid format
- Noindex tags: intentional vs accidental
- Crawl depth: important pages within 3 clicks of homepage
- JavaScript rendering: critical content requires JS execution
- Crawl budget: for large sites (>10k pages), efficiency matters

#### AI Crawler Management (2025-2026)

Manage AI training crawlers via robots.txt:

| Crawler | Company | Token | Purpose |
|---------|---------|-------|---------|
| GPTBot | OpenAI | `GPTBot` | Model training |
| ChatGPT-User | OpenAI | `ChatGPT-User` | Real-time browsing |
| ClaudeBot | Anthropic | `ClaudeBot` | Model training |
| PerplexityBot | Perplexity | `PerplexityBot` | Search index |
| Google-Extended | Google | `Google-Extended` | Gemini training ONLY |
| CCBot | Common Crawl | `CCBot` | Open dataset |

**Key distinction:** Blocking `Google-Extended` does NOT affect Google Search indexing or AI Overviews — those use `Googlebot`.

**Selective blocking example:**
```
User-agent: GPTBot
Disallow: /

User-agent: Google-Extended
Disallow: /

User-agent: *
Allow: /
```

### 2. Indexability
- Canonical tags: self-referencing, no conflicts with noindex
- Duplicate content: near-duplicates, parameter URLs, www vs non-www
- Thin content: pages below minimum word counts per type
- Pagination: rel=next/prev or load-more pattern
- Hreflang: correct for multi-language/multi-region sites
- Index bloat: unnecessary pages consuming crawl budget

### 3. Security
- HTTPS: enforced, valid SSL certificate, no mixed content
- Security headers:
  - Content-Security-Policy (CSP)
  - X-Frame-Options
  - X-Content-Type-Options
  - Referrer-Policy
  - Permissions-Policy

### 4. URL Structure
- Descriptive, readable URLs
- Consistent URL structure (trailing slashes)
- No infinite parameters (e.g., `?session=`)
- Hyphens as word separators (not underscores)
- No case sensitivity issues

### 5. Mobile
- Responsive design
- Viewport meta tag present
- Tap target sizing (minimum 48x48px)
- Font legibility on mobile
- No horizontal scroll

### 6. Core Web Vitals (INP —取代 FID)

| Metric | Target | What it measures |
|--------|--------|----------------|
| LCP | < 2.5s | Largest Contentful Paint — load speed |
| INP | < 200ms | Interaction to Next Paint — responsiveness |
| CLS | < 0.1 | Cumulative Layout Shift — visual stability |

> **INP replaced FID** on March 12, 2024. FID fully removed from Chrome tools Sept 9, 2024.

Use `mcp_firecrawl_firecrawl_scrape` with PageSpeed analysis, or call:
```bash
python3 /workspace/claw-seo/scripts/pagespeed_check.py <url> --json
```

### 7. Structured Data
- Schema.org markup present (JSON-LD preferred)
- Valid JSON-LD syntax
- No deprecated schema types:
  - HowTo (deprecated Sept 2023)
  - FAQPage (restricted to gov/health sites, Aug 2023)
  - SpecialAnnouncement (deprecated July 2025)

### 8. JavaScript Rendering
- Critical content visible without JS
- Lazy-loaded content has fallback
- No content behind infinite scroll without "Load More"
- Server-side rendering (SSR) or pre-rendering recommended

### 9. IndexNow Protocol
- Site supports IndexNow for instant URL submission
- Sitemap includes lastmod dates

## Audit Commands

```bash
# PageSpeed Insights + CrUX
python3 /workspace/claw-seo/scripts/pagespeed_check.py <url> --json

# Fetch page HTML
python3 /workspace/claw-seo/scripts/fetch_page.py <url>

# Parse HTML for SEO elements
python3 /workspace/claw-seo/scripts/parse_html.py <url>
```

## Output Format

```
# Technical SEO Audit — {domain}

## Category Scores (0-100)
| Category | Score | Status |
|----------|-------|--------|
| Crawlability | XX | ✅/⚠️/❌ |
| Indexability | XX | ✅/⚠️/❌ |
| Security | XX | ✅/⚠️/❌ |
| URL Structure | XX | ✅/⚠️/❌ |
| Mobile | XX | ✅/⚠️/❌ |
| Core Web Vitals | XX | ✅/⚠️/❌ |
| Structured Data | XX | ✅/⚠️/❌ |
| JS Rendering | XX | ✅/⚠️/❌ |
| IndexNow | XX | ✅/⚠️/❌ |

## Findings by Category
{category_findings}

## Priority Fixes
{prioritized_fixes}
```
