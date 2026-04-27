---
name: seo-programmatic
description: >
  Programmatic SEO planning and analysis for pages generated at scale from data
  sources. Covers template engines, URL patterns, internal linking automation,
  thin content safeguards, and index bloat prevention. Use when user says
  programmatic SEO, pages at scale, dynamic pages, template pages,
  generated pages, or data-driven SEO.
user-invokable: true
argument-hint: "[url or plan]"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Programmatic SEO Analysis & Planning

Build and audit SEO pages generated at scale from structured data sources. Enforces quality gates to prevent thin content penalties and index bloat.

## Commands

| Command | Purpose |
|---------|---------|
| `programmatic audit <url>` | Audit an existing programmatic page setup |
| `programmatic plan <data-source>` | Plan a new programmatic SEO campaign |
| `programmatic template <url>` | Analyze template quality and uniqueness |
| `programmatic urls <data-source>` | Generate URL pattern from data structure |

## Workflow

### Step 1: Data Source Assessment

Evaluate the data powering programmatic pages:

**CSV/JSON files:**
- Row count, column uniqueness, missing values
- Are there enough unique attributes per row to generate distinct pages?
- Flag duplicate or near-duplicate records (>80% field overlap)

**API endpoints:**
- Response structure, data freshness, rate limits
- Is data publicly accessible or requires auth?
- Update frequency — stale data produces stale pages

**Database queries:**
- Record count, field completeness, update frequency
- Can queries be optimized for SEO page generation?

**Data Quality Checklist:**
- [ ] Each record has enough unique attributes for distinct content
- [ ] No duplicate records (enforce uniqueness on key fields)
- [ ] Data freshness verified (last updated date)
- [ ] NULL/missing values handled with conditional logic
- [ ] New records automatically picked up by generation process

### Step 2: Template Engine Planning

Design templates that produce unique, valuable pages:

**Variable injection points:**
- Title tag (unique per page)
- H1 (unique per page)
- Meta description (unique per page)
- Body sections (dynamic per page)
- Schema markup (dynamic per page)
- URL slug (derived from data)

**Content block types:**
| Type | Description | SEO Value |
|------|-------------|-----------|
| Static shared | Same across all pages | Low |
| Dynamic unique | Per-record data injection | High |
| Conditional | Show/hide based on data | Medium |
| Supplementary | Related items, tips, UGC | High |

**Template Review Checklist:**
- Each page must read as a standalone, valuable resource
- No "mad-libs" patterns (only swapping names/numbers in identical text)
- Dynamic sections must add genuine information
- Minimum 40% unique dynamic content per page
- At least one unique paragraph per page (not just variable substitution)

### Step 3: URL Pattern Strategy

**Common Patterns:**
| Pattern | Example | Use Case |
|---------|---------|---------|
| `/tools/[tool-name]` | `/tools/semrush-vs-ahrefs` | Tool directory |
| `/[city]/[service]` | `/new-york/plumber` | Location + service |
| `/integrations/[platform]` | `/integrations/slack` | Integration pages |
| `/glossary/[term]` | `/glossary/seo` | Definition pages |
| `/templates/[name]` | `/templates/resume-template` | Downloadable resources |
| `/[category]/[product]` | `/laptops/macbook-pro-16` | Product pages |

**URL Rules:**
- Lowercase, hyphenated slugs derived from data
- Logical hierarchy reflecting site architecture
- No duplicate slugs; enforce uniqueness at generation time
- Keep URLs under 100 characters
- No query parameters for primary content URLs
- Consistent trailing slash usage

### Step 4: Internal Linking Automation

**Hub/Spoke Model:**
- Category hub pages linking to individual programmatic pages
- Hub pages target high-volume head terms
- Spoke pages target long-tail variants

**Auto-linking rules:**
- Related items: Link to 3-5 related pages based on data attributes
- Breadcrumbs: Generate BreadcrumbList schema from URL hierarchy
- Cross-linking: Link between pages sharing attributes
- Anchor text: Descriptive and varied (avoid exact-match repetition)
- Link density: 3-5 internal links per 1,000 words

### Step 5: Thin Content Safeguards

**Quality Gates:**

| Metric | Threshold | Action |
|--------|-----------|--------|
| Pages without content review | 100+ | ⚠️ WARNING: require audit before publish |
| Pages without justification | 500+ | 🛑 HARD STOP: require explicit approval |
| Unique content per page | <40% | ❌ Flag as thin content (penalty risk) |
| Words per page (minimum) | <300 | ❌ Flag as thin content |
| Duplicate title tags | >5% | ❌ Flag for deduplication |

**Content enrichment triggers:**
- If base template produces <500 words: add 2+ supplementary sections
- If page has <2 unique paragraphs: inject FAQ, pros/cons, or case study
- If product has no description: exclude from generation or add placeholder

### Step 6: Index Bloat Prevention

**Crawl budget protection:**
- `noindex` on parameter-heavy URLs (`?sort=`, `?filter=`)
- Canonical tags pointing to primary version
- `rel="canonical"` on paginated series (`?page=2` → canonical to page 1)
- Submit XML sitemap only for indexable programmatic pages

**Generation staging:**
1. Generate to staging environment
2. Run thin content audit across all pages
3. Fix flagged pages before moving to production
4. Submit sitemap incrementally (not all at once)

## Schema for Programmatic Pages

### Article Schema (for blog-style programmatic pages)
```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[Dynamic from data]",
  "author": { "@type": "Organization", "name": "[Brand]" },
  "datePublished": "[Date]",
  "dateModified": "[Date]"
}
```

### BreadcrumbList Schema
```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [{
    "@type": "ListItem",
    "position": 1,
    "name": "[Category]",
    "item": "https://example.com/[category]"
  }, {
    "@type": "ListItem",
    "position": 2,
    "name": "[Page-specific title]",
    "item": "https://example.com/[full-url]"
  }]
}
```

## Output Format

```
# Programmatic SEO Audit — {domain or data-source}

## Data Source Assessment
| Metric | Value |
|--------|-------|
| Records | {count} |
| Unique fields | {count} |
| Missing values | {pct} |
| Duplicate risk | {assessment} |
| Freshness | {last_updated} |

## Template Analysis
| Page | Unique Content | Word Count | Quality Gate |
|------|----------------|-----------|-------------|
| {page1} | {pct} | {count} | ✅/❌ |
| {page2} | {pct} | {count} | ✅/❌ |

## URL Pattern
| Pattern | Example | Count |
|---------|---------|-------|
| /[category]/[item] | {example} | {n} |

## Thin Content Flags
- Pages flagged: {count}
- Pages requiring audit: {count}
- Hard stops triggered: {count}

## Internal Linking
- Hub pages: {count}
- Spoke pages: {count}
- Avg link density: {count}/1000 words

## Recommendations
{recommendations}
```
