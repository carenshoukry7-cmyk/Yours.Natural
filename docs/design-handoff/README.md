# Handoff: Yours — Storefront & Cash-on-Delivery Checkout

## Overview
Yours is a natural skin, hair, and bath care brand based in Heliopolis, Cairo. This package covers two views:

1. **Storefront** (`Yours Website.dc.html`) — a single-page site: hero, about, 8-product catalogue with variant selection and a product detail modal, 6 customer reviews, and a contact/footer block. Each section is a full-bleed photo or muted video background with a tinted overlay.
2. **Checkout** (`Yours Checkout.dc.html`) — a two-column checkout with delivery details, an order summary, and **cash on delivery as the only payment method**. No card, wallet, or online payment path exists or should be added.

Currency is **EGP** throughout. Prices are entered manually (no tax calculation).

## About the Design Files
The files in this bundle are **design references created in HTML** — prototypes that show the intended look and behavior. They are not production code to copy directly. They use a small in-house HTML component runtime (`support.js`, `image-slot.js`) that exists only to make the prototypes interactive in a browser; do not port that runtime.

The task is to **recreate these designs in the target codebase's existing environment** (React, Vue, Next.js, Shopify theme, native, etc.) using its established patterns, component library, and styling approach. If no environment exists yet, choose the most appropriate framework for an e-commerce storefront and implement the designs there.

## Fidelity
**High-fidelity.** Colors, typography, spacing, and interactions are final. Recreate the UI faithfully using the codebase's own libraries and primitives. The product data (names, variants, prices) is real client data and should be treated as the seed catalogue.

---

## Design Tokens

### Colors
| Token | Hex | Use |
|---|---|---|
| Cream (page) | `#F9F1E8` | Page background, inputs, cards on dark sections |
| White (surface) | `#FFFFFF` | Cards, product tiles, form panels |
| Olive (primary) | `#645D1E` | Buttons, prices, eyebrow labels, selected chips, links |
| Mocha (ink) | `#422B1C` | Headings, body text, dark footer background |
| Ink 85% | `rgba(66,43,28,.85)` | Body paragraphs |
| Ink 75% | `rgba(66,43,28,.75)` | Secondary paragraphs |
| Ink 55% | `rgba(66,43,28,.55)` | Field labels, unit labels |
| Ink border | `rgba(66,43,28,.22)` | Input borders |
| Hairline | `rgba(66,43,28,.14)` | Dividers |
| Olive tint | `rgba(100,93,30,.09)` | Selected payment block, note callout |
| Olive chip border | `rgba(100,93,30,.4)` | Unselected variant chip border |
| Modal scrim | `rgba(46,29,18,.6)` + `backdrop-filter: blur(4px)` | Overlays |
| Reviews overlay | `rgba(76,64,28,.78)` | Tint over reviews video |
| Contact overlay | `rgba(46,29,18,.82)` | Tint over contact photo |

There are exactly two background families: cream/white for light sections, olive/mocha for dark ones. Do not introduce further colors or gradients (the hero uses one cream-to-transparent gradient overlay only).

### Typography
- **Display / headings:** `Cormorant Garamond`, weights 400/500/600, italic used for pull-quotes and notes.
- **UI / body:** `Jost`, weights 300/400/500.
- **Eyebrow labels:** Jost, 11–13px, `letter-spacing: .22em–.32em`, `text-transform: uppercase`.
- **Buttons:** Jost, 11–13px, `letter-spacing: .16em–.18em`, uppercase.
- Headings use fluid sizing, e.g. hero `clamp(44px, 6.5vw, 84px)`, section titles `clamp(34px, 4vw, 54px)`, card titles 22px, modal title `clamp(30px, 3.4vw, 42px)`.
- Body 14–17px at weight 300, `line-height: 1.55–1.8`.

### Spacing & layout
- Section padding: `clamp(56px, 8vw, 110px)` vertical, `clamp(20px, 6vw, 72px)` horizontal.
- Content max-widths: 1200px (hero, products), 1140px (checkout), 1100px (reviews, contact), 880px (product modal).
- Grid gaps: 16–28px in the product grid, `clamp(24px, 5vw, 72px)` between major columns.
- **Border radius: 0 everywhere.** The only rounded elements are circles (review avatars, the payment radio dot).
- Shadows: cards `0 14px 34px rgba(66,43,28,.08–.1)`; card hover `0 22px 48px rgba(66,43,28,.16)`; modals `0 30px 80px rgba(0,0,0,.35)`.
- Transitions: `.22s–.35s ease`. Entrance animation `fadeUp` — `translateY(14px)` + opacity, `.7–.8s ease`, applied on scroll-entry where supported (`animation-timeline: view()`), plain fade-in as fallback.

