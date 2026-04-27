---
name: hermes-seo
description: >
  Comprehensive SEO analysis for any website or business type. Full site audits,
  single-page analysis, technical SEO (crawlability, indexability, Core Web Vitals),
  schema markup, content quality (E-E-A-T), sitemap analysis, and GEO for AI Overviews.
  Industry detection for SaaS, e-commerce, local, publishers, agencies.
  Triggers on: SEO, audit, schema, Core Web Vitals, sitemap, E-E-A-T, AI Overviews,
  technical SEO, content quality, page speed, structured data, backlink analysis.
user-invokable: true
argument-hint: "[command] [url]"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
  platform: hermes
  firecrawl: required
  upstream: https://github.com/AgriciDaniel/claude-seo
---

# SEO Agent — Universal SEO Analysis

**Platform:** Hermes Agent (forked from claude-seo v1.9.6)  
**Upstream:** [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo)  
**Branch:** `hermes-port` — syncs from upstream, stays current

## Capabilities

This SEO agent provides 23 specialized analysis capabilities across technical SEO,
content quality, schema markup, local SEO, AI search optimization, and more.

## Commands

| Command | What it does |
|---------|-------------|
| `audit <url>` | Full website audit with parallel subagent delegation |
| `page <url>` | Deep single-page analysis |
| `technical <url>` | Technical SEO audit (9 categories) |
| `content <url>` | E-E-A-T and content quality analysis |
| `schema <url>` | Schema.org detection, validation, generation |
| `sitemap <url>` | XML sitemap analysis or generation |
| `geo <url>` | AI Overviews / Generative Engine Optimization |
| `local <url>` | Local SEO (GBP, citations, reviews, map pack) |
| `maps [command]` | Maps intelligence (geo-grid, GBP audit, competitors) |
| `hreflang <url>` | Hreflang/i18n SEO audit and generation |
| `backlinks <url>` | Backlink profile analysis |
| `cluster <keyword>` | Semantic clustering and content architecture |
| `sxo <url>` | Search Experience Optimization |
| `drift baseline <url>` | Capture SEO baseline for change monitoring |
| `drift compare <url>` | Compare current state to stored baseline |
| `drift history <url>` | Show drift history over time |
| `ecommerce <url>` | E-commerce SEO analysis |

## Data Sources

| Source | What's Available | Cost |
|--------|----------------|------|
| Firecrawl (Nous subscription) | Site crawling, scraping, SEO audits | ✅ Included |
| Google PageSpeed Insights | Core Web Vitals (lab data) | ✅ Free |
| Google CrUX API | Core Web Vitals (field data) | ✅ Free |
| Google Search Console | Top queries, sitemap status | ✅ Free |
| Common Crawl | Backlink web graph | ✅ Free |
| Moz API | Domain Authority, Page Authority | ✅ Free tier |
| Bing Webmaster | Backlink competitor comparison | ✅ Free |
| DataForSEO MCP | Live SERP, keyword research | 💰 Paid |

## Orchestration Logic

When running `audit <url>`:
1. **Fetch homepage** — use `mcp_firecrawl_firecrawl_scrape` to get homepage content
2. **Detect business type** — analyze signals (see Industry Detection below)
3. **Crawl site** — use `mcp_firecrawl_firecrawl_crawl` for up to 500 pages
4. **Run parallel analyses** — spawn subagents for each SEO dimension
5. **Aggregate results** — combine into unified SEO Health Score (0-100)
6. **Generate report** — prioritized action plan (Critical → High → Medium → Low)

## Business Type Detection

Detect from homepage signals:

| Type | Signals |
|------|---------|
| **SaaS** | pricing page, /features, /integrations, /docs, "free trial", "sign up" |
| **Local Service** | phone number, address, service area, "serving [city]", Google Maps embed |
| **E-commerce** | /products, /collections, /cart, "add to cart", product schema |
| **Publisher** | /blog, /articles, /topics, article schema, author pages, publication dates |
| **Agency** | /case-studies, /portfolio, /industries, "our work", client logos |

Auto-suggest `local <url>` when local business signals detected.

## Quality Gates

- ⚠️ **WARNING** at 30+ location pages (enforce 60%+ unique content)
- 🛑 **HARD STOP** at 50+ location pages (require justification)
- Never recommend **HowTo schema** (deprecated Sept 2023)
- **FAQ schema** — restricted to gov/health sites; commercial sites flag as Info priority
- All Core Web Vitals use **INP** (not FID; FID removed Sept 2024)

## Sub-Skills Available

| Sub-Skill | Purpose |
|-----------|---------|
| `seo-audit` | Full site audit orchestrator |
| `seo-technical` | 9-category technical audit |
| `seo-content` | E-E-A-T, readability, thin content |
| `seo-schema` | Schema.org markup |
| `seo-page` | Single-page deep analysis |
| `seo-sitemap` | XML sitemap analysis/generation |
| `seo-geo` | AI search / GEO |
| `seo-local` | Local SEO |
| `seo-maps` | Maps intelligence |
| `seo-backlinks` | Backlink profile |
| `seo-cluster` | Semantic clustering |
| `seo-sxo` | Search experience |
| `seo-ecommerce` | E-commerce analysis |
| `seo-hreflang` | International SEO |
| `seo-images` | Image optimization |
| `seo-drift` | SEO change monitoring |

## Output Format

Every analysis returns:
1. **Health Score** (0-100) with category breakdown
2. **Findings** — categorized by severity (Critical / High / Medium / Low / Info)
3. **Prioritized Action Plan** — what to fix first with effort estimates
4. **Quick Wins** — items that take <1 hour but improve score meaningfully

## Running Scripts

The `claw-seo` scripts live in the upstream repo at `/workspace/claw-seo/scripts/`.
Run any script via `terminal()` with the full path:

```bash
python3 /workspace/claw-seo/scripts/fetch_page.py <url>
python3 /workspace/claw-seo/scripts/parse_html.py <url>
python3 /workspace/claw-seo/scripts/pagespeed_check.py <url> --json
```

## Community Footer

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Forked from [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo) — universal SEO skill for Claude Code. Ported to Hermes Agent on the `hermes-port` branch.
