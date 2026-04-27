---
name: seo-competitor-pages
description: >
  Generate SEO-optimized competitor comparison and alternatives pages. Covers
  "X vs Y" layouts, "alternatives to X" pages, feature matrices, schema markup,
  and conversion optimization. Use when user says comparison page, vs page,
  alternatives page, competitor comparison, X vs Y, versus, compare competitors,
  or alternative to.
user-invokable: true
argument-hint: "[url or generate] [competitor]"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Competitor Comparison & Alternatives Pages

Create high-converting comparison and alternatives pages that target competitive intent keywords.

## Page Types

### 1. "X vs Y" Comparison Pages
- Direct head-to-head comparison between two products/services
- Balanced feature-by-feature analysis
- Clear verdict or recommendation with justification
- Target keyword: `[Product A] vs [Product B]`

### 2. "Alternatives to X" Pages
- List of alternatives to a specific product/service
- Each alternative with brief summary, pros/cons, best-for use case
- Target keyword: `[Product] alternatives`, `best alternatives to [Product]`

### 3. "Best [Category] Tools" Roundup Pages
- Curated list of top tools/services in a category
- Ranking criteria clearly stated
- Target keyword: `best [category] tools [year]`, `top [category] software`

### 4. Comparison Table Pages
- Feature matrix with multiple products in columns
- Sortable/filterable if interactive
- Target keyword: `[category] comparison`, `[category] comparison chart`

## Workflow

### Step 1: Analyze Competing Pages

Use Firecrawl to scrape and analyze existing comparison pages for the target keyword:

1. Search: `"[Product A] vs [Product B]"` via web search
2. Scrape top 3 ranking pages via Firecrawl
3. Extract: page structure, word count, schema types, heading hierarchy, table format
4. Identify content gaps in existing comparisons

### Step 2: Identify Your Product's Differentiators

Before writing comparison content, clarify:
- Which features does your product have that competitors don't?
- Where are you genuinely weaker?
- What's your price positioning vs competitors?
- Who is your ideal user (best-for use case)?

**Honest, balanced comparisons rank better** — Google's helpful content system rewards pages that accurately represent alternatives.

### Step 3: Structure the Page

**"X vs Y" Layout:**
```
## [Product A] Overview
{name, description, key use case, pricing}

## [Product B] Overview
{name, description, key use case, pricing}

## Feature Comparison
| Feature         | [Product A] | [Product B] |
|----------------|:------------:|:------------:|
| Feature 1      | ✅           | ✅           |
| Feature 2       | ⚠️ Partial   | ✅           |
| Feature 3       | ✅           | ❌           |
| Pricing (from) | $X/mo        | $Y/mo        |
| Free Tier      | ✅           | ❌           |

## [Product A] Pros
- ...

## [Product B] Pros
- ...

## Verdict
{balanced recommendation based on use case}
```

**"Alternatives" Layout:**
```
## Best [Product] Alternatives
{brief intro}

## [Alternative 1]
- **Best for:** {use case}
- **Pros:** ...
- **Cons:** ...
- **Pricing:** ...
- **Link:** {affiliate or direct}

## [Alternative 2]
- ...

## How to Choose
{decision matrix based on priorities}
```

## Feature Matrix Generation

```
| Feature          | Your Product | Competitor A | Competitor B |
|------------------|:------------:|:------------:|:------------:|
| Feature 1        | ✅           | ✅           | ❌           |
| Feature 2        | ✅           | ⚠️ Partial   | ✅           |
| Feature 3        | ✅           | ❌           | ❌           |
| Pricing (from)   | $X/mo        | $Y/mo        | $Z/mo        |
| Free Tier        | ✅           | ❌           | ✅           |
| Trial Period     | 14 days      | 7 days       | 30 days      |
| Support          | 24/7 Chat    | Email only   | 24/7 Phone   |
```

## Data Accuracy Requirements

- All feature claims must be verifiable from public sources
- Pricing must be current (include "as of [date]" note)
- Update frequency: review quarterly or when competitors ship major changes
- Link to source for each competitor data point where possible

## Schema Markup

### Product Schema with AggregateRating
```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "[Product Name]",
  "description": "[Product Description]",
  "brand": {
    "@type": "Brand",
    "name": "[Brand Name]"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "[Rating]",
    "reviewCount": "[Count]"
  }
}
```

### FAQ Schema for Comparison Pages
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "Which is better, [Product A] or [Product B]?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "[Balanced answer based on use case]"
    }
  }]
}
```

### ItemList for Alternatives/Roundup Pages
```json
{
  "@context": "https://schema.org",
  "@type": "ItemList",
  "itemListElement": [{
    "@type": "ListItem",
    "position": 1,
    "item": {
      "@type": "Product",
      "name": "[Product Name]",
      "url": "https://example.com/review/[product]"
    }
  }]
}
```

## Thin Content Guardrails

| Page Type | Minimum Content |
|-----------|----------------|
| "X vs Y" | 1,500 words (balanced analysis) |
| "Alternatives" | 800 words base + 300 words per alternative |
| "Best [Category]" | 2,000 words (50+ items) or 1,200 words (10 items) |
| Feature matrix only | Add 500-word intro + 100-word per-item summaries |

**WARNING:** Pages with <400 words will likely be flagged as thin content.

## Output Format

```
# Competitor Comparison — {[Product] vs [Competitor]}

## SERP Analysis
- Top ranking pages: {count}
- Average word count: {count}
- Common schema types: {list}
- Content gaps identified: {list}

## Comparison Structure
- Page type: {type}
- Target keyword: {keyword}
- Word count target: ~{count}

## Feature Matrix
{matrix}

## Schema Markup
- Product schema: ✅/❌
- FAQ schema: ✅/❌
- ItemList: ✅/❌

## Content Recommendations
{recommendations}
```
