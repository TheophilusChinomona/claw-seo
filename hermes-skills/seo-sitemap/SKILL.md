---
name: seo-sitemap
description: >
  XML sitemap analysis and generation. Validates existing sitemaps, checks for
  quality issues, and generates industry-specific sitemap templates. Use when
  user says sitemap, XML sitemap, generate sitemap, or sitemap analysis.
user-invokable: true
argument-hint: "<url or 'generate'>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# XML Sitemap Analysis & Generation

## Sitemap Analysis Process

1. Check if sitemap exists at standard locations:
   - `/sitemap.xml` (most common)
   - `/sitemap_index.xml`
   - `/sitemap.xml.gz`
   - `/wp-sitemap.xml` (WordPress)

2. Parse sitemap for:
   - URL count and patterns
   - `<lastmod>` presence and accuracy
   - `<changefreq>` values
   - `<priority>` values
   - Protocol compliance (XML namespace)

3. Validate against quality gates

## Sitemap Quality Gates

| Check | Pass | Fail |
|-------|------|------|
| Valid XML | Well-formed | Malformed |
| HTTPS URLs only | All HTTPS | HTTP URLs present |
| Canonical alignment | URLs match canonicals | Canonical conflicts |
| Response codes | All 200 | Dead URLs (4xx/5xx) |
| Size | < 50MB or < 50k URLs | Exceeds limits |
| lastmod dates | Present, valid | Missing or future dates |
| Images in sitemap | Product/image pages included | Missing |
| News sitemaps | News sites only | Non-news sites |

## Industry Sitemap Templates

### SaaS
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://example.com/</loc><priority>1.0</priority><changefreq>weekly</changefreq></url>
  <url><loc>https://example.com/features/</loc><priority>0.9</priority></url>
  <url><loc>https://example.com/pricing/</loc><priority>0.8</priority></url>
  <url><loc>https://example.com/blog/</loc><priority>0.8</priority></url>
  <url><loc>https://example.com/docs/</loc><priority>0.7</priority></url>
</urlset>
```

### E-commerce
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:image="http://www.google.com/schemas/sitemap-image/1.1">
  <url><loc>https://example.com/</loc><priority>1.0</priority></url>
  <url><loc>https://example.com/collections/</loc><priority>0.9</priority></url>
  <url><loc>https://example.com/products/{slug}/</loc>
    <image:image>...</image:image>
  </url>
</urlset>
```

### Local Business
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <url><loc>https://example.com/</loc><priority>1.0</priority></url>
  <url><loc>https://example.com/services/</loc><priority>0.8</priority></url>
  <url><loc>https://example.com/locations/{city}/</loc><priority>0.7</priority></url>
</urlset>
```

## Sitemap Generation Rules

- **Priority 1.0:** Homepage only
- **Priority 0.8-0.9:** Top-level pages (features, pricing, about)
- **Priority 0.6-0.7:** Blog posts, category pages
- **Priority 0.5:** Product pages, individual posts
- **Priority 0.3-0.4:** Archive, tag pages (optional)
- **Noindex pages:** Never include
- **Blocked by robots.txt:** Never include
- **4xx/5xx URLs:** Never include
- **lastmod:** Always include (helps Google prioritize recrawling)

## Sitemap Analysis Output

```
# XML Sitemap Analysis — {domain}

## Sitemap Details
- Location: {url}
- Total URLs: {count}
- Lastmod dates: {present}/missing
- changefreq specified: Yes/No
- Priority specified: Yes/No

## Quality Gate Results
| Gate | Status |
|------|--------|
| Valid XML | ✅/❌ |
| HTTPS only | ✅/❌ |
| No dead URLs | ✅/❌ |
| Size under limit | ✅/❌ |
| lastmod dates | ✅/❌ |

## Recommendations
{recommendations}

## Sitemap Generation
{generated_sitemap_xml}
```