---

## Screen 1 — Storefront (`Yours Website.dc.html`)

### Nav
Sticky, `rgba(249,241,232,.92)` + `blur(8px)`, 1px bottom hairline. Left: Yours logo image, 44px tall, `mix-blend-mode: multiply`. Right: About / Products / Reviews / Contact — Jost 14px, `.14em` tracking, uppercase, anchor-scrolling to section ids.

### Hero
Full-bleed muted looping video background (`assets/bg-video-2.mp4`), `object-fit: cover`, `object-position: 50% 55%`, with a cream gradient overlay left-to-right (`.94 → .86 → .45` alpha at 100deg). Two-column grid, `minmax(300px, 1fr)`.
- Left: eyebrow "100% Natural"; H1 "Naturally, it's Yours."; body paragraph; two buttons — solid olive "Shop the range" (hover mocha) and olive-outline "Our story" (hover fills olive).
- Right: a polaroid-style frame — white card, 14px padding, 52px bottom padding, offset olive block behind it at 12% opacity, product photo inside, and the italic caption "skincare, naturally yours" in olive.

### About
Background photo `assets/bg-flatlay.png` with `rgba(255,255,255,.82)` overlay. Two columns: framed store-shelf photo (`assets/about-shelves.jpg`) on a cream card, and the copy — eyebrow "Our story", H2 "About the Brand", two paragraphs (founded 1984, dermatologist-recommended, 100% natural).

### Products
Background photo `assets/bg-palm.png` with `rgba(249,241,232,.78)` overlay. Centered eyebrow + H2 "Our Products".

Grid is **`repeat(4, 1fr)`** — a fixed 4 columns at every breakpoint, 2 rows of 4. (Known constraint: it does not collapse on mobile. In the real implementation, make it responsive — 2 columns under ~900px, 1 under ~560px.)

Each card: white, 14px padding / 28px bottom, cursor pointer, hover lifts `translateY(-6px)` with the deeper shadow. Contents top to bottom:
1. Image, 190px tall, `overflow: hidden`. `object-fit` is per-product (`cover` by default, `contain` for the Sleek Bundle so the tall portrait is not cropped).
2. Eyebrow tag (10px, `.26em`, olive).
3. Product name — Cormorant 22px.
4. Description — 13px/1.5, max 30ch.
5. Variant label (10px uppercase), then **the first 3 variant chips only**. Chips: 11.5px Jost, 6px×11px padding, `white-space: nowrap`; selected = olive fill + cream text; unselected = transparent with `rgba(100,93,30,.4)` border. Clicking a chip must `stopPropagation` so it does not open the modal.
6. Price — Cormorant 25px olive + "EGP" in 11px uppercase. A zero/unset price renders as an em dash, not "0".
7. "Order now" button — olive, 10px×24px padding, links to `#contact`, also stops propagation.

Clicking anywhere else on the card opens the product modal.

### Product detail modal
Scrim + centered panel: cream `#F9F1E8`, max-width 880px, `max-height: 90vh` scrollable, two-column grid `minmax(280px, 1fr)`, `fadeUp` entrance. Close button top-right: 38px square, `rgba(66,43,28,.85)` background, cream ✕.

- **Left:** product image, `min-height: 320px`, `object-fit` per product. For products with a gallery, a row of 56px square thumbnails sits at bottom-left, 8px gap; the active one has a 2px olive border, inactive ones `opacity: .7`. Clicking a thumbnail swaps the main image.
- **Right:** eyebrow tag; H3 product name; full description; an optional italic note in an olive-tint block (used by the Sleek Bundle); hairline; **the full variant list** (all chips, wrapped); an optional second chip row for a separate axis (used by Perfumes: size drives price, scent is a separate choice); an optional free-text comment box; price — Cormorant 38px olive + "EGP"; and an "Order now" button (14px×36px) that closes the modal and jumps to contact.

Selecting a variant updates the price live, and for products where variants carry their own image (Sleek Bundle), selecting a variant also swaps the displayed image on both the card and the modal.

