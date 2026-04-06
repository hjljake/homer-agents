---
name: lp-layout-optimization
display_name: LP Layout Optimization
description: Framework for analyzing and optimizing landing page structure, visual hierarchy, section ordering, and content flow — covers page flow frameworks (PAS, AIDA, BAB), viewport optimization, CTA rhythm, mobile stacking, whitespace specifications, and distraction auditing.
category: analysis
---

# Landing Page Layout Optimization

Layout is the invisible architecture of conversion. Two pages with identical copy can convert at wildly different rates based on how that copy is arranged, spaced, and sequenced. Layout optimization ensures the right content appears at the right time in the visitor's scroll journey, with visual hierarchy that guides the eye toward the CTA.

---

## Why Layout Matters More Than Most Teams Think

A common mistake: optimizing copy while ignoring structure. The best headline in the world fails if:
- It's competing with 6 other elements for attention
- The CTA is below a wall of text nobody reads
- The social proof section appears AFTER the user has already decided to leave
- The mobile layout stacks elements in the wrong order
- Whitespace is so tight the page feels cramped and desperate

Layout is the delivery system for your content. Optimize the delivery system, and every piece of content on the page performs better.

---

## Page Flow Frameworks

Every landing page tells a story. The layout determines the order of that story. These frameworks describe proven narrative structures.

### PAS: Problem → Agitation → Solution

**Structure:**
```
[Hero: Name the problem]
    ↓
[Agitation: Show consequences of not solving it]
    ↓
[Solution: Present your offer as the answer]
    ↓
[Proof: Show it works]
    ↓
[CTA: Take action]
```

