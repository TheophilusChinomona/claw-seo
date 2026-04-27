---
name: seo-geo
description: >
  Optimize content for AI Overviews (Google), ChatGPT web search, Perplexity,
  and other AI-powered search experiences. GEO analysis including brand mention
  signals, AI crawler accessibility, passage-level citability scoring, and
  platform-specific optimization. Use when user says AI Overviews, GEO, AI search,
  LLM optimization, Perplexity, AI citations, ChatGPT search, or AI visibility.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# AI Search / GEO Optimization

## Key Statistics

| Metric | Value |
|--------|-------|
| AI Overviews reach | 1.5 billion users/month, 200+ countries |
| AI Overviews query coverage | 50%+ of all queries |
| AI-referred sessions growth | 527% (Jan-May 2025) |
| ChatGPT weekly active users | 900 million |
| Perplexity monthly queries | 500+ million |

## Critical Insight: Brand Mentions > Backlinks

**Brand mentions correlate 3x more strongly with AI visibility than backlinks.**
(Ahrefs December 2025 study of 75,000 brands)

| Signal | Correlation with AI Citations |
|--------|-------------------------------|
| YouTube mentions | ~0.737 (strongest) |
| Reddit mentions | High |
| Wikipedia presence | High |
| LinkedIn presence | Moderate |
| Domain Rating (backlinks) | ~0.266 (weak) |

## GEO Analysis Criteria

### 1. Citability Score (25%)

**Optimal passage length: 134-167 words** for AI citation.

**Strong signals:**
- Clear, quotable sentences with specific facts/statistics
- Self-contained answer blocks (extractable without context)
- Direct answer in first 40-60 words of section
- Claims attributed with specific sources
- Definitions: "X is..." or "X refers to..." patterns
- Unique data points not found elsewhere

**Weak signals:**
- Vague, general statements
- Opinion without evidence
- Conclusions buried in paragraphs
- No specific data points

### 2. Structural Readability (20%)

**92% of AI Overview citations come from top-10 ranking pages**, but 47% come from pages ranking below position 5.

**Strong signals:**
- Clean H1->H2->H3 heading hierarchy
- Question-based headings (matches query patterns)
- Short paragraphs (2-4 sentences)
- Tables for comparative data
- Ordered/unordered lists for step-by-step content
- FAQ sections with clear Q&A format

**Weak signals:**
- Wall of text with no structure
- Inconsistent heading hierarchy
- No lists or tables
- Information buried in paragraphs

### 3. Multi-Modal Content (15%)

Content with multi-modal elements sees **156% higher selection rates**.

**Check for:**
- Text + relevant images
- Video content (embedded or linked)
- Infographics and charts
- Interactive elements (calculators, tools)
- Structured data supporting media

### 4. Authority & Brand Signals (20%)

**Strong signals:**
- Wikipedia presence
- YouTube channel with relevant content
- Reddit mentions in relevant communities
- Industry press coverage
- Social proof (LinkedIn, Trustpilot, G2, Capterra)

### 5. llms.txt Compliance (10%)

- `/llms.txt` file exists (new emerging standard)
- Allows AI crawlers access to content
- Structured for machine reading

### 6. AI Crawler Access (10%)

Check robots.txt for AI crawler tokens:

| Crawler | Token | Purpose |
|---------|-------|---------|
| GPTBot | OpenAI | Model training |
| ClaudeBot | Anthropic | Model training |
| PerplexityBot | Perplexity | Search + training |
| Google-Extended | Google | Gemini training only |
| CCBot | Common Crawl | Open dataset |

**Note:** Blocking `Google-Extended` does NOT affect Google Search or AI Overviews — those use `Googlebot`.

## AI Citation Checklist

```
## AI Citation Readiness
- [ ] Direct answer in first 60 words
- [ ] Specific statistics with sources
- [ ] Definition-style openings (X is / X refers to)
- [ ] Question-based H2s matching user queries
- [ ] Lists and tables for multi-item content
- [ ] Multi-modal content (image + text)
- [ ] Wikipedia or YouTube presence
- [ ] External links to authoritative sources
- [ ] No thin/AI-generated-sounding content
- [ ] llms.txt or robots.txt allows AI crawlers
```

## Output Format

```
# GEO / AI Search Optimization — {domain}

## Citability Score: {score}/100
| Signal | Status |
|--------|--------|
| Passage length 134-167 words | ✅/❌ |
| Direct answer in first 60 words | ✅/❌ |
| Quotable statistics | ✅/❌ |
| Self-contained answer blocks | ✅/❌ |

## Structure Score: {score}/100
| Signal | Status |
|--------|--------|
| Clean heading hierarchy | ✅/❌ |
| Question-based H2s | ✅/❌ |
| Lists + tables present | ✅/❌ |
| Short paragraphs (<4 sentences) | ✅/❌ |

## Authority Signals
- Wikipedia: {present}/not found
- YouTube: {present}/not found
- Reddit: {present}/not found
- Industry press: {present}/not found

## AI Crawler Access
| Crawler | Allowed? |
|---------|----------|
| GPTBot | ✅/❌ |
| ClaudeBot | ✅/❌ |
| Googlebot | ✅/❌ |

## Recommendations
{prioritized_recommendations}
```