### Reviews
Full-bleed muted looping video (`assets/bg-video-1.mp4`) with `rgba(76,64,28,.78)` overlay. Eyebrow "Kind words" + H2 "Customer Reviews" in cream. Grid `minmax(280px, 1fr)`, **6 cards**. Each: cream panel, `clamp(28px,4vw,44px)` padding, centered column, 16px gap — 96px circular avatar, name in Cormorant 24px/600, italic quote in Cormorant 20px wrapped in typographic quotes, and a 5-glyph olive flower rating (`❀ ❀ ❀ ❀ ❀`, `.3em` tracking).

**Open item:** reviewer names and avatars are placeholders. The client's real names are Mariam Amgad, Mina Sameh, Momen Ashraf, Nour Elsobky, Jana Alaa, Farrah Ali; avatar images were not delivered. Wire this section to real review data.

### Contact / footer
Background photo `assets/bg-coconuts.png` with `rgba(46,29,18,.82)` overlay, cream text. Two columns: brand block (Cormorant 44px "Yours", eyebrow "100% Natural", tagline) and contact block (H2 "Contact Us" + labelled Location / Phone / Email rows). Real details: **Heliopolis — Cairo**, **+20 1200 455 560**, **sales@yours.com**. Bottom bar above a `rgba(249,241,232,.18)` hairline: copyright left, "Brand Guidelines — Edition 2026" right.

### Background video requirements
Both videos are `autoplay loop muted playsinline`, absolutely positioned, `object-fit: cover`. They must be **silent and unmuteable** (`muted = true`, `volume = 0` enforced in JS, no controls) and must carry **no baked-in typography** in the visible crop — the reviews clip has a caption near the top which the landscape crop deliberately cuts off (`object-position: 50% 60%`). Preserve that crop. The prototype also re-fetches a video as a blob and retries playback if the element errors; in production, host the videos properly and use a poster frame instead.

---

## Screen 2 — Checkout (`Yours Checkout.dc.html`)

### Purpose
Collect delivery details and confirm a cash-on-delivery order.

### Layout
Nav (logo left, "← Continue shopping" right, 1px bottom hairline), then a 1140px container with `clamp(32px,5vw,64px)` vertical padding. Eyebrow "Checkout", H1 "Complete your order", then a responsive grid — `repeat(auto-fit, minmax(min(100%, 320px), 1fr))`, `align-items: start`, gap `clamp(24px,4vw,52px)` — which gives equal-width form and summary columns side by side above roughly 700px and collapses to a single full-width column below that.

### Delivery details panel
White card, `clamp(24px,3.5vw,40px)` padding. H2 "Delivery details" (Cormorant 28px). A `minmax(200px, 1fr)` sub-grid with 18px gaps holds: **Full name**, **Phone number** (placeholder `01xxxxxxxxx`), **Governorate** (select), **City / area**. Below, full-width: **Street address** ("Street, building, floor, apartment") and **Order notes (optional)** — a 3-row textarea, "Preferred oil type, delivery time, or anything else".

Field styling: label = 11px uppercase `.22em` at ink-55%; input = 15px weight 300, cream background, `1px solid rgba(66,43,28,.22)`, `13px 14px` padding, no radius, no focus ring in the prototype — **add a visible focus state in production** (olive 1px border or 2px olive outline).

### Payment panel
White card. H2 "Payment" plus the line "Cash on delivery is our only payment method — you pay the courier when your order arrives." Then a single pre-selected option block: olive-tint background, 1px olive border, 20px×22px padding, a 20px circle with a 5px olive ring on cream (a permanently-checked radio), "Cash on delivery" in Cormorant 23px/600 and "Pay in cash to the courier on arrival" beneath. This is the only method — no alternatives, no method switcher.

### Order summary panel
White card, static position (not sticky, so it reads correctly once stacked below the form on narrow screens). H2 "Order summary", then line items: 64px square photo, name in Cormorant 20px, `variant · Qty n` at 12.5px, and the line total in Cormorant 19px olive. Hairline, then **Subtotal** and **Delivery — {governorate}** rows (14.5px, weight 300). Hairline, then the total row: label "Total due on delivery" (11px uppercase) and the amount in Cormorant 36px olive with a small uppercase "EGP". Then the primary button, then the reassurance line: "We will call you to confirm before dispatch. Delivery takes 2–5 business days."

