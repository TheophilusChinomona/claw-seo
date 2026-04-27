---
name: seo-hreflang
description: >
  Hreflang and international SEO audit, validation, and generation. Detects
  common mistakes, validates language/region codes, and generates correct hreflang
  implementations for HTML, HTTP headers, and XML sitemap. Use when user says
  hreflang, i18n SEO, international SEO, multi-language, multi-region, or language tags.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Hreflang & International SEO

Validate existing hreflang implementations or generate correct hreflang tags for multi-language and multi-region sites.

## Validation Checks

### 1. Self-Referencing Tags
- Every page must include an hreflang tag pointing to itself
- The self-referencing URL must exactly match the page's canonical URL
- Missing self-referencing tags cause Google to ignore the entire hreflang set

### 2. Return Tags
- If page A links to page B with hreflang, page B must link back to page A
- Every hreflang relationship must be bidirectional (A→B and B→A)
- Missing return tags invalidate the hreflang signal for both pages

### 3. x-default Tag
- Required: designates the fallback page for unmatched languages/regions
- Typically points to the language selector page or English version
- Only one x-default per set of alternates
- Must also have return tags from all other language versions

### 4. Language Code Validation
- Must use ISO 639-1 two-letter codes (e.g., `en`, `fr`, `de`, `ja`)
- Common errors:
  - `eng` instead of `en` (ISO 639-2, not valid for hreflang)
  - `jp` instead of `ja` (incorrect code for Japanese)
  - `zh` without region qualifier (ambiguous; use `zh-Hans` or `zh-Hant`)

### 5. Region Code Validation
- Optional region qualifier uses ISO 3166-1 Alpha-2 (e.g., `en-US`, `en-GB`, `pt-BR`)
- Format: `language-REGION` (lowercase language, uppercase region)
- Common errors:
  - `en-uk` instead of `en-GB` (UK is not a valid ISO 3166-1 code)
  - `es-LA` (Latin America is not a country; use specific countries)
  - Region without language prefix

### 6. Canonical URL Alignment
- Hreflang tags must only appear on canonical URLs
- If a page has `rel=canonical` pointing elsewhere, hreflang on that page is ignored
- The canonical URL and hreflang URL must match exactly

### 7. Protocol Consistency
- All URLs in an hreflang set must use the same protocol (HTTPS)
- Mixed HTTP/HTTPS in hreflang sets causes validation failures

### 8. Cross-Domain Support
- Hreflang works across different domains (e.g., example.com and example.de)
- Cross-domain hreflang requires return tags on both domains
- Verify both domains are verified in Google Search Console

## Common Mistakes

| Issue | Severity | Fix |
|-------|----------|-----|
| Missing self-referencing tag | Critical | Add hreflang pointing to same page URL |
| Missing return tags | Critical | Add matching return tags on all alternates |
| Missing x-default | High | Add x-default pointing to fallback page |
| Invalid language code (`eng`/`jp`) | High | Replace with ISO 639-1 code |
| Invalid region code (`en-uk`) | High | Replace with `en-GB` |
| Mixed HTTP/HTTPS | High | Standardize all to HTTPS |
| Non-canonical page in hreflang set | Medium | Remove or fix canonical first |

## Three Implementation Methods

### 1. HTML `<link>` Tags (in `<head>`)
```html
<link rel="alternate" hreflang="en" href="https://example.com/">
<link rel="alternate" hreflang="es" href="https://example.com/es/">
<link rel="alternate" hreflang="x-default" href="https://example.com/">
```

### 2. HTTP Headers (for PDFs, non-HTML)
```
Link: <https://example.com/>; rel="alternate"; hreflang="en"
Link: <https://example.com/es/>; rel="alternate"; hreflang="es"
```

### 3. XML Sitemap
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
        xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <url>
    <loc>https://example.com/</loc>
    <xhtml:link rel="alternate" hreflang="en" href="https://example.com/"/>
    <xhtml:link rel="alternate" hreflang="es" href="https://example.com/es/"/>
    <xhtml:link rel="alternate" hreflang="x-default" href="https://example.com/"/>
  </url>
</urlset>
```

## Cultural Profiles Reference

| Region | Language Code | Notes |
|--------|--------------|-------|
| US | `en-US` | Default for English |
| UK | `en-GB` | British English |
| Australia | `en-AU` | Australian English |
| Brazil | `pt-BR` | Brazilian Portuguese |
| Portugal | `pt-PT` | European Portuguese |
| Chinese Simplified | `zh-Hans` | Mainland China |
| Chinese Traditional | `zh-Hant` | Taiwan, Hong Kong |
| Spanish Spain | `es-ES` | European Spanish |
| Spanish LATAM | `es-MX` | Mexican Spanish |

## Output Format

```
# Hreflang / International SEO — {domain}

## Validation Results
| Check | Status | Details |
|-------|--------|---------|
| Self-referencing tags | ✅/❌ | {n}/{total} present |
| Return tags | ✅/❌ | {n} bidirectional pairs |
| x-default tag | ✅/❌ | Present/Missing |
| Language codes | ✅/❌ | {n} invalid codes found |
| Region codes | ✅/❌ | {n} invalid codes found |
| Canonical alignment | ✅/❌ | {n} conflicts |
| Protocol consistency | ✅/❌ | All HTTPS/Mixed |

## Issues Found
{issues}

## Generated Hreflang Tags
```html
{generated_html_tags}
```

## Sitemap Implementation
```xml
{generated_sitemap_xml}
```

## Recommendations
{recommendations}
```
