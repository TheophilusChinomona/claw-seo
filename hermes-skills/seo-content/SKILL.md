---
name: seo-content
description: >
  E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness) analysis,
  content quality scoring, readability assessment, thin content detection, and AI
  citation readiness. Use when user says content analysis, E-E-A-T, content quality,
  readability, thin content, or AI citations.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Content Quality & E-E-A-T Analysis

## E-E-A-T Framework (Google Quality Rater Guidelines, Sept 2025)

### Experience
- First-hand knowledge signals: original screenshots, direct quotes, personal stories
- User-generated content authenticity
- "I tried this" / "my results" language
- Real photos vs stock photos

**Questions to answer:**
- Does the content come from actual experience?
- Are there original, firsthand depictions (photos, video, data)?
- Is there authentic, unique insight not found elsewhere?

### Expertise
- Author credentials visible and verifiable
- Topic depth and accuracy
- Niche authority vs generalist approach
- YMYL topics require formal credentials

**Questions to answer:**
- Who wrote this? Are credentials shown?
- Is the author an authority on this specific topic?
- Does the content go beyond surface-level information?

### Authoritativeness
- Industry recognition and citations
- Links from authoritative sources
- Social proof and mentions
- Author/page reputation

**Questions to answer:**
- Who links to this page? Are they authoritative?
- Does the site have external citations?
- Is the author/site known as a go-to resource?

### Trustworthiness
- Contact information present
- About page with physical address/identity
- SSL/security signals
- Clear sourcing and citations
- Accurate, up-to-date information

**Questions to answer:**
- Can you verify who runs this site?
- Is contact information available?
- Is the content accurate and current?
- Are sources cited with links?

## Content Quality Thresholds

| Page Type | Min Words | Quality Signals |
|-----------|----------|----------------|
| Blog post | 800+ | H2s, images, external links |
| About page | 300+ | Team, credentials, mission |
| Product page | 150+ | Specs, reviews, clear CTA |
| Landing page | 100+ | Single clear offer |
| Contact page | 50+ | Physical address, phone |
| Homepage | 200+ | Clear value proposition |

**Thin content:** Any page below minimum threshold for its type.

## Readability Assessment

- **Flesch-Kincaid Grade Level:** Target < 10 for general audiences
- **Sentence length:** Average < 20 words
- **Paragraph length:** Max 3-4 sentences per paragraph
- **Passive voice:** Keep < 20% of sentences
- **Complex words:** Avoid jargon without explanation

## AI Citation Readiness

For content to be cited by AI Overviews, Perplexity, ChatGPT:
- **Clear, direct answers** to common questions (的首句)
- **Structured data** — schema markup helps AI parse content
- **Named entities** — proper nouns clearly identified
- **Source citations** — link to authoritative sources
- **No thin content** — AI bypasses thin content
- **Factual accuracy** — AI prefers verifiable claims
- **Helpful supplementary content** — examples, stats, comparisons

## Content Analysis Commands

```bash
# Fetch and parse HTML for content elements
python3 /workspace/claw-seo/scripts/parse_html.py <url>
```

## Output Format

```
# Content Quality & E-E-A-T Analysis — {domain}

## E-E-A-T Scores (0-100)
| Factor | Score | Assessment |
|--------|-------|------------|
| Experience | XX | Strong/Moderate/Weak |
| Expertise | XX | Strong/Moderate/Weak |
| Authoritativeness | XX | Strong/Moderate/Weak |
| Trustworthiness | XX | Strong/Moderate/Weak |

## Content Quality Metrics
- Word count: {count}
- Readability grade: {grade}
- Thin content pages: {count}
- AI citation ready: Yes/No

## Findings
{findings}

## Recommendations
{recommendations}
```
