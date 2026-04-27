---
name: seo-local
description: >
  Local SEO analysis covering Google Business Profile (GBP) optimization, NAP
  consistency, citation health, review signals, local schema markup, location
  page quality, multi-location SEO, and industry-specific recommendations.
  Detects business type (brick-and-mortar, SAB, hybrid) and industry vertical.
  Use when user says local SEO, Google Business Profile, GBP, map pack, citations,
  NAP consistency, local rankings, service area, or multi-location.
user-invokable: true
argument-hint: "<url>"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
---

# Local SEO Analysis

## Key Statistics

| Metric | Value |
|--------|-------|
| GBP signals share of local pack weight | 32% |
| Proximity share of ranking variance | 55.2% |
| Review signals share | ~20% |
| Mobile "near me" searches → visit in 24h | 76% |
| ChatGPT usage for local recommendations | 45% (up from 6%) |
| Local pack ad growth (Jan 2025 → Jan 2026) | 1% → 22% |

## Business Type Detection

Detect from page signals before analysis:

### Brick-and-Mortar
- Physical street address visible in footer/content
- Google Maps embed with pin/directions
- "Visit us at", "Located at", "Come see us"
- Structured address in LocalBusiness schema

### Service Area Business (SAB)
- No visible physical address
- Service area mentions: "serving [city]", "service area includes"
- "We come to you", "On-site service"
- `areaServed` in schema without `address.streetAddress`

### Hybrid
- Both physical address AND service area language
- "Visit our showroom" + "We also serve [areas]"

**Impact:** SABs skip physical address + embedded map verification. Brick-and-mortar gets full NAP + map checks.

## Industry Vertical Detection

| Vertical | Detection Signals |
|----------|------------------|
| **Restaurant** | /menu, reservations, cuisine types, dine-in, takeout |
| **Healthcare** | insurance, appointments, NPI, "Dr.", HIPAA |
| **Legal** | attorney, practice areas, bar admission, "free consultation" |
| **Home Services** | service area, emergency, "free estimate", licensed/insured |
| **Real Estate** | listings, MLS, agent bio, "open house" |
| **Automotive** | inventory, test drive, dealership, "new/used/certified" |

## Analysis Dimensions

### 1. GBP Signals (25%)

Primary category is the **single most important local pack factor**.

**Check for:**
- GBP embed or reference on page (Maps iframe, place ID, reviews widget)
- Primary category appropriateness
- Evidence of secondary categories (optimal: 4 additional)
- Business hours visible (rank higher when open)
- GBP link URL strategy: do NOT link to strongest organic page (Sterling Sky Diversity Update — risks suppressing organic rankings)
- Google Verified badge eligibility

**Q&A note (deprecated Dec 2025):** Recommend recreating Q&A content as FAQ sections on the website. GBP removed existing Q&A with no export available.

### 2. NAP Consistency (20%)

NAP = Name, Address, Phone Number

**Check across:**
- Website header/footer
- Google Business Profile (if accessible)
- Bing Places
- Apple Maps
- Yelp, Facebook, other citations

**NAP consistency rules:**
- Name: Exact match everywhere (including Inc./LLC abbreviations)
- Address: Suite numbers, street abbreviations consistent
- Phone: Same format everywhere (preferably local pattern)
- Hours: Consistent across all listings

### 3. Citation Health (15%)

**Citation platforms to check:**
- Google Business Profile
- Bing Places
- Apple Maps
- Yelp
- Facebook
- Yellow Pages
- BBB (Better Business Bureau)
- Industry-specific: Zillow (real estate), WeddingWire (vendors), etc.

**NAP accuracy on each citation.** Inconsistent NAP = trust signal loss.

### 4. Review Signals (20%)

**Check for:**
- Google reviews (quantity, recency, velocity, sentiment)
- Review response rate (business responding to reviews)
- Distribution across platforms
- Negative review handling
- Review quantity vs competitors

**Metrics:**
- Review count trend (growing or stagnant?)
- Average rating (4.0+ is competitive)
- Response rate to negative reviews

### 5. Local Schema Markup (10%)

**Required for local businesses:**
```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "...",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "...",
    "addressLocality": "...",
    "addressRegion": "...",
    "postalCode": "...",
    "addressCountry": "..."
  },
  "telephone": "...",
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": "...",
    "longitude": "..."
  },
  "openingHours": "..."
}
```

### 6. Location Page Quality (10%)

For multi-location businesses:

**Thin content guardrails:**
- ⚠️ **WARNING** at 30+ location pages (enforce 60%+ unique content per page)
- 🛑 **HARD STOP** at 50+ location pages (require user justification)
- Each location page needs unique: address, phone, hours, staff, testimonials, photos
- No doorway page patterns (near-identical pages with only city name changed)

## Output Format

```
# Local SEO Analysis — {domain}

## Business Type: {type} | Vertical: {vertical}

## GBP Signals
| Signal | Status |
|--------|--------|
| GBP embed present | ✅/❌ |
| Primary category aligned | ✅/❌ |
| Secondary categories (4 optimal) | ✅/❌ |
| Business hours visible | ✅/❌ |
| Google Verified eligible | ✅/❌ |

## NAP Consistency
| Platform | Name | Address | Phone |
|----------|------|---------|-------|
| Website | ✅/❌ | ✅/❌ | ✅/❌ |
| Google | ✅/❌ | ✅/❌ | ✅/❌ |
| Bing | ✅/❌ | ✅/❌ | ✅/❌ |
| Apple | ✅/❌ | ✅/❌ | ✅/❌ |

## Citation Health: {score}/100
- Citations found: {count}
- Consistent citations: {count}
- Inconsistent: {count}

## Review Signals
- Google reviews: {count} (avg {rating} stars)
- Review velocity: {trend}
- Response rate: {percentage}

## Local Schema: {present}/not found

## Recommendations
{recommendations}
```
