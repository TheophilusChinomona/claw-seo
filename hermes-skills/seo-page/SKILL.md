---
name: seo-page
description: >
  Deep single-page SEO analysis. Covers all on-page factors: title, meta description,
  headings, content, images, links, schema, Core Web Vitals, and mobile usability.
  Use when user says analyze page, single page, page audit, or check this URL.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Single Page SEO Analysis

## On-Page Factors Checklist

### Title Tag
- [ ] 50-60 characters
- [ ] Primary keyword near the beginning
- [ ] Unique per page (no duplicate titles)
- [ ] Readable (no keyword stuffing)
- [ ] Brand name at end (format: "Title | Brand")

### Meta Description
- [ ] 150-160 characters
- [ ] Call-to-action included
- [ ] Primary + secondary keywords included
- [ ] Unique per page
- [ ] Accurately describes page content

### Heading Structure (H1-H6)
- [ ] Exactly one H1 per page
- [ ] H1 matches or closely relates to title tag
- [ ] Logical heading hierarchy (no skipped levels)
- [ ] Keywords in H2s and H3s where natural
- [ ] No heading spam (same keyword in multiple H2s)

### Content Quality
- [ ] Word count appropriate for page type (see seo-content thresholds)
- [ ] Primary keyword in first 100 words
- [ ] Keyword density 0.5-3% (avoid stuffing)
- [ ] LSI/semantic keywords used naturally
- [ ] External links to authoritative sources
- [ ] Images with alt text

### Images
- [ ] Alt text on all images (descriptive, keyword-inclusive)
- [ ] Image file names descriptive (e.g., `seo-checklist.jpg` not `IMG_1234.jpg`)
- [ ] Images compressed (WebP preferred, <150KB for heroes)
- [ ] Width/height attributes set (prevents CLS)
- [ ] Lazy loading for below-fold images

### Internal Links
- [ ] Links to related pages on site
- [ ] Descriptive anchor text (no "click here")
- [ ] No broken links
- [ ] No excessive links (rule of thumb: <100 per page)

### URL
- [ ] Descriptive, readable (not `/page?id=123`)
- [ ] Primary keyword included
- [ ] Hyphens as separators (not underscores)
- [ ] Consistent lowercase
- [ ] No parameters unless necessary

### Schema/Structured Data
- [ ] JSON-LD present and valid
- [ ] Matches page content type
- [ ] No deprecated schema types

### Core Web Vitals (INP)
- [ ] LCP < 2.5s
- [ ] INP < 200ms
- [ ] CLS < 0.1

### Mobile Usability
- [ ] Responsive design
- [ ] Viewport meta tag present
- [ ] No horizontal scroll
- [ ] Tap targets ≥ 48px
- [ ] Font readable without zooming

## Analysis Approach

1. Scrape the page with `mcp_firecrawl_firecrawl_scrape(url, formats=["markdown", "html"])`
2. Parse the HTML structure for SEO elements
3. Run PageSpeed check: `python3 /workspace/claw-seo/scripts/pagespeed_check.py <url> --json`
4. Capture screenshot: `python3 /workspace/claw-seo/scripts/capture_screenshot.py <url>`
5. Score each factor and aggregate

## Output Format

```
# Single Page SEO Analysis — {url}

## Scores
| Factor | Score | Status |
|--------|-------|--------|
| Title Tag | XX/100 | ✅/⚠️/❌ |
| Meta Description | XX/100 | ✅/⚠️/❌ |
| Heading Structure | XX/100 | ✅/⚠️/❌ |
| Content Quality | XX/100 | ✅/⚠️/❌ |
| Images | XX/100 | ✅/⚠️/❌ |
| Internal Links | XX/100 | ✅/⚠️/❌ |
| URL | XX/100 | ✅/⚠️/❌ |
| Schema | XX/100 | ✅/⚠️/❌ |
| Core Web Vitals | XX/100 | ✅/⚠️/❌ |
| Mobile Usability | XX/100 | ✅/⚠️/❌ |

## Overall Page Score: {score}/100 ({grade})

## Critical Issues
{critical_issues}

## Recommendations
{recommendations}

## Quick Wins
{quick_wins}
```
