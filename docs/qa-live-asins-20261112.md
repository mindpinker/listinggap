# Live ASIN QA — 2026-11-12

Harness: `scripts/qa-live-asins.cjs` + `tests/live-asins.json`
Input: 22 real ASINs, 8 categories, 3 marketplaces (US, DE, JP)
Raw results: `qa-results/2026-11-12-*-live-asins.json`
Environment: Chrome 142, US-exit HTTP proxy, fresh profile, unpacked build 1.0.1

## Result

| Metric | Count |
| --- | --- |
| ASINs attempted | 22 |
| Listing extracted (title + bullets) | 15 |
| Amazon sign-in wall on review pages | 14 of 15 |
| Reviews parsed | 11, from one listing |
| A+ detected | 14 |
| No A+ | 1 |
| Hard failures | 8 |

Every listing that loaded produced a title, five or more bullets, image count, rating, review
count, and A+ detection. The failure is not listing parsing; it is the review source.

## What broke

1. **Amazon now sends `/product-reviews/` to a sign-in page.** The old code received HTTP 200,
   parsed zero reviews, and reported “0 reviews” as if the listing had none. Fixed: the
   content script detects the sign-in document, stops fetching, sets
   `extraction.signInRequired`, and the panel now explains the fallback.
2. **Localized pages are not the same page.** A `zh-cn` Amazon.com page returned 8
   “bullets”, no Customers-say block, and no usable review markup. This mostly affects
   China/HK IPs; a US/EU shopper sees the English layout. Not changed, documented as a
   known limitation.
3. **A fetched review page that parses to zero rows was silent.** Fixed in source after the
   1.0.1 package was submitted: it now records “A review page loaded but no review text
   could be parsed”, which will ship in the next build.

## Honest read

The review-driven promise now depends on either (a) reviews rendered on the product page,
(b) Amazon’s “Customers say” summary, or (c) the user pasting/importing reviews. The
automatic 1–3 star crawl is no longer reliable for logged-out shoppers.

Before spending on acquisition, the next build should:

- make “Paste reviews” the first-class path when `signInRequired` is true;
- parse every review block Amazon renders inline, including the “Top reviews” carousel;
- keep the manual sample in the exported report so the evidence trail stays honest.

## Reproduce

```powershell
$env:QA_PROXY="http://127.0.0.1:7897"
$env:QA_OFFSET="0"
$env:QA_LIMIT="8"
node scripts/qa-live-asins.cjs
```

Amazon rate-limits rapid runs and may redirect `/dp/` to the homepage. The harness retries
twice with a 12–20 s backoff and records `blocked` separately from `failed`.
