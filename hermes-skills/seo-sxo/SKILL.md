---
name: seo-sxo
description: >
  Search Experience Optimization: reads Google SERPs backwards to detect page-type
  mismatches, derives user stories from search intent signals, and scores pages from
  multiple persona perspectives. Identifies why well-optimized pages fail to rank by
  analyzing what Google rewards for each keyword. Use when user says SXO, search
  experience, page type mismatch, SERP analysis, user story, persona scoring,
  intent mismatch, or wireframe.
user-invokable: true
argument-hint: "<url> [keyword]"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  original_author: "Florian Schmitz (Pro Hub Challenge)"
  version: "1.0.0"
  category: seo
---

# Search Experience Optimization (SXO)

SXO bridges the gap between SEO (what Google rewards) and UX (what users need). A page can score 95/100 on technical SEO and still fail to rank because it is the **wrong page type** for the keyword.

## Core Insight

If Google shows 8 product pages and 2 comparison pages for your keyword, your blog post will never break through — no matter how well-optimized it is.

## Key Statistics

| Stat | Value |
|------|-------|
| SEO-only pages that still don't rank | ~40% |
| SXO mismatch as root cause | High correlation |
| Pages improved after SXO fix | Significant rank gains |

## Commands

| Command | Purpose |
|---------|---------|
| `sxo <url>` | Full SXO analysis (auto-detect keyword from page) |
| `sxo <url> <keyword>` | Full SXO analysis for a specific keyword |
| `sxo wireframe <url>` | Generate IST/SOLL wireframe with placeholders |

## Execution Pipeline

### Step 1: Target Acquisition

1. Fetch target URL via Firecrawl scrape
2. Extract: title, H1, meta description, headings hierarchy, word count, schema markup, CTAs, media elements
3. If no keyword provided, extract primary keyword from title + H1 overlap
4. Validate keyword is non-empty before proceeding

### Step 2: SERP Backwards Analysis

For the target keyword, analyze the top 10 organic results:

**For each result, record:**
- Page type (classify using taxonomy below)
- Content format (long-form, listicle, how-to, comparison, tool, video)
- Word count estimate (from snippet + page structure)
- Schema types present (ratings, FAQ, HowTo)
- Media signals (video carousel, image pack)

**Record SERP features:**
- Featured snippet (paragraph / list / table / video)
- People Also Ask (extract all visible questions)
- Ads (top and bottom — count and analyze themes)
- Related searches
- Knowledge panel / local pack / shopping results
- AI Overview presence and source types

### Step 3: Page-Type Mismatch Detection

Compare target page type against SERP consensus.

**SERP Consensus thresholds:**
- >60% = Strong consensus (Google clearly prefers one type)
- 40-60% = Mixed (multiple types compete)
- <40% = Fragmented (no clear winner)

**If mismatch detected:**
- Page type mismatch = Hard STOP. Recommend rebuilding or choosing a different keyword
- Content depth gap = Address with additional sections
- Format mismatch = Restructure to match winning format

### Step 4: Persona-Based Scoring

Score the page from multiple user perspective angles:

| Persona | What They Need | Score Weight |
|--------|---------------|-------------|
| **Researcher** | Deep information, data, citations | 20% |
| **Buyer** | Price, specs, reviews, comparison | 20% |
| **Navigator** | Clear CTA, easy path to purchase | 15% |
| **Troubleshooter** | FAQ, how-to, problem solutions | 15% |
| **Explorer** | Visual content, videos, examples | 15% |
| **Validator** | Social proof, reviews, trust signals | 15% |

### Step 5: IST/SOLL Wireframe

Generate a wireframe showing:
- **IST** (Ist-Zustand = Current State): What the page currently looks like
- **SOLL** (Soll-Zustand = Target State): What it should look like after SXO fixes

```
## IST Wireframe — {url}
┌─────────────────────────────────────────────┐
│ H1: {title}                                │
│ Meta: {description}                        │
├─────────────────────────────────────────────┤
│ [Content blocks from SERP analysis]         │
│ Current page type: {type}                  │
│ Current format: {format}                   │
└─────────────────────────────────────────────┘

## SOLL Wireframe — {keyword}
┌─────────────────────────────────────────────┐
│ H1: [SERP-informed title targeting kw]     │
│ Meta: [CTR-optimized description]           │
├─────────────────────────────────────────────┤
│ [Required content blocks per SERP consensus]│
│ Target page type: {type}                   │
│ Target format: {format}                     │
│ Media signals: {requirements}               │
└─────────────────────────────────────────────┘
```

## Page Type Taxonomy

| Type | Description | Google Expectation |
|------|-------------|-------------------|
| Blog Post | Editorial, opinion, news | Informational |
| Product Page | Price, specs, buy button | Transactional |
| Category Page | Listing of products/articles | Browse |
| Comparison | Side-by-side analysis | Research |
| How-To Guide | Step-by-step instructions | Informational |
| Tool/App | Interactive functionality | Utility |
| Landing Page | Conversion-focused | Commercial |
| Home Page | Portal/navigation | Brand |

## Output Format

```
# SXO Analysis — {domain}

## Target Keyword: {keyword}

## SERP Analysis: {keyword}
- Results analyzed: 10
- SERP consensus: {strong/mixed/fragmented} ({pct}% dominant type)
- Dominant page type: {type} ({pct}%)
- Dominant format: {format}
- Word count expectation: ~{count} words
- Media expectation: {images/video/both}

## Page-Type Mismatch
| Check | Status |
|-------|--------|
| Target type vs SERP consensus | ✅ Match / ❌ Mismatch |
| Content depth | ✅ Sufficient / ⚠️ Gap |
| Format alignment | ✅ Match / ❌ Mismatch |

## Persona Scores: {domain}
| Persona | Score | Notes |
|--------|-------|-------|
| Researcher | {n}/100 | {notes} |
| Buyer | {n}/100 | {notes} |
| Navigator | {n}/100 | {notes} |
| Troubleshooter | {n}/100 | {notes} |
| Explorer | {n}/100 | {notes} |
| Validator | {n}/100 | {notes} |

## Key Issues Found
{issues}

## Recommendations
{recommendations}
```
