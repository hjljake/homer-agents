---
name: cta-optimization
display_name: CTA Optimization
description: Conversion CTA frameworks — copy formulas, placement strategy, design principles, industry patterns, psychology, A/B testing, and anti-patterns for optimizing calls-to-action across full websites
category: planning
---

# CTA Optimization

When analyzing and optimizing calls-to-action across a website, apply these frameworks and principles.

## Definitions

- **Primary CTA:** The single most important action you want the visitor to take on a given page. Every page should have exactly one primary CTA.
- **Secondary CTA:** An alternative action for visitors not ready for the primary (e.g., "Learn more" vs "Buy now").
- **Sticky CTA:** A CTA that remains visible as the user scrolls (fixed header bar, floating button, sticky footer).
- **Inline CTA:** A CTA embedded within page content (mid-article, between sections).
- **Exit-intent CTA:** Triggered when the user's cursor moves toward the browser close/back button.
- **Ghost CTA:** A CTA that exists but is visually buried — low contrast, small size, below the fold with no scroll cue.

## CTA Anatomy

Every effective CTA has four components:

1. **Copy** — what the button/link says
2. **Placement** — where it sits on the page and in the user journey
3. **Design** — color, size, shape, contrast, whitespace
4. **Context** — the surrounding copy, imagery, and trust signals that support the action

Optimizing only one component without considering the others produces weak results. All four must work together.

## Copy Formulas

### The Core Formula
**Action Verb + Value Proposition**

Good: "Start my free trial" / "Get your custom plan" / "Download the guide"
Bad: "Submit" / "Click here" / "Learn more" (no value)

### First-Person vs Second-Person

| Voice | Example | Best For |
|---|---|---|
| First-person ("my") | "Start my free trial" | SaaS, subscriptions, personal services |
| Second-person ("your") | "Get your custom plan" | E-commerce, professional services |
| Imperative | "Shop the collection" | Retail, fashion, lifestyle |

First-person copy outperforms second-person by 25-90% in most A/B tests (Unbounce, ContentVerve studies). Default to first-person unless brand voice strongly dictates otherwise.

### Power Words by Intent

| Intent | Words | Example |
|---|---|---|
| Urgency | Now, Today, Instant, Limited | "Get instant access" |
| Value | Free, Save, Exclusive, Bonus | "Save 20% today" |
| Safety | Guaranteed, Risk-free, No commitment | "Try risk-free for 30 days" |
| Curiosity | Discover, Unlock, Reveal, See how | "Discover your plan" |
| Simplicity | Easy, Quick, In minutes, One-click | "Set up in 5 minutes" |

### Copy Length

- **Buttons:** 2-5 words. Longer buttons have lower click rates.
- **Supporting text (below button):** 1 short sentence max. "No credit card required." / "Cancel anytime." / "Join 10,000+ businesses."
- **Avoid:** Full sentences on buttons, jargon, passive voice.

### What NOT to Write

- "Submit" — the worst-performing CTA word. Implies the user is giving something up.
- "Click here" — meaningless, not accessible, provides no value signal.
- "Buy now" on a landing page where the user hasn't seen value yet — too aggressive too early.
- ALL CAPS — reads as shouting; use title case or sentence case.
- Multiple exclamation marks — damages credibility.

## Placement Strategy

### Above the Fold (Critical)

The primary CTA must be visible without scrolling on both desktop and mobile. This is non-negotiable for:
- Homepage
- Landing pages
- Product pages
- Pricing pages

"Above the fold" on mobile is approximately the top 600px. On desktop, approximately top 700px. Test on actual devices.

### The Scroll Pattern

For longer pages, repeat the CTA at natural decision points:

```
[Hero section — Primary CTA]
     |
[Value proposition / features]
     |
[Social proof section]
     |
[Mid-page CTA repeat — same or slightly varied copy]
     |
[Detailed info / FAQ / objection handling]
     |
[Final CTA — often with urgency or guarantee framing]
```

3 CTA instances on a long page is the sweet spot. More than 4 creates "banner blindness" where users stop noticing them.

### Placement by Page Type

| Page | Primary CTA | Placement Notes |
|---|---|---|
| Homepage | Main value prop action | Hero section, above fold. Secondary CTA for "learn more" path. |
| Product page | Add to cart / Buy | Near price, sticky on mobile. Supporting trust signals adjacent. |
| Landing page | Single conversion goal | Hero + mid-page + bottom. Remove navigation to reduce exits. |
| Blog post | Related product/service or email signup | Inline after 2-3 paragraphs + end of post. Not in hero (they came to read). |
| Pricing page | Plan selection | One CTA per plan. Highlight recommended plan. |
| About page | Contact/demo request | After the story section, where trust is highest. |

