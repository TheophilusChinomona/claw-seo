---
name: seo-images
description: >
  Image optimization analysis for SEO and performance. Checks alt text, file sizes,
  formats, responsive images (srcset), lazy loading, CLS prevention, image SERP
  rankings, and file optimization (WebP/AVIF conversion). Use when user says
  image optimization, alt text, image SEO, image size, image audit, optimize images,
  image metadata, image SERP, or convert to WebP.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Image Optimization Analysis

## Checks

### Alt Text
- Present on all `<img>` elements (except decorative: `role="presentation"`)
- Descriptive: describes the image content, not "image.jpg" or "photo"
- Includes relevant keywords where natural, not keyword-stuffed
- Length: 10-125 characters

**Good examples:**
- "Professional plumber repairing kitchen sink faucet"
- "Red 2024 Toyota Camry sedan front view"
- "Team meeting in modern office conference room"

**Bad examples:**
- "image.jpg" (filename, not description)
- "plumber plumbing plumber services" (keyword stuffing)
- "Click here" (not descriptive)

### File Size

| Image Category | Target | Warning | Critical |
|----------------|--------|---------|----------|
| Thumbnails | < 50KB | > 100KB | > 200KB |
| Content images | < 100KB | > 200KB | > 500KB |
| Hero/banner images | < 200KB | > 300KB | > 700KB |

### Format

| Format | Browser Support | Use Case |
|--------|----------------|----------|
| WebP | 97%+ | Default recommendation |
| AVIF | 92%+ | Best compression, newer |
| JPEG | 100% | Fallback for photos |
| PNG | 100% | Graphics with transparency |
| SVG | 100% | Icons, logos, illustrations |

### Recommended `<picture>` Pattern

```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg"
       alt="Descriptive alt text"
       width="800" height="600"
       loading="lazy" decoding="async">
</picture>
```

Browser uses first supported format. AVIF 93.8%, WebP 95.3%.

### Responsive Images
- `srcset` attribute for multiple sizes
- `sizes` attribute matching layout breakpoints
- Appropriate resolution for device pixel ratios

```html
<img
  src="image-800.jpg"
  srcset="image-400.jpg 400w, image-800.jpg 800w, image-1200.jpg 1200w"
  sizes="(max-width: 600px) 400px, (max-width: 1200px) 800px, 1200px"
  alt="Description"
>
```

### Lazy Loading
- `loading="lazy"` on below-fold images
- Do NOT lazy-load above-fold/hero images (hurts LCP)
- Check for native vs JavaScript-based lazy loading

### CLS Prevention
- `width` and `height` attributes on all `<img>`
- `aspect-ratio` CSS property for reserve space
- No layout shifts after image loads

### Image File Names
- Descriptive: `seo-checklist.jpg` not `IMG_1234.jpg`
- Hyphens as word separators (not underscores)
- Keywords where relevant and natural

## Image Sitemap

For image-heavy sites, recommend image sitemap:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:image="http://www.google.com/schemas/sitemap-image/1.1">
  <url>
    <loc>https://example.com/blog/seo-guide</loc>
    <image:image>
      <image:loc>https://example.com/images/seo-guide-hero.webp</image:loc>
      <image:title>Complete SEO Guide for Beginners</image:title>
      <image:caption>Step-by-step SEO checklist</image:caption>
    </image:image>
  </url>
</urlset>
```

## Image SEO Checklist

```
## Alt Text
- [ ] All content images have descriptive alt text
- [ ] No alt text keyword stuffing
- [ ] Alt text 10-125 characters
- [ ] Decorative images marked role="presentation"

## File Size
- [ ] Thumbnails < 50KB
- [ ] Content images < 100KB
- [ ] Hero images < 200KB
- [ ] Using WebP or AVIF format

## Format
- [ ] <picture> element with format fallbacks
- [ ] JPEG for photos, PNG for graphics
- [ ] SVG for icons and logos

## Responsive
- [ ] srcset with multiple sizes
- [ ] sizes attribute correct
- [ ] Correct resolution for device pixel ratios

## CLS Prevention
- [ ] width/height attributes on all images
- [ ] No layout shifts after load

## Lazy Loading
- [ ] Below-fold images lazy-loaded
- [ ] Above-fold/hero images NOT lazy-loaded
```

## Output Format

```
# Image SEO Analysis — {domain}

## Alt Text: {score}/100
- Total images: {count}
- Images with alt text: {count}
- Missing alt text: {count}
- Descriptive alt text: {count}
- Keyword stuffed: {count}

## File Sizes
| Category | Count | Under Target | Over Target |
|----------|-------|-------------|-------------|
| Thumbnail | {n} | {n} | {n} |
| Content | {n} | {n} | {n} |
| Hero | {n} | {n} | {n} |

## Format Distribution
| Format | Count | Percentage |
|--------|-------|------------|
| WebP | {n} | {pct} |
| AVIF | {n} | {pct} |
| JPEG | {n} | {pct} |
| PNG | {n} | {pct} |

## Issues Found
{category_findings}

## Recommendations
{recommendations}
```
