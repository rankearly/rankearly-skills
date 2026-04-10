---
name: schema-markup
description: Use when writing, reviewing, or debugging Schema.org JSON-LD markup for rich results — Article, Product, FAQ, HowTo, LocalBusiness, Breadcrumb, Organization, Event, Recipe, VideoObject, Review — or when validating structured data and fixing rich-snippet eligibility issues.
metadata:
  displayName: Schema Markup
  status: live
---

# Schema.org Structured Data

The general shape of JSON-LD and the common `@type` vocabulary is assumed knowledge. This skill captures only the things that are easy to get wrong: recent Google rich-result deprecations, exact magic strings, numeric constraints, and implementation gotchas.

## Recent Google deprecations

Do not promise rich results for these types:

- **FAQPage rich results** — For Google Search, these are now limited to well-known, authoritative government and health websites. For most other sites, FAQ markup will not usually produce visible FAQ rich results.
- **HowTo rich results** — Deprecated in Google Search and no longer shown on desktop or mobile. Don't add HowTo markup just to chase Google rich results.
- **sameAs for Knowledge Panels** — Still a valid structured-data property for disambiguation and linking to official profiles, but it is not a "claim or control your Knowledge Panel" lever.

When users ask for FAQ or HowTo schema, explain these limits first so they can decide whether the markup is still worth adding.

## Choosing the right type

LLMs commonly pick the wrong `@type`:

- **Listicles / "best of" / "top 10" posts** → `ItemList` with numbered `ListItem` entries (optionally wrapping `Product`, `Review`, or `SoftwareApplication` nodes). This is what triggers the numbered/carousel rich result. Defaulting to `Article` or `BlogPosting` on a listicle is a missed opportunity.
- **Comparison / "X vs Y" pages** → there is no `Comparison` type. Use `Article` (or `BlogPosting`) for the page itself plus a `Product`/`SoftwareApplication` node per item being compared, optionally inside an `ItemList`.
- **SaaS landing page** → `SoftwareApplication` (or `WebApplication`) with `offers`, `aggregateRating`, `applicationCategory`. Not `Product`.
- **Single Q&A thread (forum, Stack Overflow–style)** → `QAPage`, not `FAQPage`. `FAQPage` is reserved for author-curated Q&A lists, and only on pages where the Q&A is actually visible to users.
- **LocalBusiness** → always use the most specific subtype available (`Dentist`, `Restaurant`, `AutoRepair`, `HairSalon`, etc.) instead of bare `LocalBusiness`. Google uses the subtype to decide which knowledge-panel features to offer.

## Required formats and literal strings

Google silently ignores these if misspelled:

| Context | Required literal |
|---|---|
| Offer availability | Full IRI form: `https://schema.org/InStock`, `/OutOfStock`, `/PreOrder`, `/BackOrder`, `/Discontinued` (not bare `"InStock"`) |
| Offer itemCondition | `https://schema.org/NewCondition`, `/UsedCondition`, `/RefurbishedCondition`, `/DamagedCondition` |
| Event eventAttendanceMode | `https://schema.org/OfflineEventAttendanceMode`, `/OnlineEventAttendanceMode`, `/MixedEventAttendanceMode` |
| Event eventStatus | `https://schema.org/EventScheduled`, `/EventCancelled`, `/EventMovedOnline`, `/EventPostponed`, `/EventRescheduled` |
| WebSite SearchAction | `"query-input": "required name=search_term_string"` and `target` must contain `{search_term_string}` |
| Dates | ISO 8601 only — `2026-04-10` or `2026-04-10T14:30:00+08:00`. Never `MM/DD/YYYY` or other locale formats. |
| Durations | ISO 8601 duration — `PT30M`, `PT1H15M`, `P1DT2H` |
| Prices | String or number without currency symbol: `"29.99"` not `"$29.99"`. Currency goes in `priceCurrency` as ISO 4217. |

All URLs in the payload (`url`, `image`, `@id`, `itemReviewed`, etc.) must be absolute and HTTPS. Relative paths and `http://` image URLs are both rejected.

## Google numeric and image constraints

| Property | Requirement |
|---|---|
| `Article.headline` | ≤ 110 characters (Google truncates; not a Schema.org rule) |
| `Article.image` | ≥ 1200px wide for AMP/Top Stories; ≥ 696px wide otherwise. Supply multiple aspect ratios: 16×9, 4×3, 1×1 |
| `Organization.logo` | ≥ 112×112px, on-white or transparent, not cropped |
| `Recipe.image` / `Product.image` | Supply 16×9, 4×3, **and** 1×1 — Google picks by surface |
| `Product.offers.priceValidUntil` | Required if price changes; omit only if indefinitely stable |
| `AggregateRating.ratingCount` or `reviewCount` | At least one required; `bestRating` defaults to 5 if omitted |

## Per-type gotchas

### Product — merchant listings vs product snippets (post-2023 split)

Google now evaluates `Product` markup against two different requirement tiers. The basic set LLMs usually produce only qualifies for **product snippets** (review stars in blue-link results). To be eligible for **merchant listings** (free shopping tab, product image carousels), the same markup must additionally include:

