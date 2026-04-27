---
name: seo-backlinks
description: >
  Backlink profile analysis: referring domains, anchor text distribution, toxic
  link detection, and competitor gap analysis. Works with free APIs (Moz, Bing
  Webmaster, Common Crawl) and DataForSEO extension. Use when user says backlinks,
  link profile, referring domains, anchor text, toxic links, link gap, link building,
  disavow, or backlink audit.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
  compatibility: "Free: Common Crawl + verification always. Optional: Moz API, Bing Webmaster (free signup). Premium: DataForSEO."
---

# Backlink Profile Analysis

## Source Detection

Detect available data sources before analysis:

1. **DataForSEO MCP** (premium): Check if `dataforseo_backlinks_summary` tool available
2. **Moz API** (free signup): `python3 /workspace/claw-seo/scripts/backlinks_auth.py --check moz --json`
3. **Bing Webmaster** (free signup): `python3 /workspace/claw-seo/scripts/backlinks_auth.py --check bing --json`
4. **Common Crawl** (always): Domain-level graph with PageRank
5. **Verification Crawler** (always): Checks if known backlinks still exist

Run `python3 /workspace/claw-seo/scripts/backlinks_auth.py --check --json` to detect all sources at once.

If no sources beyond always-available tier: produce report using Common Crawl domain metrics, then suggest running `/seo backlinks setup`.

## Quick Reference

| Command | Purpose |
|---------|---------|
| `backlinks <url>` | Full backlink profile analysis |
| `backlinks gap <url1> <url2>` | Competitor backlink gap analysis |
| `backlinks toxic <url>` | Toxic link detection + disavow recommendations |
| `backlinks new <url>` | New and lost backlinks |
| `backlinks verify <url> --links <file>` | Verify known backlinks still exist |
| `backlinks setup` | Show setup instructions for free backlink APIs |

## Analysis Framework (7 Sections)

### 1. Profile Overview

| Metric | Good | Warning | Critical |
|--------|------|---------|----------|
| Referring domains | >100 | 20-100 | <20 |
| Follow ratio | >60% | 40-60% | <40% |
| Domain diversity | No single domain >5% | 1 domain >10% | 1 domain >25% |
| Trend | Growing/stable | Slow decline | Rapid decline |

**Data sources (in preference order):**
- DataForSEO: `dataforseo_backlinks_summary`
- Moz: `python3 /workspace/claw-seo/scripts/moz_api.py metrics <url> --json`
- Common Crawl: `python3 /workspace/claw-seo/scripts/commoncrawl_graph.py <domain> --json`

### 2. Anchor Text Distribution

**Healthy benchmarks:**

| Anchor Type | Target | Over-Optimization Signal |
|-------------|--------|--------------------------|
| Branded (company/domain name) | 30-50% | <15% |
| URL/naked link | 15-25% | N/A |
| Generic ("click here", "learn more") | 10-20% | N/A |
| Exact match keyword | 3-10% | >15% |
| Partial match keyword | 5-15% | >25% |
| Long-tail / natural | 5-15% | N/A |

**Flag if exact-match anchors exceed 15%** — Google Penguin risk signal.

### 3. Referring Domain Quality

Analyze:
- **TLD distribution**: .edu, .gov, .org = high authority. Excessive .xyz, .info = low quality
- **Country distribution**: 80%+ from irrelevant countries = PBN signal
- **Domain rank distribution**: Healthy profiles have links from all authority tiers
- **Follow/nofollow per domain**: Sites that only nofollow = limited SEO value

### 4. Toxic Link Detection

**Toxic signals:**
- Links from link farms or PBNs
- Exact-match anchor text from unrelated sites
- Links from foreign language sites with irrelevant content
- Over-optimized anchor text from low-authority domains
- Sudden spikes in new links (unnatural pattern)

**Disavow recommendations:**
- Identify domains with 50%+ exact-match keyword anchors from unrelated sites
- Flag .xyz, .info, .click, .loan domains with DA < 20
- Flag links from sites with zero organic search presence
- Document disavow file additions for Google Search Console

### 5. New & Lost Links (DataForSEO only)

Track growth/decline:
- New referring domains (last 30 days)
- Lost referring domains
- Link velocity trend

### 6. Competitor Gap Analysis

Compare your profile to competitors:
- Which referring domains do competitors have that you don't?
- What anchor text patterns work for competitors?
- Gap = link building opportunities

### 7. Link Velocity Analysis

- Natural link velocity: gradual growth
- Spikes: potential unnatural linking patterns
- Decline: competitor overtook you or lost links

## Scripts Available

```bash
# Detect all available sources
python3 /workspace/claw-seo/scripts/backlinks_auth.py --check --json

# Moz metrics
python3 /workspace/claw-seo/scripts/moz_api.py metrics <domain> --json

# Common Crawl domain graph
python3 /workspace/claw-seo/scripts/commoncrawl_graph.py <domain> --json

# Verify known backlinks still exist
python3 /workspace/claw-seo/scripts/verify_backlinks.py <url> --links <file>

# Bing Webmaster links
python3 /workspace/claw-seo/scripts/bing_webmaster.py links <url> --json
```

## Output Format

```
# Backlink Profile Analysis — {domain}

## Profile Overview
| Metric | Value | Assessment |
|--------|-------|------------|
| Total backlinks | {n} | ✅/⚠️/❌ |
| Referring domains | {n} | ✅/⚠️/❌ |
| Follow ratio | {pct} | ✅/⚠️/❌ |
| Domain diversity | {score} | ✅/⚠️/❌ |
| Trend | {trend} | ✅/⚠️/❌ |

## Anchor Text Distribution
| Type | Actual | Target | Status |
|------|--------|--------|--------|
| Branded | 35% | 30-50% | ✅ |
| Exact match | 18% | 3-10% | ⚠️ |

## Top Referring Domains
{domain_list}

## Toxic Links Flagged
{toxic_links}

## Competitor Gap
{competitor_gap_opportunities}

## Recommendations
{link_building_recommendations}
```
