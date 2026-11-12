# Post-launch follow-up — 2026-11-12

Seven actions after the public launch. Status is deliberately split into **live**, **local
and ready**, and **blocked**.

## 1. Verify a real store install

**Blocked by network region.**

The developer console confirms “已发布 - 公开发布” for 1.0.0 and “待审核” for 1.0.1.
From this machine, `chromewebstore.google.com/detail/...` returns “内容无法访问 / 此商品无法
购买或下载”, and so does a control item (uBlock Origin). The page is gated for the whole
region, not for this listing. A US/EU tester is still required to complete the
install → audit → copy flow.

## 2. Install entry points on existing traffic

**Live.**

- GitHub Pages hero now has “Install free on Chrome”; the privacy link moved to the
  fineprint and footer.
- `README.md` puts the store link first, with unpacked install second and the China
  exclusion noted.
- The existing “AI Review Summary for Amazon” popup now ends with a single ListingGap card
  (“You have seen what buyers complain about. Next, check which of those complaints your
  listing still fails to answer.”). No new permissions, no worker changes.
  Version 0.1.5 is submitted for review.

## 3. First 10 real sellers

**Local and ready, not sent.**

- `promotion/listinggap_leads_20261112.csv` — 10 live threads across r/AmazonSeller,
  r/AmazonFBA, and r/FulfillmentByAmazon, each with problem, fit, and whether an ASIN is
  needed.
- `promotion/listinggap_outreach_20261112.md` — three qualifying questions, a no-link first
  reply, disclosure language, and a post-audit follow-up.

Nothing was posted. The user must approve each reply; r/AmazonSeller also has a weekly
promotion thread that should be used instead of cold comments.

## 4. Minimum feedback loop

**Shipped in 1.0.1 (pending review).**

- Settings → “Report a problem” and the panel footer → “Report a bug”.
- `.github/ISSUE_TEMPLATE/extraction-bug.yml` asks for ASIN, marketplace, category, failed
  stage, expected result, Chrome version, and an optional redacted screenshot.
- The form is live on GitHub and the extension links straight to it.

## 5. Twenty-ASIN extraction QA

**Executed, with a product finding.**

22 ASINs across 8 categories and 3 marketplaces. 15 listing extractions succeeded with
title, bullets, images, rating, and A+ detection. 14 of those hit Amazon’s new sign-in wall
on review pages. Details and the three fixes are in `docs/qa-live-asins-20261112.md`.

## 6. First five honest reviews

**Shipped in 1.0.1 (pending review).**

The prompt appears only after a live audit has been copied or exported, never on first open,
at most once every 90 days, with no incentive and no five-star ask.

## 7. Name and trademark screen

**Done, with a hard limit.**

Live CWS search: `ListingGap` returns no results; `Listing Gap` returns ListingLens and
others but no ListingGap. `Listing Doctor` is confirmed taken by two extensions and must not
be used. USPTO/EUIPO/WIPO could not be completed because all three are captcha/JS-gated;
this is recorded in `docs/trademark-check.md` and must be closed by an attorney before paid
promotion.

## The one number that matters now

The review-source regression is bigger than any acquisition tactic. Until the paste/import
path is measured, installs will not convert into useful audits:

- 100 targeted visits → target ≥ 5 completed audits (currently unmeasured)
- 30 audits → target ≥ 9 copy/export (currently unmeasured)
- 10 seller conversations → target 3 “that matched what I saw” replies

Instrument the funnel before buying traffic. The extension has no analytics by design, so
the only honest measurement is manual: ask testers to report install → audit → export, and
count the GitHub issues and store reviews that arrive.
