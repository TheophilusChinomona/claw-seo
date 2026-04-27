---
name: seo-ecommerce
description: >
  E-commerce SEO analysis: Google Shopping visibility, Amazon marketplace
  intelligence, product schema validation, competitor pricing analysis, and
  marketplace keyword gaps. Combines on-page product SEO with marketplace data.
  Use when user says ecommerce SEO, product SEO, Google Shopping, marketplace SEO,
  product schema, Amazon SEO, product listings, shopping ads, or merchant SEO.
user-invokable: true
argument-hint: "<url or keyword>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  original_author: "Matej Marjanovic (Pro Hub Challenge)"
  version: "1.0.0"
  category: seo
  compatibility: "Enhanced with DataForSEO Merchant API (optional)"
---

# E-commerce SEO Analysis

Comprehensive product page optimization, marketplace intelligence, and competitive pricing analysis.

## Commands

| Command | Purpose | DataForSEO? |
|---------|---------|-------------|
| `ecommerce <url>` | Full e-commerce SEO analysis | Optional |
| `ecommerce products <keyword>` | Google Shopping competitive analysis | Required |
| `ecommerce gaps <domain>` | Keyword gap: organic vs Shopping visibility | Required |
| `ecommerce schema <url>` | Product schema validation and enhancement | No |

## 1. Product Page Analysis (No DataForSEO Needed)

### Product SEO Checklist

#### Title Tag
- [ ] Contains primary product keyword
- [ ] Includes brand name
- [ ] Under 60 characters
- [ ] Format: `[Product Name] - [Key Feature] | [Brand]`

#### Meta Description
- [ ] Contains product keyword + benefit
- [ ] Includes price or "from $XX"
- [ ] Call-to-action present
- [ ] Under 155 characters

#### Heading Structure
- [ ] Single H1 matching primary product name
- [ ] H2s for: Features, Specifications, Reviews, Related Products
- [ ] No duplicate H1 tags across product variants

#### Product Images
- [ ] Alt text includes product name + distinguishing feature
- [ ] File names descriptive (not `IMG_001.jpg`)
- [ ] WebP format served
- [ ] At least 3 images per product
- [ ] Image dimensions >= 800px for Google Shopping
- [ ] Lazy loading on below-fold images only

#### Internal Linking
- [ ] Breadcrumb: Home > Category > Subcategory > Product
- [ ] Related products section (cross-sell / upsell)
- [ ] Link back to category page with keyword-rich anchor

### Thin Content Guardrails

| Page Count | Action |
|------------|--------|
| 1-50 | Acceptable if each page is unique |
| 50-100 | 30% of pages must have unique content |
| 100+ | **HARD STOP** — Require product schema + category uniqueness |

## 2. Product Schema Validation

Required fields for `Product` schema:

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Product Name",
  "description": "...",
  "sku": "SKU-123",
  "gtin13": "1234567890123",
  "brand": {
    "@type": "Brand",
    "name": "Brand Name"
  },
  "image": ["https://..."],
  "offers": {
    "@type": "Offer",
    "price": "99.99",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock",
    "seller": {
      "@type": "Organization",
      "name": "Seller Name"
    }
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "reviewCount": "128"
  }
}
```

### Common Product Schema Mistakes

| Issue | Severity | Fix |
|-------|----------|-----|
| Missing `availability` | Critical | Add to Offer |
| Wrong currency format | High | Use ISO 4217 (USD, EUR, GBP) |
| Price without currency | High | Always include `priceCurrency` |
| Missing `name` or `description` | Critical | Required fields |
| `image` as string instead of array | Medium | Use array for multiple images |

## 3. Google Shopping Analysis (DataForSEO Required)

**Check for:**
- Product visibility in Google Shopping results
- Price competitiveness vs competitors
- Title optimization (first 150 characters most important)
- Image eligibility (>= 250x250px, no promotional overlays)
- Merchant center issues preventing visibility

## 4. Amazon SEO (if marketplace competitor)

**Keyword research for Amazon:**
- Use Amazon autocomplete (search suggestions)
- Backend keywords (hidden search terms)
- A+ Content for brand registered sellers
- Review velocity impact on rank

## 5. Faceted Navigation & Canonicals

**E-commerce common issues:**

1. **Faceted navigation crawl bloat**
   - Infinite URL space from filter combinations
   - Solution: `noindex` on filtered URLs, proper canonical to parent category

2. **Variant pages**
   - Size/color variants should canonical to main product page
   - Use `rel="alternate" media="only screen and (resolution: 2dppx)"` for responsive images

3. **Pagination**
   - Paginated series: `rel="prev"` / `rel="next"` pointing to sorted views
   - Or: `view-all` page with canonical to page 1

## Output Format

```
# E-commerce SEO Analysis — {domain}

## Product Page SEO
| Element | Status | Recommendation |
|---------|--------|----------------|
| Title tag | ✅/❌ | {reco} |
| Meta description | ✅/❌ | {reco} |
| H1 | ✅/❌ | {reco} |
| Image alt text | ✅/❌ | {reco} |
| Image formats | ✅/❌ | {reco} |
| Internal links | ✅/❌ | {reco} |
| Breadcrumbs | ✅/❌ | {reco} |

## Product Schema: {score}/100
- Required fields present: {n}/{total}
- Optional fields present: {n}/{total}
- Errors found: {count}

## Thin Content
- Product pages analyzed: {count}
- Thin content flagged: {count}

## Faceted Navigation
| Issue | Status |
|-------|--------|
| Filter bloat | ✅/❌ Fixed |
| Variant canonicals | ✅/❌ Fixed |
| Pagination handled | ✅/❌ Fixed |

## Recommendations
{recommendations}
```