### Sticky CTAs

When to use:
- Product pages (sticky "Add to Cart" on mobile)
- Landing pages with long-form content
- Pricing pages (sticky plan comparison header)

When NOT to use:
- Blog content (distracting, hurts reading experience)
- Information pages where no immediate action is expected
- When combined with other sticky elements (nav + sticky CTA = too much chrome)

Sticky placement:
- **Mobile:** Bottom of screen (thumb-friendly). Height: 56-64px max.
- **Desktop:** Top bar or floating element in lower-right corner. Not both.

### Exit-Intent

Use sparingly — one exit-intent per session maximum. Best for:
- Discount offers on e-commerce
- Lead magnets on content sites
- Cart abandonment saves

Never use on:
- Checkout pages (distracting during payment)
- Pages where the user is already engaged (reading, filling a form)
- Mobile (exit-intent detection is unreliable on mobile)

## Design Principles

### Contrast

The CTA must be the highest-contrast element on the page. If your site is blue-themed, the CTA should NOT be blue.

**The 3-Second Test:** If someone glances at the page for 3 seconds, the CTA should be the first thing they remember seeing.

Methods:
- Complementary color (opposite on the color wheel from the dominant page color)
- Size contrast (significantly larger than surrounding elements)
- Whitespace isolation (padding around the CTA so it doesn't blend into content)

### Button Sizing

| Context | Minimum Size | Recommended |
|---|---|---|
| Desktop primary CTA | 44px height | 48-56px height, 200-300px width |
| Mobile primary CTA | 48px height (Apple HIG) | 56px height, full-width or near-full-width |
| Secondary CTA | 36px height | 40-44px height |
| Inline text CTA | N/A | Underlined, different color, clear hover state |

Touch targets on mobile must be at least 48x48px (Google), ideally 56px+. Anything smaller causes mis-taps and frustration.

### Shape & Style

- **Rounded corners** (4-8px radius) outperform sharp corners in most tests
- **Drop shadow** or subtle border helps the button "lift" off the page
- **Filled buttons** for primary CTAs, **outline buttons** for secondary
- **Arrow icons** (→) after CTA text can increase click-through 2-5%
- **Loading states** — always show feedback after click (spinner, checkmark)

### Whitespace

Minimum 24px padding around the CTA on all sides. The CTA should never touch or overlap with:
- Navigation elements
- Other buttons
- Dense text blocks
- Image edges

### Mobile-Specific Design

- Full-width or near-full-width buttons on mobile (with 16px side margins)
- Thumb zone: primary CTA should be in the lower 40% of the screen (reachable with one hand)
- Stack CTAs vertically on mobile (never side-by-side)
- Minimum 12px gap between stacked buttons to prevent mis-taps
- Text size: 16px minimum on buttons (prevents iOS zoom on focus)

## Industry-Specific Patterns

### E-Commerce / Retail
- "Add to Cart" near price, with "Buy Now" as secondary for impulse purchases
- Free shipping threshold CTA: "Add $X more for free shipping"
- Product page CTAs should include: price, variant selection, quantity near the button
- Mobile: sticky "Add to Cart" that appears after scrolling past the product image

### SaaS / Software
- "Start free trial" with "No credit card required" supporting text
- Pricing page: one CTA per tier, recommended tier visually highlighted
- Demo request CTA for enterprise (secondary path alongside self-serve)
- In-app upgrade CTAs at feature gates

### Professional Services (Consulting, Legal, Medical)
- "Book a consultation" or "Schedule a call" — relationship-first language
- Phone number as CTA (click-to-call on mobile) alongside form-based CTA
- Trust signals critical: credentials, testimonials, case studies adjacent to CTA
- Avoid urgency tactics — feels inappropriate for high-trust services

### Local Business
- "Call now" (click-to-call) as primary mobile CTA
- "Get directions" as secondary (links to maps)
- "Book online" if booking system exists
- Hours of operation visible near CTA (reduces friction: "Are they even open?")

### Content / Media / Education
- "Subscribe" or "Get the newsletter" with preview of what they'll receive
- Lead magnets: "Download the [specific thing]" beats "Sign up" every time
- Course CTAs: "Enroll now" with price and "30-day guarantee" supporting text
- Free tier CTA should be prominent; paid tier CTA uses contrast/urgency

## CTA Audit Checklist

When analyzing existing CTAs on a website, evaluate each against:

### Visibility
- [ ] Primary CTA is above the fold on desktop
- [ ] Primary CTA is above the fold on mobile
- [ ] CTA has sufficient color contrast against background (WCAG AA minimum: 4.5:1 for text)
- [ ] CTA is not competing with other visual elements of equal weight
- [ ] CTA is visible without interacting with any modal, drawer, or accordion

### Copy
- [ ] Uses action verb + value proposition (not "Submit" or "Click here")
- [ ] Is 2-5 words
- [ ] Matches the visitor's intent at this point in the journey
- [ ] Supporting text addresses the #1 objection ("No credit card required", "Free shipping", etc.)

### Design
- [ ] Button meets minimum touch target (48px height mobile, 44px desktop)
- [ ] Has adequate whitespace/padding around it (24px minimum)
- [ ] Filled style for primary, outline for secondary (clear hierarchy)
- [ ] Hover/focus state is visible and provides feedback
- [ ] Loading/success state exists after click

### Placement
- [ ] Appears at natural decision points (not randomly placed)
- [ ] Repeated appropriately on long pages (2-3 instances)
- [ ] Not buried below excessive content before any CTA appears
- [ ] Mobile placement is thumb-friendly (lower 40% of screen for sticky)

### Context
- [ ] Surrounding content builds toward the action (value prop, social proof, objection handling)
- [ ] Trust signals are adjacent (reviews, guarantees, security badges)
- [ ] No distracting elements compete for attention near the CTA
- [ ] Page has a clear visual hierarchy leading the eye to the CTA

### Red Flags
- [ ] Multiple competing primary CTAs on the same viewport (pick one)
- [ ] CTA color matches the site's dominant color (no contrast)
- [ ] CTA below a wall of text with no visual break
- [ ] "Submit" or "Click here" as button text
- [ ] No CTA visible above the fold
- [ ] Pop-ups or modals that obscure the CTA
- [ ] Different CTAs competing for the same action ("Buy Now" + "Add to Cart" + "Purchase" all visible)

## A/B Testing Framework for CTAs

### What to Test (Priority Order)

1. **Copy** — highest impact, lowest effort. Test value prop, voice (my vs your), power words.
2. **Placement** — above fold vs below, sticky vs static, inline vs isolated.
3. **Color** — contrast against page, warm vs cool, brand vs high-contrast accent.
4. **Size** — larger buttons generally win, but test to find the ceiling.
5. **Supporting text** — "No credit card required" vs "Join 10,000+ businesses" vs no text.

### Test Design

- Change ONE variable per test
- Run for minimum 2 full business cycles (typically 2-4 weeks)
- Need 100+ conversions per variant for statistical significance at 95% confidence
- Use the existing conversion rate to calculate required sample size
- Don't end tests early on positive results — wait for full sample

### Common Test Outcomes

| Test | Typical Winner | Lift Range |
|---|---|---|
| "Start my free trial" vs "Start your free trial" | First-person | 10-40% |
| "Submit" vs [value-based copy] | Value-based | 20-90% |
| Above fold vs below fold | Above fold | 15-50% |
| High contrast vs low contrast button | High contrast | 10-30% |
| With supporting text vs without | With supporting text | 5-25% |
| Sticky CTA vs static (mobile) | Sticky | 10-20% |

## Anti-Patterns to Avoid

- **The "Submit" button:** Worst-performing CTA word. Always replace.
- **The invisible CTA:** Same color as the page, small, buried in content. Ghost CTAs convert at near-zero.
- **CTA overload:** More than 2 distinct actions per page viewport causes decision paralysis.
- **The bait-and-switch:** CTA says "Free trial" but the next page asks for payment info with no trial.
- **The moving target:** CTAs that shift position as the page loads (layout shift). Causes mis-clicks and frustration. Cumulative Layout Shift (CLS) should be <0.1.
- **The guilt trip:** "No thanks, I don't want to grow my business" dismiss copy. Manipulative and damages trust.
- **The hidden dismiss:** Pop-up CTAs where the X or "no thanks" option is hard to find. Violates FTC guidelines and annoys users.
- **The premature ask:** Asking for a high-commitment action (buy, subscribe) before establishing any value. Match CTA commitment level to page position in the funnel.
- **Inconsistent language:** Homepage says "Get Started", pricing says "Sign Up", header says "Try Free". Pick one phrase and use it everywhere.
