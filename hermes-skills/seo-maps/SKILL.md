---
name: seo-maps
description: >
  Maps intelligence for local SEO — geo-grid rank tracking, GBP profile auditing,
  review intelligence across Google/Tripadvisor/Trustpilot, cross-platform NAP
  verification, competitor radius mapping, and LocalBusiness schema generation.
  Three-tier capability: free (Overpass + Geoapify), DataForSEO (full), DataForSEO
  + Google Maps (maximum). Use when user says maps, geo-grid, rank tracking,
  GBP audit, review velocity, competitor radius, local rank tracking, or SoLV.
user-invokable: true
argument-hint: "<command> [keyword|location|url]"
license: MIT
metadata:
  author: Praxis (Hermes port of AgriciDaniel/claude-seo)
  version: "1.0.0"
  category: seo
  compatibility: "DataForSEO MCP for Tier 1+, Google Maps API for Tier 2"
---

# Maps Intelligence

**Boundary with seo-local:** This skill analyzes business presence on maps **platforms** (via APIs). seo-local analyzes local SEO signals on the **website** (via HTML fetch). Do not duplicate — recommend `seo-local` for website-level checks.

## Quick Reference

| Command | What it does |
|---------|-------------|
| `maps audit <url>` | Full maps presence audit (auto-selects tier) |
| `maps grid <keyword> <location>` | Geo-grid rank scan (7x7, 1 keyword default) |
| `maps reviews <business> <location>` | Cross-platform review intelligence |
| `maps competitors <keyword> <location>` | Competitor radius mapping |
| `maps nap <business-name>` | Cross-platform NAP verification |
| `maps schema <business-name>` | Generate LocalBusiness JSON-LD |
| `maps gbp <business> <location>` | GBP completeness audit |

## Three-Tier Capability Detection

### Tier 0 (Free)
**Always available.** Overpass API + Geoapify + static checklist + schema generation.
Capabilities: competitor discovery, geocoding, static GBP checklist, cross-platform NAP guidance, schema generation.

### Tier 1 (DataForSEO)
**Requires:** DataForSEO MCP (`business_data_business_listings_search` tool available).
Capabilities: Everything in Tier 0 PLUS geo-grid rank tracking, live GBP profile audit, review intelligence (velocity, sentiment, distribution), GBP post activity.

### Tier 2 (DataForSEO + Google Maps Platform)
**Requires:** Tier 1 + Google Maps API key.
Capabilities: Everything in Tier 1 PLUS Google Places details, real-time business status, photo analysis.

**Always communicate the detected tier to the user at the start of analysis.**

## Geo-Grid Rank Tracking (Tier 1+)

Simulates Google Maps searches from multiple GPS coordinates to show ranking variation across a geographic area.

### Workflow
1. Geocode business address to center lat/lng
2. Generate grid points (default: 7x7, 5km radius) using Haversine offset
3. **Display cost estimate before proceeding** — DataForSEO credits consumed
4. Fire Maps SERP API calls per grid point
5. Find target business rank at each point
6. Calculate **SoLV** (Share of Local Voice): `(top_3_count / total_points) * 100`
7. Render ASCII heatmap in output

### Cost Warning (Required)
```
Geo-Grid Scan: [keyword] at [location]
Grid: 7x7 (49 points) | Keywords: [N] | Est. cost: $[amount]
DataForSEO credits will be consumed. Proceed?
```

## NAP Cross-Platform Verification (Tier 0+)

Check NAP consistency across:
- Google Maps
- Bing Places
- Apple Maps
- OpenStreetMap

For each platform, verify: Business name, full address, phone number.

## GBP Completeness Audit (Tier 1+)

Check:
- Business name accuracy
- Category completeness (primary + secondary)
- Hours (including special hours)
- Photos (count, variety)
- Posts (recency, frequency)
- Q&A (dec 2025: deprecated in GBP, recommend FAQ on website)
- Reviews response rate

## Review Intelligence (Tier 1+)

Cross-platform review data from:
- Google Business Profile
- Tripadvisor
- Trustpilot
- Facebook

**Metrics:**
- Total review count per platform
- Average rating per platform
- Review velocity (new reviews/month)
- Sentiment distribution (positive/neutral/negative)
- Response rate to negative reviews

## Schema Generation (Tier 0+)

Generate LocalBusiness JSON-LD from structured data.

**Required fields:**
- `@type` (LocalBusiness or specific subtype)
- `name`
- `address` (PostalAddress)
- `telephone`
- `geo` (GeoCoordinates)
- `openingHours`

**Optional but recommended:**
- `image`
- `url`
- `priceRange`
- `aggregateRating`
- `sameAs` (social profiles)

## Output Format

```
# Maps Intelligence — {domain}

## Capability Tier: {0/1/2}

## Geo-Grid Rankings: {keyword} at {location}
Share of Local Voice (SoLV): {score}%
Top-3 appearances: {count}/{total_points}
[ASCII heatmap]

## Competitor Radius: {count} competitors found
| Competitor | SoLV | Distance |
|-----------|------|----------|
| Business A | 78% | 0.2km |
| Business B | 45% | 0.5km |

## NAP Verification
| Platform | Name | Address | Phone |
|----------|------|---------|-------|
| Google | ✅/❌ | ✅/❌ | ✅/❌ |
| Bing | ✅/❌ | ✅/❌ | ✅/❌ |
| Apple | ✅/❌ | ✅/❌ | ✅/❌ |
| OSM | ✅/❌ | ✅/❌ | ✅/❌ |

## Review Summary
| Platform | Count | Avg Rating | Velocity |
|----------|-------|------------|----------|
| Google | {n} | {x}★ | {trend} |
| Tripadvisor | {n} | {x}★ | {trend} |
| Trustpilot | {n} | {x}★ | {trend} |

## Recommendations
{recommendations}
```