### Primary button states
Full width, 17px×24px padding, 12.5px uppercase `.18em`, `transition: background .25s ease`.
- **Enabled** (name, phone, and street address all non-empty): olive background, cream text, `cursor: pointer`, label "Place order — cash on delivery".
- **Disabled**: `rgba(66,43,28,.18)` background, `rgba(66,43,28,.5)` text, `cursor: not-allowed`, label "Fill in name, phone & address".

### Confirmation overlay
On submit: scrim + centered cream panel, max-width 520px, `clamp(32px,5vw,52px)` padding, centered, `fadeUp`. Eyebrow "Order received", H3 "Thank you, {first name}", body "Your order is confirmed. Please have **{total} EGP** in cash ready for the courier. We will call {phone} to confirm the delivery window." and a "Done" button (olive) that closes it. Backdrop click also closes.

### Shipping table (prototype values — confirm with the client)
| Governorate | Delivery |
|---|---|
| Cairo | 50 EGP |
| Giza | 50 EGP |
| Alexandria | 65 EGP |
| Delta & Canal | 75 EGP |
| Upper Egypt | 85 EGP |
| Red Sea & Sinai | 110 EGP |

---

## Interactions & Behavior
- **Anchor navigation** — nav links and "Order now" buttons scroll to section ids; `scroll-behavior: smooth`.
- **Variant selection** — per-product, persists while the page is open; drives price and (where defined) the displayed image. Chip clicks must not bubble to the card's open handler.
- **Product modal** — open on card click; close on ✕, backdrop click, or "Order now". Gallery index resets to 0 on each open.
- **Scroll reveal** — sections and cards fade up as they enter the viewport, once. Implemented with CSS scroll-driven animations and a plain fade-in fallback; must never be able to leave content permanently invisible.
- **Checkout validation** — name, phone, and street address required; everything else optional. Validate the phone as an Egyptian mobile number in production (`01[0125]\d{8}`) and surface inline errors, which the prototype does not.
- **Responsive** — every section is fluid via `clamp()` and `auto-fit` grids, and the checkout collapses from two columns to one below roughly 700px. The one exception is the storefront product grid's fixed `repeat(4, 1fr)`, which does not collapse and needs a responsive fix in production.

## State Management
Storefront: `selectedVariant` per product, `openProductIndex | null`, `galleryIndex`, `selectedScent` (Perfumes), and a free-text note (Sleek Bundle).
Checkout: `fullName`, `phone`, `governorate`, `city`, `address`, `notes`, `placed`. Derived: line totals, subtotal, shipping (from governorate), total, and form validity.
Production additions: a real cart shared between the two screens, order submission to a backend, and an order reference number in the confirmation.

## Catalogue data (as designed)

| Product | Variant axis | Options and prices (EGP) |
|---|---|---|
| Natural Oils (15ml) | Oil type | Castor 100, Rose 115, Peppermint 110, Coconut 170, Arugula 170, Lavender 150, Garlic 180, Argan 170, Jojoba 200, Almond (Sweet-Hot) 180, Saad 200, Sesame 170, Rosemary 210, Clove 210 |
| Solid Perfume Stick | Scent | Vanilla Cream, Oud, Rose Vanilla, Coconut, Pomegranate Musk, White Musk, White Oud, Salted Caramel, Caramel Musk, Rose Musk — all 250 |
| Solid Perfume Jar | Scent | Same 10 scents — all 270 |
| Sleek Bundle | Item | Full Bundle 515 (default), Brush 150, Castor Oil 30ml 100, Hair Wax Stick 350. Note shown: the included oil can be per request; default is castor oil. Includes a free-text box for the customer's preferred oil. |
| Perfumes | Size (+ scent) | 10 ml 220, 20 ml 340. Scents: Sweet Oud, Coconut, Musk, Flower Heaven, Rose Vanilla |
| Natural Soap Bar | Scent | Turmeric & Honey 120, Oatmeal 110, Rose 130, Goat Milk 140, Charcoal 125 |
| Green Clay Mask | Blend | Matcha 220, Sidr Seeds 200, Charcoal 240, Moroccan Clay 230, Turmeric 210 |
| Botanical Serum | Blend | Jasmine 380, Neroli 400, Chamomile 360, Rosehip 420, Lotus 410 |

Prices for products beyond Natural Oils, the perfume stick/jar, Perfumes, and the Sleek Bundle are **placeholders** — confirm all of them with the client before launch.

## Assets
All in `assets/`, supplied by the client (product photography, brand logo, and two background clips).

