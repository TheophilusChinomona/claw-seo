# claw-seo

SEO analysis suite for Hermes Agent — audits, technical SEO, content, schema, local, maps, backlinks, and more.

> Forked from [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo) and adapted for Hermes Agent with enhanced skills, Firecrawl-powered crawling, and free-tier-first data sources.

---

## Two Branches

| Branch | Purpose |
|--------|---------|
| `main` | Upstream [claude-seo](https://github.com/AgriciDaniel/claude-seo) — vanilla Claude CLI skills |
| `hermes-port` | **This repo's focus** — Hermes Agent skills, forked conventions, additional skills |

All hermes-specific work lives on `hermes-port`. Upstream updates merge into `main`, then rebase `hermes-port` on top.

---

## Quick Start

```bash
# Clone the hermes-port branch
git clone --branch hermes-port https://github.com/TheophilusChinomona/claw-seo.git ~/claw-seo

# Install skills to Hermes
cp -r ~/claw-seo/hermes-skills/* ~/.hermes/skills/

# Run a full site audit
/seo audit <url>
```

---

## Skills Inventory

**18 SEO skills** across all phases, installed to `~/.hermes/skills/`.

### Orchestrator
| Skill | Description |
|-------|-------------|
| `hermes-seo` | Main entry point. Routes to sub-skills by command. Run `/seo audit`, `/seo technical`, etc. |

### Phase 1 — Core Audits
| Skill | Description |
|-------|-------------|
| `seo-audit` | Full site audit — spawns parallel subagents across all audit categories |
| `seo-technical` | 9-category technical audit: CWV, INP, security, redirects, canonical, meta, robots, structured data, hreflang, sitemaps |
| `seo-content` | E-E-A-T signals, Flesch-Kincaid readability, thin content detection, internal links |
| `seo-schema` | JSON-LD detection, validation, and generation — 20+ schema types |
| `seo-page` | Single-page deep analysis — 30-point on-page checklist |
| `seo-sitemap` | XML sitemap validation and generation with industry templates |

### Phase 2 — Specialized Audits
| Skill | Description |
|-------|-------------|
| `seo-geo` | AI Overviews / GEO optimization — citability scoring, brand signals, AI crawler access |
| `seo-local` | Google Business Profile, NAP consistency, local citations, review signals, local schema |
| `seo-maps` | Geo-grid rank tracking, SoLV scoring, cross-platform NAP verification |
| `seo-backlinks` | Moz + Bing Webmaster + Common Crawl, anchor text analysis, toxic link detection |
| `seo-images` | Alt text, WebP/AVIF formats, srcset, lazy loading, CLS prevention |
| `seo-hreflang` | International SEO — x-default, return tags, language code validation |

### Phase 3 — Strategy & Content
| Skill | Description |
|-------|-------------|
| `seo-cluster` | SERP-overlap keyword clustering, hub-and-spoke architecture, content brief generation |
| `seo-sxo` | Search Experience Optimization — page-type mismatch detection, persona scoring, IST/SOLL wireframes |
| `seo-ecommerce` | Product schema, faceted navigation, canonical issues, thin content guards |

### Phase 4 — Advanced
| Skill | Description |
|-------|-------------|
| `seo-competitor-pages` | "X vs Y" comparison pages, alternatives pages, feature matrices, schema markup |
| `seo-programmatic` | Pages-at-scale planning — template engines, URL patterns, thin content safeguards, index bloat prevention |

---

## Commands Reference

Run any skill by invoking its command from Hermes:

```bash
/seo audit <url>           # Full site audit (parallel subagents)
/seo technical <url>       # Technical SEO audit
/seo content <url>         # Content + E-E-A-T analysis
/seo schema <url>          # Structured data audit
/seo page <url>            # Single-page analysis
/seo sitemap <url>         # Sitemap validation
/seo geo <url>             # AI Overviews / GEO optimization
/seo local <url>           # Local SEO (GBP, NAP, citations)
/seo maps <keyword>       # Geo-grid rank tracking
/seo backlinks <url>       # Backlink profile analysis
/seo images <url>          # Image optimization audit
/seo hreflang <url>        # International SEO validation
/seo cluster <keyword>     # Keyword clustering + content architecture
/seo sxo <url> [keyword]  # Search Experience Optimization
/seo ecommerce <url>      # E-commerce product page analysis
/seo competitor <url>      # Competitor comparison pages
/seo programmatic <url>    # Programmatic SEO planning
```

---

## Data Sources

Free tier first — no paid APIs required for core audits:

| Source | Capability | Cost |
|--------|-----------|------|
| Firecrawl MCP | Crawling, scraping, SERP analysis | Included (Nous subscription) |
| Google PageSpeed Insights | Core Web Vitals | Free |
| Google CrUX | Real user metrics | Free |
| Google Search Console | Search performance | Free |
| Common Crawl | Domain-level backlink graph | Always available |
| Moz API | Domain Authority, link metrics | Free tier available |
| Bing Webmaster | Link data | Free tier available |
| DataForSEO MCP | Advanced backlink + maps data | Premium |

---

## Reports

Client deliverables are saved to `reports/`.

```
reports/
└── REPORT-<client-domain>.md   ← client-ready audit reports
```

---

## Repository Structure

```
claw-seo/
├── hermes-skills/              ← Hermes Agent SEO skills (18 skills)
│   ├── hermes-seo/             ← orchestrator
│   ├── seo-audit/              ← full site audit
│   ├── seo-technical/           ← technical audit
│   ├── seo-content/            ← content analysis
│   ├── seo-schema/             ← structured data
│   ├── seo-page/               ← single-page audit
│   ├── seo-sitemap/            ← sitemap validation
│   ├── seo-geo/                ← AI Overviews / GEO
│   ├── seo-local/              ← local SEO
│   ├── seo-maps/               ← geo-grid rank tracking
│   ├── seo-backlinks/          ← backlink analysis
│   ├── seo-images/             ← image optimization
│   ├── seo-hreflang/           ← international SEO
│   ├── seo-cluster/            ← keyword clustering
│   ├── seo-sxo/                ← search experience optimization
│   ├── seo-ecommerce/         ← product page SEO
│   ├── seo-competitor-pages/   ← comparison pages
│   └── seo-programmatic/       ← programmatic SEO
├── reports/                     ← client deliverables
├── skills/                      ← upstream claude-seo (main branch)
├── scripts/                      ← Python utilities
├── AGENTS.md
├── CHANGELOG.md
├── CONTRIBUTING.md
└── CONTRIBUTORS.md
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Agent | Hermes Agent |
| Crawling | Firecrawl MCP (Nous subscription) |
| SEO Data | Google PSI, CrUX, GSC, Common Crawl, Moz, Bing |
| Skills Format | YAML frontmatter + Markdown (Hermes native) |
| Repo Hosting | GitHub (TheophilusChinomona/claw-seo) |

---

## Contributing

1. All new hermes skills go on `hermes-port` branch
2. Skills use YAML frontmatter format — see existing skills for structure
3. Upstream changes merge into `main`, then rebase `hermes-port`
4. Client reports go in `reports/` — never in `hermes-skills/`
5. Test new skills against a real site before committing

---

## Upstream

- **Upstream:** [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo) v1.9.6
- **Fork:** [TheophilusChinomona/claw-seo](https://github.com/TheophilusChinomona/claw-seo)
- Hermes port by Praxis

---

## License

MIT — same as upstream.
