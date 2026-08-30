# Yours — Storefront & Checkout

A working storefront and cash-on-delivery checkout for **Yours**, a
natural skin/hair/bath care brand in Heliopolis, Cairo — rebuilt from the
client's own design files (`Yours Website.dc.html`, `Yours Checkout.dc.html`,
`README.md` handoff, `bgvideo1.mp4`/`bgvideo2.mp4`) to real brand fidelity:
cream/white/olive/mocha palette, square corners, Cormorant Garamond + Jost,
the real 8-product EGP catalogue, real customer quotes, and the client's
own hero/reviews background videos.

## Live link

**https://claude.ai/code/artifact/56df3897-0939-4757-b53d-6ef0cc30d341**

One URL serves both roles:

- **As the store owner** — a **"Store settings"** link appears in the
  footer. It opens a panel to edit the hero copy, about paragraphs,
  contact details, the shipping fee per governorate, the full product
  catalogue (name, tag, description, variants with price, note callouts),
  and reviews. **Save changes** publishes instantly for every visitor.
- **As a customer** — the same URL, storefront only: browse by category,
  pick a variant (and, for Perfumes, a scent), open the product modal,
  add to bag, and check out. Checkout is **cash on delivery only** —
  matching the client's design exactly — with the real governorate
  shipping table baked in, and a confirmation screen with an order
  reference.

## What's faithful vs. what's still a placeholder

**Faithful to the design:** every color, type choice, spacing rule, the
real catalogue (names/variants/prices), real review quotes, the exact
checkout copy and button states, the client's actual hero and reviews
background videos, and — pulled from the brand's asset drive — the real
logo, hero shot, about-shelves photo, all 8 product photos (with photo
galleries on the Solid Perfume Stick, Hair Wax Stick, and Sleek Bundle),
and the three section background photos (about/products/contact).

**Still placeholders:**
- Review avatars — the source files in the drive are 13–17MB each, over
  the download tool's size limit in this environment. They render as an
  olive initials circle instead; drop in compressed versions (a few
  hundred KB) via the admin's asset pipeline to swap them in.
- No backend yet: orders aren't saved anywhere the owner can review later,
  no order confirmation email, and no WhatsApp order notification. The
  original design brief also asks for a real database, authenticated
  admin, and full Arabic/RTL bilingual support — that's a genuine
  production build (e.g. Next.js + Postgres + WhatsApp Cloud API), well
  beyond what a static page can do; this artifact is the storefront/
  checkout front end, functioning end-to-end for browsing and placing an
  order, ready to sit in front of that backend once it exists.

## Files

- `site/index.html` — the storefront/checkout page, source of truth for
  the published artifact above (photos and videos are inlined directly
  into it as base64). Edit it and republish (via Claude) to update the
  live link.
- `docs/design-handoff/` — the client's original design handoff docs
  (`README.md`, `PHOTOINDEX.md`) mapping every asset filename to the
  product/section it belongs to.
