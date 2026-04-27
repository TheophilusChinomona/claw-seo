---
name: seo-schema
description: >
  Schema.org structured data detection, validation, and generation. Supports JSON-LD
  (preferred), Microdata, and RDFa. Use when user says schema, structured data,
  JSON-LD, schema markup, or rich results.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Schema.org Markup Analysis

## Detection

1. Parse HTML for all three formats:
   - **JSON-LD** (preferred) — `<script type="application/ld+json">`
   - **Microdata** — `itemscope itemprop` attributes
   - **RDFa** — `typeof resource` attributes

2. Validate each schema against Google's supported types

3. Check for:
   - Self-referencing canonical + schema alignment
   - Conflicting noindex + schema
   - Deprecated schema types

## Schema Types by Page Type

| Page Type | Recommended Schema |
|-----------|-------------------|
| Homepage | Organization, WebSite, SearchAction |
| Blog post | Article, BlogPosting, Author, DatePublished |
| Product page | Product, Offer, AggregateRating |
| FAQ page | Question + answer pairs (gov/health only) |
| About page | Organization, Person |
| Contact page | Organization, Place, PostalAddress |
| Local business | LocalBusiness, Restaurant, etc. |
| Event | Event, EventVenue |
| Video | VideoObject, Clip |
| Recipe | Recipe with CookTime, Nutrition |

## Deprecated Schema Types

| Type | Deprecated |替代 |
|------|-----------|-----|
| HowTo | Sept 2023 | FAQPage or step-by-step Article |
| FAQPage | Aug 2023 | Restricted to gov/health sites |
| SpecialAnnouncement | July 2025 | Event or NewsArticle |

**Commercial sites with FAQPage:** Flag as Info priority (not Critical), noting AI/LLM citation benefit. Do NOT recommend adding new FAQPage for Google rich results.

## Schema Validation Checklist

- [ ] JSON-LD is valid JSON (use json.loads() to verify)
- [ ] @type matches page content
- [ ] Required properties present for @type
- [ ] URLs are absolute and valid
- [ ] Images have width/height attributes
- [ ] Self-referencing sameAs links
- [ ] No deprecated types used
- [ ] No duplicate schema for same entity

## Generation Templates

Use `schema/templates.json` for ready-to-use JSON-LD snippets:

```json
{
  "Organization": {
    "@context": "https://schema.org",
    "@type": "Organization",
    "name": "...",
    "url": "...",
    "logo": "...",
    "sameAs": ["...", "..."]
  },
  "WebSite": {
    "@context": "https://schema.org",
    "@type": "WebSite",
    "name": "...",
    "url": "...",
    "potentialAction": {
      "@type": "SearchAction",
      "target": "...{search_term_string}",
      "query-input": "required name=search_term_string"
    }
  }
}
```

## Additional Schema Types (v1.9.0+)

For video content:
- **VideoObject** — Video page markup with thumbnails, duration, upload date
- **BroadcastEvent** — LIVE badge support for live streaming
- **Clip** — Key moments/chapters within videos
- **SeekToAction** — Enable seek functionality in video rich results
- **SoftwareSourceCode** — Open source and code repository pages

## Output Format

```
# Schema.org Markup Analysis — {domain}

## Detected Schemas
| Type | Format | Status |
|------|--------|--------|
| Organization | JSON-LD | ✅ Valid |
| Article | Microdata | ⚠️ Missing required fields |

## Schema Opportunities
{missing_opportunities}

## Deprecation Warnings
{deprecated_schemas}

## Generated Schema
```json
{generated_schema}
```

## Recommendations
{recommendations}
```
