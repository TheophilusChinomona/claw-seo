---
name: seo-cluster
description: >
  SERP-based semantic topic clustering for content architecture planning. Groups
  keywords by actual Google SERP overlap (not text similarity), designs hub-and-spoke
  content clusters with internal link matrices, and generates visualizations. Use when
  user says topic cluster, content cluster, semantic clustering, pillar page,
  hub and spoke, content architecture, keyword grouping, or cluster plan.
user-invokable: true
argument-hint: "<seed-keyword or url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  original_author: "Lutfiya Miller (Pro Hub Challenge Winner)"
  version: "1.0.0"
  category: seo
---

# Semantic Topic Clustering

SERP-overlap-driven keyword clustering for content architecture. Groups keywords by how Google actually ranks them (shared top-10 results), not by text similarity. Designs hub-and-spoke content clusters with internal link matrices.

## Quick Reference

| Command | What it does |
|---------|-------------|
| `cluster plan <seed-keyword>` | Full workflow: expand, cluster, architect, visualize |
| `cluster execute` | Execute plan: create content or output briefs |
| `cluster map` | Regenerate the interactive cluster visualization |

## Workflow

### Step 1: Seed Keyword Expansion

Expand the seed keyword into 30-50 variants using web search:

1. **Related searches** — Extract "related searches" and "people also search for"
2. **People Also Ask (PAA)** — Extract all PAA questions from SERP results
3. **Long-tail modifiers** — Append: "best", "how to", "vs", "for beginners", "tools", "examples", "guide", "mistakes", "checklist"
4. **Question mining** — Generate who/what/when/where/why/how variants
5. **Intent modifiers** — Add commercial modifiers: "pricing", "review", "alternative", "comparison", "top"

**Target: 30-50 unique keyword variants.**

### Step 2: SERP Overlap Clustering

**Core differentiator.** This groups keywords by actual Google ranking behavior.

**Thresholds:**

| Shared Results | Relationship | Action |
|---------------|-------------|--------|
| 7-10 | Same post | Merge into single target page |
| 4-6 | Same cluster | Group under same spoke cluster |
| 2-3 | Interlink | Place in adjacent clusters, add cross-links |
| 0-1 | Separate | Assign to different clusters or exclude |

**Optimization:** With 40 keywords, full pairwise = 780 comparisons. Instead:
- Pre-group by intent (4 groups of ~10 = 180 comparisons)
- Only cross-check group boundary keywords
- Skip pairs where both are long-tail variants of same head term

### Step 3: Cluster Architecture

Build the hub-and-spoke model:

**Hub Page (Pillar)**
- Targets the seed keyword (highest search volume)
- Comprehensive, 3,000+ word guide
- Links to all spoke pages with keyword-rich anchors

**Spoke Pages**
- Target sub-topics within the cluster
- 1,500-2,500 words each
- Link back to hub AND cross-link related spokes
- Target long-tail keywords

### Step 4: Internal Link Matrix

Design the cross-linking structure:

| From | To | Anchor Text |
|------|----|-------------|
| Hub | Spoke 1 | [keyword-rich] |
| Hub | Spoke 2 | [keyword-rich] |
| Spoke 1 | Hub | [seed keyword] |
| Spoke 1 | Spoke 2 | [contextual] |
| Spoke 2 | Hub | [seed keyword] |
| Spoke 2 | Spoke 1 | [contextual] |

### Step 5: Content Brief Generation

For each spoke page, generate:
- Target keyword
- Target word count
- Required sections (from SERP analysis)
- Questions to answer (from PAA)
- Internal link targets
- Unique angle (what competitors miss)

## Cluster Visualization (ASCII)

```
                    ┌──────────────┐
                    │  [HUB PAGE]  │
                    │ seed keyword │
                    └──────┬───────┘
           ┌───────────────┼───────────────┐
           │               │               │
    ┌──────▼──────┐  ┌─────▼─────┐  ┌──────▼──────┐
    │  SPOKE 1   │  │  SPOKE 2  │  │  SPOKE 3    │
    │ long-tail A │  │ long-tail B│  │ long-tail C │
    └──────┬──────┘  └─────┬─────┘  └──────┬──────┘
           │               │               │
    ┌──────▼──────┐  ┌─────▼─────┐  ┌──────▼──────┐
    │  SPOKE 1.1 │  │  SPOKE 2.1│  │  SPOKE 3.1  │
    │ ultra-long  │  │ ultra-long │  │ ultra-long  │
    └─────────────┘  └───────────┘  └─────────────┘
```

## Output Format

```
# Topic Cluster — {seed_keyword}

## Keyword Universe: {count} keywords
## Clusters Formed: {count}
## Spoke Pages: {count}

## Cluster Map
{ascii_visualization}

## Hub Page
| Field | Value |
|-------|-------|
| URL | {url or TBD} |
| Target keyword | {seed_keyword} |
| Word count | ~3,000+ |
| Sections | {list} |

## Spoke Pages
| Spoke | Keyword | Word Count | Cross-links |
|-------|---------|------------|-------------|
| 1 | {kw} | ~1,500 | Hub, Spoke 2 |
| 2 | {kw} | ~1,500 | Hub, Spoke 1 |

## Internal Link Matrix
{matrix}

## Content Briefs
### Spoke 1: {keyword}
- Target: {keyword}
- Word count: ~1,500
- Required sections: {sections}
- PAA questions: {questions}
- Unique angle: {angle}

## Recommendations
{recommendations}
```
