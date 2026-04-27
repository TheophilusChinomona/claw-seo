---
name: seo-audit
description: >
  Full website SEO audit with parallel subagent delegation. Crawls up to 500 pages,
  detects business type, delegates to 8+ SEO specialists, generates health score (0-100).
  Use when user says audit, full SEO check, analyze my site, or website health check.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Full Website SEO Audit

## Process

1. **Fetch homepage** — use `mcp_firecrawl_firecrawl_scrape` to get homepage HTML
2. **Detect business type** — analyze homepage signals (SaaS / local / e-commerce / publisher / agency)
3. **Crawl site** — use `mcp_firecrawl_firecrawl_crawl` for up to 500 pages
4. **Run parallel analyses** via `delegate_task`:
   - `seo-technical` — robots.txt, sitemaps, canonicals, Core Web Vitals, security headers
   - `seo-content` — E-E-A-T, readability, thin content, AI citation readiness
   - `seo-schema` — detection, validation, generation recommendations
   - `seo-sitemap` — structure analysis, quality gates, missing pages
   - `seo-geo` — AI crawler access, llms.txt, citability
   - `seo-sxo` — page-type mismatch, user stories, persona scoring
5. **Conditional additions**:
   - `seo-local` — if local business signals detected
   - `seo-ecommerce` — if e-commerce signals detected
   - `seo-backlinks` — if backlink APIs available
6. **Score** — aggregate into SEO Health Score (0-100)
7. **Report** — generate prioritized action plan

## Crawl Configuration

```
Max pages: 500
Respect robots.txt: Yes
Follow redirects: Yes (max 3 hops)
Timeout per page: 30 seconds
```

## Scoring Weights

| Category | Weight |
|----------|--------|
| Technical SEO | 22% |
| Content Quality | 23% |
| On-Page SEO | 20% |
| Schema / Structured Data | 10% |
| Performance (CWV) | 10% |
| AI Search Readiness | 10% |
| Images | 5% |

## Output Structure

### Executive Summary
- Overall SEO Health Score (0-100) with grade (A/B/C/D/F)
- Business type detected
- Top 3 critical issues
- Top 3 quick wins

### Technical SEO
- Crawlability issues
- Indexability problems
- Security concerns
- Core Web Vitals status

### Content Quality
- E-E-A-T assessment
- Readability issues
- Thin content pages

### Schema / Structured Data
- Detected markup
- Missing opportunities
- Deprecation warnings

### Action Plan
- Critical (fix immediately)
- High (fix within 1 week)
- Medium (fix within 1 month)
- Low (nice to have)

## Firecrawl Integration

```python
# Crawl the site first
mcp_firecrawl_firecrawl_crawl(url="https://target.com/*", limit=500)

# Then run targeted scrapes for specific pages
mcp_firecrawl_firecrawl_scrape(url="https://target.com/about", formats=["markdown"])
```

## Audit Report Template

```
# SEO Audit Report — {domain}

**Date:** {date}  
**URLs Analyzed:** {count}  
**Business Type:** {type}  
**SEO Health Score:** {score}/100 ({grade})

## Executive Summary
{summary}

## Detailed Findings
{detailed_findings}

## Prioritized Action Plan
{action_plan}

## Quick Wins (Under 1 Hour)
{quick_wins}
```
