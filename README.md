# ListingGap

**Find the buyer objections your Amazon listing never answers — then rewrite the title and bullets with evidence. Free, private, no account.**

ListingGap is a Manifest V3 Chrome side-panel extension for Amazon sellers. It reads the product page and the reviews a buyer would see, clusters recurring objections, checks whether the listing copy answers them, and produces a paste-ready rewrite.

The name passed a Chrome Web Store screen on 2026-11-12; registry clearance is still open
(see `docs/trademark-check.md`).

## Chrome Web Store status

Published on 2026-11-06; re-verified in the developer dashboard on 2026-11-12.

- Item ID: `jdmmcbmgmhhjcblaefgmofllhaodafkg`
- Status: **Published — public** (已发布 - 公开发布)
- Version: `1.0.1` submitted for review on 2026-11-12 (feedback entry, sign-in detection,
  post-success review prompt). `1.0.2` is packaged and ready to submit after 1.0.1 is
  approved (adds a diagnostic when a review page parses to zero rows). `1.0.0` is the live
  public build.
- Current users: 2
- Ratings: none yet
- Auto-publish on approval: enabled
- Distribution: all regions except China
- Homepage: https://mindpinker.github.io/listinggap/
- Privacy policy: https://mindpinker.github.io/listinggap/privacy.html
- Support: https://mindpinker.github.io/listinggap/#support
- Developer console: https://chrome.google.com/webstore/devconsole/314b6557-d5a4-40dd-b929-f71a5964c4e5/jdmmcbmgmhhjcblaefgmofllhaodafkg

Public store URL:
`https://chromewebstore.google.com/detail/jdmmcbmgmhhjcblaefgmofllhaodafkg`

Because China is excluded from distribution, the public page may show “item unavailable”
when opened from a China/Hong Kong network. Verify the public page from a US/EU IP.

## Why this exists

Most listing tools stop at a score or a generic AI paragraph. ListingGap is built around one job:

> Turn repeated buyer complaints into specific listing copy — without inventing facts or uploading the seller's data.

The product is intentionally free. There is no backend, no AI API, no license server, no account, and no upsell. The analysis engine ships with the extension, so there is no per-audit cost to recover.

## Preview

The captures in `docs/screenshots/` are 430 px QA renders of the side panel, not final store assets.

![Report view](docs/screenshots/demo-report-2.png)

## What it does

- Extracts the title, Item Highlights, bullets, description, A+ presence, price, rating, review count, image count, Q&A count, and Amazon's "Customers say" summary.
- Reads visible reviews and tries 1–3 star review pages first, then recent reviews, then a product-page fallback.
- Clusters complaints across 45 objection aspects, with negation-aware matching.
- Marks each objection as **answered**, **partly answered**, **unanswered**, or **outside what copy can fix**.
- Detects claims that reviews contradict, such as "leak proof" when buyers report leaks.
- Scores conversion readiness using four transparent components: objection coverage 40%, proof 25%, clarity 20%, differentiation 15%.
- Produces a title within the marketplace limit, five rewritten bullets, an A+ outline, and quick wins.
- Marks missing facts as `[Needs input: ...]` instead of inventing materials, certifications, or test results.
- Supports manual listing entry, pasted reviews, and CSV import when Amazon hides review bodies.
- Exports Markdown and CSV, copies individual blocks, keeps up to 20 local audits, and can generate a constrained prompt for the user's own LLM.

## Install

**Install from the Chrome Web Store (recommended):**

https://chromewebstore.google.com/detail/jdmmcbmgmhhjcblaefgmofllhaodafkg

1. Open the store link in Chrome and click **Add to Chrome**.
2. Open an Amazon product page.
3. Click the ListingGap toolbar icon to open the side panel.
4. Click **Audit this page**.

ListingGap works on Amazon US, CA, AU, UK, DE, FR, IT, ES, NL, SE, PL, BE, BR, MX, JP, IN, SG, AE, SA, TR, and EG.
China is excluded from distribution, so the store page shows “item unavailable” when opened from a
China/Hong Kong network.

### Install the unpacked build (development)

1. Open `chrome://extensions`.
2. Turn on **Developer mode**.
3. Click **Load unpacked** and select the `extension/` folder in this repository.
4. Open an Amazon product page and click the toolbar icon.

If the product page was already open when the extension was installed, reload the page once so the content script is present.

Chrome 137+ no longer honors `--load-extension`. The local verification script uses the DevTools `Extensions.loadUnpacked` API with a fresh profile instead.

## Feedback

Settings → **Report a problem** opens the extraction-bug issue form. Include the ASIN, the
marketplace, and the stage that failed (title, bullets, reviews, proof, rewrite). The form
never asks for account data, and the extension never uploads the listing.

After a live audit has been copied or exported, the panel may show one honest review
request. It is capped at once every 90 days, never appears on first open, and offers no
incentive.

