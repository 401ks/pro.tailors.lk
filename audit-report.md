# Pre-Deploy Audit Report — pro.tailors.lk

- **Deploy date:** 2026-08-11
- **Scope:** 34 live HTML pages (excludes `ui/` — 12 design prototypes, `Disallow`'d in robots.txt) + `robots.txt`, `sitemap.xml`, `llms.txt`, `og.md`, `og-image.svg`, `og-images/`
- **Mode:** SCAN ONLY — no files modified

---

## 1. URL Structure

| Check | Result | Notes |
|---|---|---|
| Every page is `<pagename>/index.html` | **PASS** | Only exception is root `404.html` (by design, error page at clean URL `/404`) |
| No `.html` in any href/src | **PASS** | 0 matches sitewide |
| No hardcoded `prop.tailors.lk` (typo domain) | **PASS** | 0 matches in any HTML/txt/xml/md/svg |
| `/app` and `/login` via a **single config variable** | **FAIL** | No config variable exists. All uses are hardcoded literals: `href="/app"` ×127 and `href="/login"` ×66 across pages. There is no deployment config file in the repo (no `netlify.toml`/`vercel.json`/`_redirects`/`_headers`), so app-redirect behavior is not verifiable from the repo alone |
| Canonical / og:url consistent per page | **PASS** | All 34 pages: exactly 1 canonical + 1 og:url, and they match |

**URLs pointing to root-relative pages resolve correctly** — verified via filesystem resolution for every internal href (see Block 5).

---

## 2. Content

| Check | Result | Notes |
|---|---|---|
| `lorem` | **PASS** | 0 matches |
| `TODO` | **PASS** | 0 matches |
| `placeholder` | **PASS** | 11 matches, all legitimate `<input placeholder="…">` form hints (early-access form, help search, invoice generator fields) |
| `coming soon content` | **PASS** | "Coming Soon" appears ~100× but all are intentional roadmap/badge UI (e.g. measurement chart, pricing calculator, payment reminders) — no empty stub content found |
| "Last Updated / Last verified" dates | **PASS** | All dates consistent: **August 8, 2026**. Legal pages use "Last updated" (`privacy`, `terms`, `data-responsibility`); comparison pages use "Last verified" (13 compare pages). No inconsistency found |
| Contact email | **PASS** | `team@tailors.lk` is the only contact email (3 `mailto:` instances are the same address with trailing punctuation in prose) |

---

## 3. SEO (per-page, 34 pages)

| Check | Result | Notes |
|---|---|---|
| `<title>` present + unique | **PASS** | All 34 present; zero duplicate og:titles across pages |
| Meta description present | **PASS** | All 34 present |
| Meta description length 50–160 chars | **WARN** | 6 pages exceed 160: `about` (199), `compare` (183), `early-access` (162), `help-and-support` (172), `terms` (170), `tools/invoice-generator` (169). Google truncates ~155–160; not deploy-blocking but worth trimming |
| Canonical present | **PASS** | All 34 |
| og:title / og:description / og:image / og:url | **PASS** | All present on all 34; og:title matches `<title>` on every page |
| twitter:card | **PASS** | `summary_large_image` on all 34 |
| og:image:alt non-empty | **PASS** | All 34 have alt text |
| robots.txt: `Allow: /og-images/`, `Disallow: /app`, `Disallow: /login`, `Sitemap:` line | **PASS** | robots.txt confirms all four (also keeps `Disallow: /ui/`) |
| sitemap.xml excludes `/app`, `/login`, `/404` | **PASS** | 33 URLs, none of the three |
| sitemap.xml has `<lastmod>` | **PASS** | `2026-08-08` on all 33 `<url>` entries |
| sitemap URL ↔ page canonical match | **PASS** | 0 sitemap entries without a matching page; 0 live pages missing from sitemap (excl. 404) |

**Full per-page SEO table** (all 34) — every row `OK` except noted:

| Page | Title | Desc | Canonical | OG img |
|---|---|---|---|---|
| `/` | Tailor Shop Software Sri Lanka | Tailors.lk Pro | 150 | `/` | og-homepage.jpg |
| `/404` | Page Not Found (404) | Tailors.lk Pro | 106 | `/404` | og-404.jpg |
| `/about/` | About Tailors.lk Pro… | 199⚠ | `/about/` | og-about.jpg |
| `/compare/` | Tailor Shop Software Comparisons… | 183⚠ | `/compare/` | og-compare.jpg |
| `/compare/us-vs-atelierware/` | Atelierware vs Tailors.lk Pro — Honest Comparison | 153 | ok | og-us-vs-atelierware.jpg |
| `/compare/us-vs-buttonstripe/` | Buttonstripe Alternative… | 153 | ok | og-us-vs-buttonstripe.jpg |
| `/compare/us-vs-dbest-tailoring/` | DBest Tailoring vs…What We Can Verify | 132 | ok | og-us-vs-dbest-tailoring.jpg |
| `/compare/us-vs-experience-5/` | eXPerience 5 vs…Design vs Operations | 153 | ok | og-us-vs-experience-5.jpg |
| `/compare/us-vs-fatbit-stitch/` | FATbit Stitch vs… | 140 | ok | og-us-vs-fatbit-stitch.jpg |
| `/compare/us-vs-handyseam/` | HandySeam Alternative… | 145 | ok | og-us-vs-handyseam.jpg |
| `/compare/us-vs-perfect-tailor/` | Perfect Tailor Management…Decoded | 136 | ok | og-us-vs-perfect-tailor.jpg |
| `/compare/us-vs-shristitch/` | ShriStitch Pricing & Alternative… | 138 | ok | og-us-vs-shristitch.jpg |
| `/compare/us-vs-smart-tailor/` | Smart Tailor App vs…Full Comparison | 140 | ok | og-us-vs-smart-tailor.jpg |
| `/compare/us-vs-sunrise-tailoring/` | Sunrise Tailoring Software Review… | 148 | ok | og-us-vs-sunrise-tailoring.jpg |
| `/compare/us-vs-tailornova/` | Tailornova vs…Not the Same Category | 152 | ok | og-us-vs-tailornova.jpg |
| `/compare/us-vs-tailoros/` | TailorOS Alternative… | 146 | ok | og-us-vs-tailoros.jpg |
| `/compare/us-vs-tailorsoft/` | TailorSoft Alternative… | 133 | ok | og-us-vs-tailorsoft.jpg |
| `/contact/` | Contact Tailors.lk Pro… | 140 | ok | og-contact.jpg |
| `/data-responsibility/` | Data Responsibility | 156 | ok | og-data-responsibility.jpg |
| `/early-access/` | Get Early Access to Tailors.lk Pro… | 162⚠ | ok | og-early-access.jpg |
| `/features/` | Tailor Shop Management Features | 145 | ok | og-features.jpg |
| `/features/customer-tracking/` | Customer Tracking Links… | 131 | ok | og-customer-tracking.jpg |
| `/features/invoicing/` | Invoicing & Payments… | 121 | ok | og-invoicing.jpg |
| `/features/measurement-vault/` | Digital Measurement Vault… | 133 | ok | og-measurement-vault.jpg |
| `/features/order-management/` | Order Management & Production Tracking… | 152 | ok | og-order-management.jpg |
| `/features/shop-branding/` | Shop Branding & Settings… | 131 | ok | og-shop-branding.jpg |
| `/help-and-support/` | Help & Support | 172⚠ | ok | og-help-and-support.jpg |
| `/how-it-works/` | How Tailors.lk Pro Works…4 Steps | 131 | ok | og-how-it-works.jpg |
| `/pricing/` | Free Tailor Shop Software | 136 | ok | og-pricing.jpg |
| `/privacy/` | Privacy Policy | 153 | ok | og-privacy.jpg |
| `/roadmap/` | Tailor Shop Software Roadmap | 149 | ok | og-roadmap.jpg |
| `/terms/` | Terms of Service | 170⚠ | ok | og-terms.jpg |
| `/tools/` | Free Tailoring Tools… | 153 | ok | og-tools.jpg |
| `/tools/invoice-generator/` | Free Tailor Invoice Generator… | 169⚠ | ok | og-invoice-generator.jpg |

All pages: `twitter:card=summary_large_image`, canonical == og:url, og:title == `<title>`, `og:image:alt` populated.

---

## 4. OG Images

| Check | Result | Notes |
|---|---|---|
| 34 `og-{slug}.jpg` files exist | **PASS** | Exactly 34 files in `og-images/`, one per page slug |
| Every page's og:image maps to an existing file | **PASS** | All 34 resolve on disk; 34 distinct images referenced, 0 missing |
| No page points og:image at `og-image.svg` | **PASS** | 0 references. (`og-image.svg` remains only as JSON-LD `Organization.logo` on all pages — that is a site logo, correct usage) |
| Dimensions | **PASS** | All 34 are **1376×768** |
| File size | **INFO** | 539–861 KB each — every file exceeds the ~400 KB sweet spot for fast social previews. Not blocking, but page-speed/social-scraper friendly would be <300 KB |
| og:image:alt empty | **PASS** | All 34 have alt text |

**Note:** `og.md` (source of truth) documents images as "1200×630"; actual files are 1376×768 and pages truthfully declare `og:image:width="1376"` / `height="768"`. This is correct — `og.md` is stale on the dimension spec only.

---

## 5. Links

| Check | Result | Notes |
|---|---|---|
| Internal link crawl (filesystem-resolved) | **PASS** | 0 broken internal links across all 34 pages (root-relative and relative hrefs both verified) |
| Footer present | **PASS** | All 33 content pages have `<footer>` + all 13 core nav links (`/features /pricing /compare /tools /roadmap /how-it-works /early-access /contact /help-and-support /about /privacy /terms /data-responsibility`). `404.html` intentionally has no footer |
| Socials use tailors.lk shortcuts | **PASS** | `https://tailors.lk/ig /fb /x /tk /yt` on all 33 content pages |
| App links use `/app` + `/login` only | **PASS** | Only `href="/app"` (127×) and `href="/login"` (66×) — no other app URL variants |
| WhatsApp | **PASS** | `wa.me/94758244216` with contextual prefill text; consistent number |
| mailto | **PASS** | `team@tailors.lk` only |

---

## 6. Encoding

| Check | Result | Notes |
|---|---|---|
| `<meta charset="UTF-8">` on every page | **PASS** | All 34 (including `404.html`) |
| Non-HTML files UTF-8 valid | **PASS** | `llms.txt`, `og.md`, `robots.txt`, `sitemap.xml`, `og-image.svg` all valid UTF-8; em-dashes in `llms.txt`/`og.md` are proper `E2 80 94` |
| Mojibake patterns | **FAIL** | **`privacy/index.html` lines 139–140**: double-encoded em dash `â€""` (bytes `C3 A2 E2 82 AC E2 80 9D`) in the "Supabase" and "Cloudflare" sub-processor bullets. Should be a single `—` (`E2 80 94`) |

Only 2 affected characters, isolated to one file.

---

## 7. Secrets

| Check | Result | Notes |
|---|---|---|
| `service_role`, `supabaseKey`, `secret`, `eyJ`, `api_key`, tokens, private keys | **PASS** | 0 matches across all HTML/txt/xml/js/json/md. No credentials, keys, or JWTs exposed |

---

## Verdict

## NO-GO

2 blocking FAILs found:

1. **Encoding (Block 6):** `privacy/index.html` lines 139–140 contain double-encoded em dashes (`â€""`). Must be replaced with a proper `—`. Affects 2 characters in 1 file.
2. **Config (Block 1):** `/app` and `/login` are hardcoded literal hrefs (127× `/app`, 66× `/login`) with **no single config variable** and no deploy redirect config in the repo. The intended redirect origin cannot be confirmed from the repository; decide and document the mechanism (e.g., host-level rewrite) before deploy.

### Non-blocking WARNs (fix if convenient)
- 6 meta descriptions >160 chars (`about`, `compare`, `early-access`, `help-and-support`, `terms`, `tools/invoice-generator`) — truncation risk in SERPs.
- All 34 OG images 539–861 KB — heavier than ideal; social scrapers may render slowly.

### Everything else — PASS
URL structure, content hygiene, SEO metadata (34/34), OG image mapping (34/34), internal links (0 broken), footer/nav, socials, sitemap, robots.txt, UTF-8 declarations, and secrets scan.