- `offers.priceSpecification` or `offers.price` + `priceCurrency` + `priceValidUntil`
- `offers.shippingDetails` → `OfferShippingDetails` with `shippingRate`, `shippingDestination`, and `deliveryTime`
- `offers.hasMerchantReturnPolicy` → `MerchantReturnPolicy` with `applicableCountry`, `returnPolicyCategory`, and (if returns allowed) `merchantReturnDays` + `returnMethod` + `returnFees`
- A product identifier: one of `gtin8` / `gtin13` / `gtin14` / `gtin` / `mpn` / `isbn`, **or** `brand.name` + `name` as a fallback pair

Missing `shippingDetails` or `hasMerchantReturnPolicy` is the #1 cause of "ineligible for merchant listings" warnings in Search Console. Either add them or tell the user their markup is product-snippet-only and shopping-tab coverage will not happen.

### SoftwareApplication

`applicationCategory` is a controlled enum, not free text. Use one of: `GameApplication`, `SocialNetworkingApplication`, `TravelApplication`, `ShoppingApplication`, `SportsApplication`, `LifestyleApplication`, `BusinessApplication`, `DesignApplication`, `DeveloperApplication`, `EducationalApplication`, `HealthApplication`, `FinanceApplication`, `SecurityApplication`, `BrowserApplication`, `CommunicationApplication`, `EntertainmentApplication`, `MultimediaApplication`, `UtilitiesApplication`, `ReferenceApplication`. For free apps, set `offers.price` to `"0"` — omitting `offers` makes the type ineligible.

### Event

Status transitions have strict co-requirements: `eventStatus: EventRescheduled` or `EventPostponed` requires `previousStartDate`. `EventMovedOnline` additionally requires flipping `eventAttendanceMode` to `OnlineEventAttendanceMode` and changing `location` to a `VirtualLocation` with a `url`. Leaving the old physical `Place` in place is a common error.

### VideoObject

`uploadDate` must not be in the future. Google rejects forward-dated videos silently (no rich result, no error).

### Recipe

`recipeInstructions` must be an array of `HowToStep` objects (each with `text`, optionally `name`/`image`/`url`), not plain strings. String-array form still validates in Schema.org but does not produce a Recipe rich result.

### WebSite

`SearchAction.target` can be either a URL string containing `{search_term_string}` or an `EntryPoint` object with `urlTemplate`. Both are valid; the object form is needed if you also want to declare `actionPlatform`.

### Review and AggregateRating — self-serving policy (high-violation area)

Google rejects and may manually penalize:
- `Review` or `aggregateRating` on `Organization` or `LocalBusiness` **about itself**. Must be nested on a reviewed sub-entity (Product, Service, Event, Book, Recipe, Course, etc.) or come from third-party reviewers.
- Any review/rating markup for content types not on Google's [supported review snippet list](https://developers.google.com/search/docs/appearance/structured-data/review-snippet#structured-data-type-definitions).

When a user asks for "5-star reviews on our homepage," redirect them to Product/Service-level markup.

## @id and @graph conventions

- One `<script type="application/ld+json">` per page with a single `@graph` is preferred over multiple script tags — it lets entities cross-reference via `@id` without duplication.
- Use fragment-style `@id` URIs anchored to the canonical URL: `https://example.com/#organization`, `https://example.com/about/#webpage`. This makes them stable and unique across the site.
- Every `@id` referenced must have exactly one full definition somewhere in the graph (on this page or another page). Dangling refs are a common validator warning.
- The page's main entity should set `mainEntityOfPage` (or be pointed at by `WebPage.mainEntity`) so Google knows which node the page is about.
- Don't ship multiple conflicting `Product` or `Article` nodes on one URL — pick one canonical, use `@graph` if you need related entities.

## React / Next.js injection

Rendering JSON-LD as JSX children will HTML-escape quotes and break the payload. Always use `dangerouslySetInnerHTML`:

```jsx
// ❌ WRONG — React escapes " to &quot; inside <script>
<script type="application/ld+json">{JSON.stringify(schema)}</script>

// ✅ CORRECT
<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{ __html: JSON.stringify(schema) }}
/>
```

Additional rules:
- Strip `undefined`/empty properties before stringifying — Google flags empty strings on required fields as errors.
- For `</script>` in any text value (e.g. HowTo step with inline code), escape as `<\/script>` to avoid prematurely closing the block.
- In the Next.js App Router, put the `<script>` in the page/layout component body (it ends up in `<body>`, which is fine for JSON-LD) or use the `<Script strategy="beforeInteractive">` wrapper if you need it in `<head>`.

## Validation workflow

1. **Rich Results Test** — https://search.google.com/test/rich-results — tells you whether Google will render a rich result for the URL. Only reports on Google-supported types.
2. **Schema Markup Validator** — https://validator.schema.org/ — validates against the full Schema.org vocabulary. Use this when Rich Results Test says "no items detected" but you have a niche type.
3. **Search Console → Enhancements** — the only place that shows aggregated errors from live indexing. Post-deploy check, not pre-deploy.

Rich Results Test reports warnings for *missing recommended fields*; these do not block eligibility but may reduce rich-result quality. Errors do block.

## Other common mistakes

- Markup describes content not present on the rendered page (spam policy violation).
- Hard-coded prices, stock, or ratings in a static template instead of pulled from live data — the markup drifts out of sync with the page and triggers spam/mismatch flags.
