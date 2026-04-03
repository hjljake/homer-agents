---
name: checkout-analysis
display_name: Checkout Analysis
description: Framework for evaluating checkout flows to identify upsell opportunities, friction points, and optimization surfaces across e-commerce platforms
category: analysis
---

# Checkout Analysis

When analyzing a checkout flow for upsell and AOV optimization opportunities, use this structured framework. The analysis may come from a live URL, screenshots provided by the user, or a text description of the flow.

## Input Methods

### From a URL
When the user provides a checkout page URL:
- Navigate the flow from product page → cart → checkout → (if possible) post-purchase
- Note each step/page in the funnel
- Identify the platform (Shopify, WooCommerce, Stripe, custom) from page structure, URL patterns, or source clues
- Catalog every existing upsell/cross-sell element already present
- Note the payment methods accepted and checkout layout (single-page vs multi-step)

### From Screenshots
When the user provides screenshots:
- Identify each screenshot's position in the funnel (product page, cart, checkout, confirmation)
- Analyze visible UI elements, calls-to-action, and product presentation
- Note what's NOT visible (missing elements are opportunities)
- Ask the user to clarify the flow between screenshots if gaps exist

### From Text Description
When the user describes the flow in their own words:
- Extract: number of steps, what happens at each step, where money changes hands
- Ask clarifying questions if the description is ambiguous
- Focus on: what the customer sees at each stage, how they add items, and how they pay

## Checkout Flow Anatomy

### Shopify Standard
```
Product Page → Cart Drawer or Cart Page → Shopify Checkout (hosted) → Thank You Page
```
- Cart drawer: primary upsell surface (apps can inject here)
- Checkout: limited customization (unless Shopify Plus)
- Post-purchase: available via apps (ReConvert, etc.) on standard; native on Plus
- Key constraint: Shopify controls the checkout page — you can't add arbitrary elements without Plus/Checkout Extensions

### WooCommerce
```
Product Page → Cart Page → Checkout Page → Thank You Page
```
- Cart page: fully customizable, prime upsell surface
- Checkout page: customizable (fields, layout, upsell sections)
- Multi-step checkout possible via plugins (CartFlows, FunnelKit)
- No platform restrictions on what you can add where

### Stripe Checkout (Hosted)
```
Product Selection → Stripe Checkout (hosted page) → Success URL (your page)
```
- Very limited upsell surface on the Stripe page itself
- Adjustable quantity and add-on line items must be set before redirect
- Success page (your domain): primary upsell surface
- Best strategy: pre-checkout upsell page or post-purchase offers on success page

### Custom / Other
```
Varies — map the actual flow step by step
```
- Identify which steps are on the user's domain (customizable) vs. third-party (constrained)
- Note where the payment form lives (PCI compliance boundary)
- Document the technical stack if knowable (React, server-rendered, etc.)

### Over the Phone / In Person
```
Conversation → Payment (manual/terminal)
```
- Upsell happens in the conversation, not in UI
- Focus on: scripts, talk tracks, decision trees, offer sequencing
- Different framework needed — conversational upsell, not UI-based

## What to Look For

### Current Upsell Surfaces (What Exists)
- [ ] Product page recommendations ("Frequently bought together", "You may also like")
- [ ] Bundle or kit offers
- [ ] Cart page cross-sell suggestions
- [ ] Order bump at checkout (checkbox add-on)
- [ ] Free shipping progress bar or threshold indicator
- [ ] Post-purchase offer on thank-you page
- [ ] Email upsell after purchase
- [ ] Subscription or recurring purchase option

### Missing Opportunities (What Doesn't Exist)
For each missing element, note:
- Where it would go in the current flow
- What type of offer would fit (upsell, cross-sell, bump, threshold)
- Estimated implementation difficulty on this platform
- Expected impact (high/medium/low based on placement and product type)

### Friction Points (What Hurts Conversion)
- [ ] Too many steps to checkout (>3 pages before payment)
- [ ] Required account creation before purchase
- [ ] Slow page load times (especially cart/checkout)
- [ ] Unclear pricing or surprise fees appearing late in the flow
- [ ] Missing trust signals (no SSL badge, no reviews, no guarantee)
- [ ] Poor mobile experience (buttons too small, text too dense, horizontal scroll)
- [ ] Confusing navigation (can't easily go back or edit cart)
- [ ] No guest checkout option

### Existing Upsell Quality Assessment
For each upsell element already present, evaluate:
- **Relevance:** Is the suggested product actually related to what the customer is buying?
- **Timing:** Does it appear at the right moment in the flow?
- **Presentation:** Is it visually clear, easy to add, easy to dismiss?
- **Pricing:** Is the upsell priced appropriately relative to the main purchase? (Rule of thumb: upsell should be <40% of cart value for order bumps, can be higher for bundles)
- **Mobile:** Does it work well on mobile devices?

## Red Flags

- **Aggressive pop-ups blocking checkout** — these increase abandonment 15-25%
- **No "no thanks" option** — forced upsells damage trust
- **Upsell more expensive than main product** — feels predatory, reduces conversion
- **Too many upsell touchpoints** — more than 2 offers per checkout session hurts conversion
- **Slow-loading upsell elements** — dynamic recommendations that delay page render
- **Generic recommendations** — "best sellers" instead of contextually relevant products
- **Upselling during payment entry** — don't distract during the most sensitive step

## Output Format

Structure your checkout analysis as:

1. **Platform Identified** — what CMS/platform they're using and version/plan if determinable
2. **Flow Map** — step-by-step description of the current checkout journey
3. **Current Upsell Inventory** — what upsell/cross-sell elements already exist, with quality assessment
4. **Opportunity Map** — what's missing, where it would go, expected impact
5. **Friction Audit** — conversion blockers identified
6. **Top 3 Quick Wins** — highest-impact, lowest-effort changes
