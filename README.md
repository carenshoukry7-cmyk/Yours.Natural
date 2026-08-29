# Yours Naturals — Checkout

A single-page storefront and checkout for **Yours** (solid perfumes, facial
oils, hair wax, coconut oil spray and soap bars) — plant-based, small-batch
skincare in the brand's cream, walnut and terracotta palette.

## Live link

The site is published as a Claude Artifact:

**https://claude.ai/code/artifact/56df3897-0939-4757-b53d-6ef0cc30d341**

- Open it as the owner and a **"Store settings"** link appears in the
  footer — edit the hero copy, shipping rule, contact email, and every
  product's name/price/description/stock, then **Save changes** to publish
  instantly for every visitor.
- Anyone else who opens the link just sees the storefront: browse by
  category, add to bag, and check out (shipping details → payment method →
  review → confirmation). It's the same URL either way — the edit panel
  only appears, and only actually saves, for the store owner.
- The artifact starts **private**. Share it from the page's share menu so
  customers can reach it.

## What the checkout does

- Cart with quantity steppers, persisted per-visitor in the browser
  (`localStorage`), a live subtotal and a free-shipping threshold.
- A 3-step checkout: shipping details (validated), payment method, review
  — then a confirmation screen with an order number and an "email me this
  order" link.
- Payment is **pay-at-pickup / bank transfer / cash-on-delivery** by
  design — the page never asks a customer for a card number, since there
  is no payment processor wired up behind it. Wire in a real processor
  (e.g. a Stripe Checkout link) before taking real card payments.
- Orders are shown to the customer (and can be emailed to them) but are
  **not** stored anywhere the owner can see later — there's no backend
  here, only the store's product catalog is saved. Treat it as a
  reservation flow: confirm and fulfill orders over email/phone.

## Files

- `site/index.html` — the storefront/checkout page, source of truth for
  the published artifact above. Republish it (via Claude) after editing
  the file directly to update the live link.