## Review fallback

Amazon often hides 1–3 star review bodies. ListingGap handles that in four layers:

1. Reviews visible on the current product page.
2. Amazon's "Customers say" summary.
3. Critical and recent review pages fetched directly from Amazon.
4. Manual paste or CSV import.

Paste format is one review per line. Prefix a rating when you know it:

```text
1|The clasp broke after two wears.
2|Much smaller than the photos.
3|The lid leaks when the bottle is on its side.
5|Love them, no issues.
```

CSV import accepts a `rating,text` pair, one product per line. A header row such as `rating,review` is skipped.

If Amazon shows a **Continue shopping** or robot-check screen, click through in the Amazon tab, reload the product page, and audit again. ListingGap now detects that state and tells you what to do instead of scoring an empty page.

## Privacy

- No backend, analytics, telemetry, advertising, account, or remote AI.
- Listing and review text is processed in the side panel on the device.
- Review-page requests go only to the Amazon domain the user is already visiting.
- Saved audits and settings use `chrome.storage.local`; they are not synced or uploaded.
- **Clear local history** in Settings deletes saved audits.
- The optional AI prompt is copied locally. ListingGap never sends it to an AI provider.

The bundled policy is at `extension/privacy.html`. A public URL is still required for the Chrome Web Store listing.

## Permissions

| Permission | Why it is needed |
|---|---|
| `activeTab` | Read the listing only when the user starts an audit |
| `storage` | Save settings and up to 20 audits locally |
| `sidePanel` | Show the report beside the Amazon page |
| Amazon host access | Read the product page and fetch review pages for the same ASIN |

There is no `scripting`, `<all_urls>`, `tabs`, or `windows` permission. The content script is declared in the manifest instead of injected with `chrome.scripting`.

## Limitations

- Amazon DOM changes can break extraction. The result is an explicit error state, not fabricated data.
- Low-star review bodies may be unavailable to logged-out or rate-limited users. Use paste/CSV.
- Analysis vocabulary is English-first. Non-English marketplaces can be read, but objection detection will be weaker.
- The audit is a hypothesis generator, not a guarantee of sales or ranking.
- The extension cannot verify the truth of a seller's claims; placeholders must be completed by the seller.
- No keyword search volume, BSR/sales estimates, PPC automation, image generation, or fake-review detection.

## Development

```powershell
cd listinggap
npm install
npm test
npm run demo
npm run verify
npm run live-check
npm run package
```

- `npm test` runs the analysis and extraction unit tests.
- `npm run demo` regenerates `extension/demo-data.js` from `tests/fixtures/jewelry.json`.
- `npm run verify` loads the real unpacked extension in a fresh Chrome profile through CDP, verifies the demo report, local storage, service worker, and privacy page.
- `npm run live-check` attempts a live Amazon extraction (`AMAZON_URL` can override the default ASIN). It is best-effort because Amazon may serve a bot interstitial; a handled interstitial is reported as a pass.
- `npm run package` writes `dist/listinggap-v<version>.zip` for the Chrome Web Store.

To verify a packaged build instead of the source folder:

```powershell
$env:EXTENSION_PATH = "C:\path\to\unzipped\extension"
node scripts/verify-extension.cjs
```

## Project layout

```text
extension/
  manifest.json          MV3 manifest
  background.js          side-panel behavior and defaults
  content.js             Amazon extraction + review-page fallback
  lib/analysis.js        scoring, objections, rewrites, exports
  sidepanel.html/css/js  report UI
  privacy.html           bundled privacy policy
  demo-data.js           generated demo fixture
scripts/
  build-demo.cjs
  build-store-assets.cjs
  package-extension.cjs
  verify-extension.cjs
tests/
  analysis.test.cjs
  extraction.test.cjs
site/
  index.html            GitHub Pages homepage / support
  privacy.html          public privacy policy
store-assets/
  screenshot-1..5.png   1280x800 Chrome Web Store screenshots
docs/
  competitor-analysis.md
  store-submission.md
```

## Research trail

- [Competitor analysis](docs/competitor-analysis.md)
- [Store submission pack](docs/store-submission.md)
- Product decision and validation kit live outside this repository in the private planning workspace.
- GitHub references: [Amazon-Listing-Analyzer](https://github.com/idis0037/Amazon-Listing-Analyzer), [ecom-agent](https://github.com/yoligehude14753/ecom-agent)

## Name and trademark

"Listing Doctor" was rejected because two Chrome Web Store listings already use it. "ListingGap" is a working name, not a cleared trademark. Before publishing:

1. Search the exact name and close variants in the Chrome Web Store.
2. Search USPTO TESS, EUIPO, and WIPO if selling internationally.
3. Check the available domain and support handle.
4. Keep the final manifest name, store title, landing-page H1, and privacy page consistent.