**Best for:** Problem-aware audiences, pain-point-driven products, cold traffic from search (they're actively looking for a solution).

**Section blueprint:**
1. **Hero** — headline names the problem, subheadline hints at the solution
2. **Pain section** — 3-4 specific consequences of the status quo, with emotional weight
3. **Bridge** — "There's a better way" transition
4. **Solution section** — your product/offer as the answer, presented as benefits
5. **Proof** — testimonials, case studies, numbers that validate the solution
6. **CTA** — clear action with risk reversal

### AIDA: Attention → Interest → Desire → Action

**Structure:**
```
[Hero: Grab attention with a bold claim or visual]
    ↓
[Interest: Explain what it is and why it matters]
    ↓
[Desire: Show outcomes, proof, benefits that make them want it]
    ↓
[Action: Remove barriers, present the CTA]
```

**Best for:** Product launches, brand-driven pages, audiences that need education before conversion.

**Section blueprint:**
1. **Hero** — attention-grabbing headline + visual, minimal text
2. **"How it works"** — 3-step process or feature walkthrough
3. **Benefits deep-dive** — 3-4 benefit sections with supporting visuals
4. **Social proof block** — concentrated proof section
5. **Offer/pricing** — what you get, what it costs
6. **FAQ / objection handling** — address remaining doubts
7. **Final CTA** — with urgency or guarantee framing

### BAB: Before → After → Bridge

**Structure:**
```
[Hero: Show the "before" state — where they are now]
    ↓
[After: Paint the "after" state — where they could be]
    ↓
[Bridge: Your product/offer is how they get from before to after]
    ↓
[Proof: Others have made this journey]
    ↓
[CTA: Start your journey]
```

**Best for:** Transformation products (courses, coaching, health, finance), aspirational audiences, warm traffic that needs to visualize the upgrade.

**Section blueprint:**
1. **Hero** — headline evokes the "before" pain, subheadline promises the "after"
2. **Before/after comparison** — visual or copy-based side-by-side
3. **The bridge** — how your solution makes the transformation possible
4. **Journey proof** — customer stories showing the before→after arc
5. **What you get** — specific deliverables/features
6. **CTA** — with transformation framing ("Start your transformation")

### Choosing a Framework

| Scenario | Recommended Framework |
|----------|----------------------|
| ICP is problem-aware, actively searching | PAS |
| ICP needs education before purchase | AIDA |
| Product is a transformation/upgrade | BAB |
| Cold traffic from paid search | PAS or AIDA |
| Cold traffic from paid social | BAB or AIDA |
| Warm traffic from email | BAB (they already know the before) |
| Warm traffic, upgrade/upsell | BAB (show before/after of current vs new plan) |

---

## Visual Hierarchy Principles

### The F-Pattern (Text-Heavy Pages)

Visitors scan in an F-shape:
1. First horizontal sweep across the top (headline)
2. Second horizontal sweep slightly lower (subheadline/first section)
3. Vertical scan down the left side (section headers, first words of paragraphs)

**Layout implications:**
- Put the most important information in the top-left quadrant
- Left-align headlines and body copy (don't center long text)
- Use strong section headers — they're the only thing most people read on the vertical scan
- Place CTAs on the left side or centered (not right-aligned)

### The Z-Pattern (Visual/Minimal Pages)

Visitors scan in a Z-shape:
1. Top-left to top-right (header/nav area)
2. Diagonal from top-right to bottom-left
3. Bottom-left to bottom-right (CTA area)

**Layout implications:**
- Logo/brand mark: top-left
- Navigation/secondary CTA: top-right
- Key visual or hero content: center (on the diagonal)
- Primary CTA: bottom-right of each section
- Works best for clean, image-forward pages with minimal copy

### The Squint Test

Blur your vision (or blur the page in Figma/Photoshop) and note:
1. What's the FIRST thing you see? (Should be the headline)
2. What's the SECOND thing? (Should be the CTA)
3. What's the THIRD thing? (Should be the primary proof element)

If the order is wrong, the visual hierarchy needs fixing. Common fixes:
- Increase headline font size / weight
- Increase CTA contrast (color, size, whitespace)
- Reduce visual weight of competing elements (tone down images, reduce font weight of non-headline text)

---

## Section-by-Section Layout Specifications

### Hero Section

| Element | Desktop | Mobile |
|---------|---------|--------|
| **Minimum height** | 600-700px (full viewport recommended) | 500-600px (first screen) |
| **Headline font size** | 36-56px (responsive) | 28-36px |
| **Subheadline font size** | 18-24px | 16-20px |
| **CTA button height** | 48-56px | 56px (larger for thumb) |
| **CTA button width** | 200-320px | Full-width minus 32px margins |
| **Whitespace above CTA** | 24-32px | 20-28px |
| **Maximum elements** | 5-6 (headline, subhead, CTA, proof snippet, visual, nav) | 4-5 (headline, subhead, CTA, proof snippet — visual may be below fold) |

**Hero layout patterns:**
- **Split hero:** Left text, right image/video (60/40 split). Best for product-visual pages.
- **Full-width hero:** Centered text over background image/gradient. Best for bold brand statements.
- **Video hero:** Full-width background video with text overlay. Use sparingly — slows page load.
- **Minimal hero:** Text-only, large typography, no image. Best for copy-driven offers.

### Proof Block

**Placement:** Immediately after hero or within hero (logo bar).

| Pattern | When to Use |
|---------|-------------|
| **Logo bar in hero** | B2B, enterprise — show 4-6 recognizable logos |
| **Star rating in hero** | Consumer, SaaS — "4.8/5 from 1,200 reviews" |
| **Testimonial strip below hero** | Services — 2-3 short quotes in a horizontal row |
| **Full proof section** | Any — dedicated section with mixed proof types |

**Spacing:** Proof should have 40-60px separation from surrounding content. It needs room to breathe — cramped proof looks manufactured.

### "How It Works" Section

**Placement:** First or second section after hero.

**Optimal layout:**
- 3 steps (3 is the magic number — more feels complex)
- Horizontal on desktop (3 columns), vertical on mobile (stacked)
- Each step: icon/number → short title → 1-2 sentence description
- Arrow or connector between steps (shows progression)
- Optional: screenshot or visual for each step

**Sizing:** 60-80px step numbers/icons. 18-20px step titles. 14-16px descriptions.

### Benefits / Features Section

**Placement:** Middle of page, after "how it works" or proof.

**Layout options:**
- **Alternating rows:** Image left/text right, then text left/image right. Creates visual rhythm. 2-4 rows.
- **Icon grid:** 3x2 or 2x3 grid of benefit cards with icon + title + description. Good for feature-heavy pages.
- **Single column:** Stacked benefit blocks with visual left and text right. Best for mobile-first pages.

**Each benefit should follow the formula:** Feature → Outcome → Proof. "AI-powered analysis (feature) → know exactly which changes will increase conversions (outcome) → average 34% lift for our customers (proof)."

### Testimonial Section

**Placement:** After benefits, before final CTA.

**Layout options:**
- **3-column cards:** Photo + name + title + quote. Best for 3 strong testimonials.
- **Single featured testimonial:** Large quote with photo and full attribution. Best for one powerful story.
- **Carousel:** Use only if you have 5+ testimonials. Most users never interact with carousels — show the best ones static.
- **Video testimonial:** Embedded video with play button. Highest impact but slowest to load.

**Minimum requirements:** Real name, real photo, real title/company. Anonymous testimonials have near-zero impact.

### CTA Section (Final)

**Placement:** Bottom of page, after all content.

**Layout:**
- Centered, full-width background (different from page background — creates visual break)
- Headline that summarizes the value proposition (different wording from hero)
- CTA button (same style as hero CTA — consistent)
- Supporting text: guarantee, risk reversal, or urgency
- Minimal: no more than 5 elements total

---

## CTA Placement Rhythm

CTAs should appear at "decision points" — moments in the scroll where the visitor has received enough information to act.

**Recommended CTA placement:**

```
[Hero CTA]                     ← After seeing the value proposition
    ↓
  2-3 sections of content
    ↓
[Mid-page CTA]                 ← After proof or "how it works"
    ↓
  2-3 sections of content
    ↓
[Final CTA section]            ← After all objections handled
```

**3 CTAs is the sweet spot** for most landing pages. Less than 2 = some visitors miss the CTA. More than 4 = CTA fatigue / banner blindness.

**CTA copy can vary slightly** to match the reader's position:
- Hero CTA: "See How It Works" (low commitment — they haven't seen proof yet)
- Mid-page CTA: "Get Started Free" (medium commitment — they've seen proof)
- Final CTA: "Start Your Free Trial Now" (highest commitment — they've seen everything)

---

## Above-the-Fold Optimization

### What Must Be Above the Fold

On desktop (top ~700px) and mobile (top ~600px):
1. **Headline** — always
2. **Subheadline** — always
3. **Primary CTA** — always
4. **One trust element** — logo bar, star rating, or customer count
5. **Primary visual** — product screenshot, hero image, or video thumbnail

What should NOT be above the fold:
- Long paragraphs of text
- Feature lists
- Multiple competing CTAs
- Form fields (unless the page's sole purpose is form completion)
- Navigation menus on landing pages (remove or minimize)

### Mobile First-Screen Audit

On mobile, the "above the fold" is even more constrained. Test on actual devices:
- iPhone SE (375 x 667): smallest common viewport
- iPhone 14/15 (390 x 844): most common iOS viewport
- Android mid-range (360 x 800): most common Android viewport

For each device, verify:
- [ ] Headline fully visible without scrolling
- [ ] Subheadline fully visible
- [ ] CTA fully visible and tappable
- [ ] No horizontal scrolling
- [ ] Text is readable without zooming

---

## Mobile Layout Stack Ordering

On mobile, horizontal elements stack vertically. The ORDER they stack matters.

### Common stacking mistakes:
- Image stacks ABOVE the headline (visitor sees a generic image first, not the value proposition)
- CTA stacks below 3 paragraphs of text (buried)
- Logo bar takes up the entire first screen (no headline visible)

### Optimal mobile stack order:
```
1. Headline (largest text)
2. Subheadline
3. CTA button (full-width)
4. Trust element (logo bar or star rating — compact)
5. Hero image (if needed — can be below fold on mobile)
```

### Desktop vs Mobile Layout Differences

| Desktop | Mobile |
|---------|--------|
| Split layouts (text + image side by side) | Stack vertically, text always first |
| 3-column benefit grids | Single column, stacked |
| Horizontal testimonial cards | Stacked cards or carousel |
| Fixed sidebar CTAs | Sticky bottom CTA bar |
| Hover effects on buttons | No hover — tap-friendly sizing |
| Multi-column forms | Single column forms, full-width inputs |

---

## Whitespace Specifications

Whitespace is not empty space — it's the space that makes content readable and the CTA findable.

### Minimum Spacing Rules

| Between... | Minimum | Recommended |
|-----------|---------|-------------|
| Major page sections | 60px | 80-120px |
| Section header and first content | 24px | 32-40px |
| Paragraphs | 16px | 20-24px |
| CTA button and surrounding elements | 24px | 32-48px |
| Form fields | 12px | 16-20px |
| Testimonial cards | 20px | 24-32px |
| Logo bar items | 32px | 40-60px |
| Page edge and content (desktop) | 40px | 80-120px |
| Page edge and content (mobile) | 16px | 20-24px |

### Content Width

- **Maximum content width:** 1200px (wider = lines become too long to read)
- **Optimal line length:** 50-75 characters per line
- **Hero headline:** Can be wider, up to 900px, for visual impact
- **Body copy blocks:** 600-700px max width for readability
- **Full-bleed sections:** Background extends to edges, content stays within max-width

---

## Navigation & Distraction Audit

### The Rule: Every Exit Point Is a Leak

On a landing page, every link that isn't the CTA is a potential exit. Audit and remove:

**Remove entirely:**
- [ ] Full site navigation (header menu)
- [ ] Footer links to other pages (about, blog, careers)
- [ ] Social media links
- [ ] "Read more" links to blog posts
- [ ] Sidebar content
- [ ] Pop-ups that compete with the page CTA

**Keep but minimize:**
- [ ] Logo (can link to homepage, but consider making it non-clickable)
- [ ] Privacy policy / terms (required, but put in a small footer)
- [ ] Trust badge links (security certifications — they open in new tabs)

**Exceptions:**
- Product pages within a larger site (keep nav for browsing)
- Long-form sales pages (table of contents for navigation within the page)
- Pricing pages (comparison may need internal links)

### The Navigation Test

Look at the page. Count every clickable element that is NOT the primary CTA.
- **0-2 non-CTA links:** Excellent focus
- **3-5 non-CTA links:** Acceptable, but review each one
- **6+ non-CTA links:** Every link is leaking conversions. Cut ruthlessly.

---

## Cold vs Warm Layout Differences

### Cold Lead Layout Priorities

1. **Trust-heavy early sections.** Social proof should appear within the first 2 sections after the hero. Cold visitors need trust established before they'll read further.
2. **"How it works" early.** Cold visitors need to understand the mechanism before they'll consider acting. Place within the first 3 sections.
3. **Remove ALL navigation.** Cold visitors from paid ads should have ONE path: read → convert. No distractions.
4. **FAQ section before final CTA.** Cold visitors have more objections that need addressing.
5. **Risk reversal prominence.** Guarantee/trial offer should be visible in at least 2 places.

**Recommended cold lead section order:**
```
Hero → Proof/logos → How it works → Benefits → Testimonials → FAQ → Final CTA
```

### Warm Lead Layout Priorities

1. **Offer-details early.** Warm visitors already trust you — they want to know the specifics of THIS offer. Lead with what they get, not why you're credible.
2. **Comparison sections.** If it's an upgrade/upsell, show current vs. proposed side by side. Warm visitors are evaluating a specific decision.
3. **Navigation can stay minimal.** Warm visitors may want to explore adjacent pages (pricing, features, docs). A minimal nav is OK.
4. **Personalized content blocks.** If possible, show segment-specific content based on their profile.
5. **Shorter pages OK.** Warm visitors don't need as much persuasion. The page can be more focused and compact.

**Recommended warm lead section order:**
```
Hero → Offer details → Comparison → Peer proof → FAQ → Final CTA
```

---

## Layout Scoring Rubric

When auditing a landing page layout, score these 8 dimensions:

| Dimension | 0 | 1 | 2 |
|-----------|---|---|---|
| **Section ordering** | Random or illogical flow | Mostly logical but some sections misplaced | Perfect narrative flow — each section answers the next question |
| **Visual hierarchy** | Fails squint test — unclear what's most important | Partially clear but competing elements | Perfect hierarchy: headline > CTA > proof > everything else |
| **Above-fold content** | Missing headline, CTA, or both | Most elements present but cramped or cut off | Complete: headline, subheadline, CTA, trust element, all visible |
| **CTA rhythm** | 0-1 CTA on the page | 2 CTAs but not at decision points | 3+ CTAs at natural decision points |
| **Whitespace** | Cramped, elements touching, no breathing room | Adequate but inconsistent | Spacious, intentional, consistent throughout |
| **Mobile layout** | Broken or poorly stacked on mobile | Functional but not optimized | Perfect mobile stack order, thumb-friendly, fast-loading |
| **Distraction level** | 6+ non-CTA links, full navigation, competing elements | 3-5 non-CTA elements | 0-2 non-CTA links, zero distractions |
| **Content density** | Either wall-of-text or so sparse there's nothing to read | Uneven — some sections dense, others empty | Balanced: enough content to convince, enough space to breathe |

**Total layout score: ___ / 16**

---

## How to Use This Skill as an Agent

When analyzing landing page layout:

1. **Identify the current page flow framework.** Is the page following PAS, AIDA, BAB, or no recognizable framework? If no framework, the first recommendation should be to restructure around one.

2. **Run the squint test.** Describe what you see first, second, third when the page is "blurred." Compare to the ideal hierarchy (headline > CTA > proof).

3. **Audit above-the-fold content.** List exactly what's visible on desktop and mobile without scrolling. Flag anything missing from the required list (headline, subheadline, CTA, trust element).

4. **Map the CTA rhythm.** List every CTA on the page, its position (which section), and its copy. Is there a CTA at every decision point? Are there too many?

5. **Measure whitespace (approximate).** Note any sections where elements are too close, or where there's too much empty space with no content.

6. **Audit distractions.** Count every non-CTA clickable element. For each, determine: does this HELP conversion or HURT conversion?

7. **Evaluate mobile stacking.** Describe the mobile layout stack order. Flag any issues (image above headline, CTA buried, etc.).

8. **Score using the rubric.** Score each of the 8 dimensions 0-2. Provide specific observations for each score.

9. **Generate recommendations.** For each dimension scoring 0 or 1, provide:
   - What's wrong (specific observation)
   - What to change (specific recommendation with placement details)
   - Wireframe-style description of the proposed layout change
   - Projected score improvement
   - Priority level (high/medium/low based on conversion impact)

10. **Map to scorecard sections.** Show how layout improvements affect scorecard scores: hero section (visual hierarchy, CTA visibility), below-fold (section ordering, momentum), mobile experience (stacking, tap targets), and brand/design (whitespace, visual hierarchy).