- Logo: `logo-cream.jpg`, `logo-green.jpg`
- Section backgrounds: `bg-video-2.mp4` (hero), `bg-flatlay.png` (about), `bg-palm.png` (products), `bg-video-1.mp4` (reviews), `bg-coconuts.png` (contact)
- Feature photos: `hero.jpg`, `about-shelves.jpg`
- Products: `oils-flatlay.jpg`, `perfume-stick-2/3/4.jpg`, `stick-vanilla.jpg`, `jar-kraft.jpg`, `perfume-sprays.jpg`, `sleek-bundle.jpg`, `sleek-bundle-2.jpg`, `sleek-bundle-card.jpg`, `wax-pink.jpg`, `soap-bars.jpg`, `clay-mask.jpg`, `serum-flower.jpg`, `body-butter.jpg`, `body-scrub.jpg`, `hair-oil.jpg`
- **Missing:** review avatars, and photos for the Brush and Castor Oil options inside the Sleek Bundle.

Optimise and serve these responsively in production (WebP/AVIF, `srcset`, video posters); they are raw phone photos here. Fonts are Google Fonts — Cormorant Garamond and Jost.

---

## Build scope for implementation

The client asked for a **fully functioning site**, not just the front end. Choose the stack you judge best for an Egyptian small-brand storefront (the client has no preference) and implement all of the following.

### Framework
No preferred stack. Pick one and state the choice in your first commit. A React meta-framework with server routes (e.g. Next.js) plus a hosted Postgres suits this scope; a Shopify or WooCommerce theme is also acceptable if it does not compromise the cash-on-delivery-only checkout or the bilingual requirement.

### Required functionality
1. **Cart persisted across pages** — add-to-cart from the product modal (carrying the chosen variant, size/scent, and any free-text note), a cart view, quantity edits, and removal. Persist across navigation and reloads (server-side cart or storage-backed), and feed the checkout summary from it rather than the hard-coded array in the prototype.
2. **Orders saved to a database** — persist customer name, phone, governorate, city, street address, notes, line items with chosen variants, per-line and total amounts, shipping fee, payment method (always cash on delivery), status, and timestamps. Generate a human-readable order reference and show it in the confirmation overlay.
3. **Order confirmation email** — send to the customer on order placement, and to the store address (`sales@yours.com`) with the full order. Match the brand: cream background, olive accents, Cormorant Garamond headings.
4. **WhatsApp order notification to the store** — push each new order to the client's WhatsApp (`+20 1200 455 560`) via WhatsApp Cloud API or an equivalent provider, including customer name, phone, address, line items, and total. This is the client's primary order channel; make delivery failures visible (retry plus an admin-visible error), never silent.
5. **Admin page to edit products and prices** — authenticated CRUD over products, their variant axes and per-variant prices, stock/visibility, photos, and the shipping-fee table. Also list and update order statuses. The prototype's catalogue is the seed data; nothing should require a code change to reprice.
6. **Arabic + English** — full bilingual UI with a language switcher and **RTL layout for Arabic**: mirror the grids, nav, product cards, modal, and checkout; keep numerals and EGP formatting locale-correct. Product names, descriptions, variant names, and reviews all need translated fields in the database. Pair the Cormorant Garamond / Jost stack with an Arabic display and UI face of similar weight and feel (e.g. a serif for headings, a clean sans for body) and set fluid sizes so Arabic text does not overflow the fixed-height cards. Have the client supply or approve the Arabic copy — do not machine-translate the brand voice.

### Payment constraint
Cash on delivery is the **only** payment method. Do not add card, wallet, or online payment paths, and do not add a payment-method switcher.

### Before launch — client input still needed
- Review avatars and the six real reviewer names (Mariam Amgad, Mina Sameh, Momen Ashraf, Nour Elsobky, Jana Alaa, Farrah Ali).
- Photos for the Brush and Castor Oil options inside the Sleek Bundle.
- Confirmed shipping fees per governorate (the table above is a placeholder).
- Confirmed prices for Natural Soap Bar, Green Clay Mask, and Botanical Serum.
- Arabic copy for all product and marketing text.

## Files
- `PHOTO-INDEX.md` + `PHOTO-INDEX-products.png` — every photo mapped to the product and slot it belongs to
- `Yours Website.dc.html` — storefront prototype
- `Yours Checkout.dc.html` — checkout prototype
- `support.js`, `image-slot.js` — prototype-only runtime, do not port
- `assets/` — all imagery and video

Open either HTML file directly in a browser to see the intended behavior.
