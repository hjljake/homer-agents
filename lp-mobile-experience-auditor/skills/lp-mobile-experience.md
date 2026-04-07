---
name: lp-mobile-experience
display_name: LP Mobile Experience Audit
description: Framework for auditing landing page mobile conversion performance — covers viewport rendering, tap target sizing, thumb-zone CTA placement, scroll depth efficiency, page speed, in-app browser compatibility, responsive stacking, and mobile form UX. Includes a 12-dimension scoring rubric (0-2 each, 24 points total) with traffic-type adaptations for cold and warm leads.
category: analysis
---

# Landing Page Mobile Experience Audit

Mobile isn't a "version" of the desktop page. It's the primary experience for the majority of landing page traffic. Paid social is 80-90% mobile. Email clicks are 60-70% mobile. SMS is 95%+ mobile. Retargeting is 70%+ mobile. Even paid search is now majority mobile.

A landing page that scores 90/100 on desktop but breaks on mobile is a 50. The mobile experience IS the experience for most visitors.

---

## Why Mobile Deserves Its Own Audit

The existing scorecard gives mobile 10 points out of 100 — enough to flag obvious problems, not enough to diagnose them. Mobile conversion has its own physics:

- **Thumb zones** dictate what gets tapped and what gets ignored
- **Viewport constraints** force hard prioritization — you can't show 6 elements above the fold
- **In-app browsers** (Gmail, Instagram, Facebook) render differently than Safari/Chrome
- **Scroll velocity** is higher on mobile — sections need to be shorter and punchier
- **Form input** is painful — every unnecessary field costs more on mobile than desktop
- **Network conditions** vary wildly — pages must be fast on 4G, not just WiFi
- **Orientation** changes can break layouts
- **Font rendering** differs across devices — what's readable on a 15" laptop is tiny on a 5.5" phone

This audit goes deep on each of these dimensions with specific, measurable criteria.

---

## The Three Viewport Breakpoints That Matter

Test every landing page on these three viewports. They cover 85%+ of mobile traffic:

| Device | Viewport | Why It Matters |
|--------|----------|----------------|
| iPhone SE / small Android | 375 x 667 | The smallest common screen. If it works here, it works everywhere. |
| iPhone 14/15 / mid Android | 390 x 844 | The most common viewport for iOS and close to mid-range Android. |
| Large phone / small tablet | 428 x 926 | iPhone Pro Max / large Android. Tests whether the layout stretches well. |

For each viewport, capture:
- What's visible above the fold (without scrolling)
- Whether the CTA is tappable without scrolling
- Whether text is readable without zooming
- Whether any element causes horizontal scroll

---

## Thumb Zone Map

The thumb zone determines what's easy vs. hard to tap on a phone held in one hand.

```
┌─────────────────────────┐
│     HARD TO REACH        │  Top 20% of screen
│     (top bar, nav)       │  Requires stretch or second hand
├─────────────────────────┤
│                          │
│     OK ZONE              │  Middle 30%
│     (content, secondary  │  Reachable but not natural
│      elements)           │
│                          │
├─────────────────────────┤
│                          │
│     NATURAL THUMB ZONE   │  Bottom 50%
│     (primary CTA, key    │  Easy one-handed reach
│      actions, sticky bar)│  THIS is where your CTA lives
│                          │
└─────────────────────────┘
```

**Implications for landing pages:**
- Primary CTA should be in the bottom 50% of the viewport OR in a sticky bottom bar
- Navigation and secondary links belong at the top (out of the way)
- Hamburger menus are fine — users know the pattern and they're in the stretch zone, reducing accidental taps
- Floating action buttons should be bottom-right (natural thumb position for right-handed users, 90% of population)

---

## Above-the-Fold Mobile Audit

On mobile, "above the fold" is roughly the top 600-700px. In that space, you must fit:

### Required elements (in priority order):
1. **Headline** — 28-36px, no more than 2 lines on the smallest viewport
2. **Subheadline** — 16-20px, no more than 3 lines
3. **Primary CTA** — full-width minus 32px margins, minimum 56px height
4. **One trust signal** — star rating, logo bar (compact), or customer count

### Acceptable to push below fold:
- Hero image (text first on mobile, always)
- Detailed subheadline or secondary copy
- Secondary CTA
- Video embed (show thumbnail, not autoplay)

### Must NOT be above the fold:
- Navigation menu (minimize or remove on landing pages)
- Large hero images that push the headline down
- Cookie consent banners that cover the CTA (use bottom-sheet style, not overlay)
- Chat widgets that obscure the CTA

### The Mobile First-Screen Test
Show someone the page on a phone for 3 seconds. Take it away. Ask:
1. What is this page about?
2. What should I do?
3. Do I trust it?

If they can't answer all three, the above-fold content needs work.

---

## Mobile Stack Ordering

When desktop layouts collapse to mobile, the ORDER elements stack matters enormously.

### Common stacking failures:
| Desktop Layout | Bad Mobile Stack | Good Mobile Stack |
|----------------|------------------|-------------------|
| Image left, text right | Image on top, text below (visitor sees image first, not value prop) | Text on top, image below |
| 3-column features | All three columns stacked, creating a wall of content | Accordion or horizontal swipe, showing one at a time |
| Sidebar CTA | CTA buried at the bottom after all content | Sticky bottom CTA bar |
| Logo bar (horizontal) | Logos stacked vertically, taking 3+ screens | Logos in 2x3 grid or horizontal scroll |
| Two-column pricing | Plans stacked, comparison lost | Tab interface or swipeable cards |
| Form + benefits side-by-side | Form below 3 screens of benefits | Benefits condensed, form prominent |

### Optimal mobile section structure:
```
[Minimal header — logo only, no nav on LP]
[Headline — largest text on screen]
[Subheadline — supporting detail]
[CTA button — full width]
[Trust signal — compact]
--- fold ---
[Section 1 — short, punchy, one key point]
[CTA repeat or anchor link]
[Section 2 — next key point]
[Social proof — 1-2 testimonials, not all of them]
[CTA repeat]
[FAQ — accordion style]
[Final CTA section]
[Minimal footer]
```

---

## Tap Target Specifications

### Size requirements:
| Element | Minimum Size | Recommended Size | Spacing Between |
|---------|-------------|------------------|-----------------|
| Primary CTA button | 48px height | 56-64px height | 16px from other tappable elements |
| Secondary buttons | 44px height | 48px height | 12px from other tappable elements |
| Text links | 44px tap area (even if text is smaller) | 48px tap area | 8px from other links |
| Form inputs | 44px height | 48-56px height | 8-12px between fields |
| Checkbox/radio | 44x44px tap area | 48x48px tap area | 12px between options |
| Close/dismiss buttons | 44x44px minimum | 48x48px | 8px from edges |
| Navigation items | 44px height | 48px height | 8px between items |

### Common tap target failures:
- Text links in body copy with no padding (tap area = text height only)
- Close buttons on modals that are too small or too close to the edge
- Form labels that don't expand the tap area of their associated input
- "Terms & Conditions" links that are 10px font with no padding
- Multiple links in a row (e.g., "Privacy Policy | Terms | Contact") with insufficient spacing

---

## Page Speed on Mobile

### Targets:
| Metric | Good | Needs Work | Poor |
|--------|------|------------|------|
| **Largest Contentful Paint (LCP)** | < 2.5s | 2.5-4.0s | > 4.0s |
| **First Input Delay (FID)** | < 100ms | 100-300ms | > 300ms |
| **Cumulative Layout Shift (CLS)** | < 0.1 | 0.1-0.25 | > 0.25 |
| **Time to Interactive (TTI)** | < 3.8s | 3.8-7.3s | > 7.3s |
| **Total page weight** | < 1.5MB | 1.5-3MB | > 3MB |

### Common speed killers on landing pages:
1. **Unoptimized hero images** — serve WebP/AVIF, compress, and set explicit width/height to prevent layout shift
2. **Third-party scripts** — analytics, chat widgets, personalization engines, heatmaps. Each one adds 100-500ms. Defer or lazy-load non-critical scripts.
3. **Web fonts** — use `font-display: swap` and preload critical fonts. Or use system fonts for body text.
4. **Video autoplay** — never autoplay on mobile. Show a thumbnail with a play button. Load the player on tap.
5. **Uncompressed CSS/JS** — minify and compress. Use code splitting to load only what the page needs.
6. **No lazy loading** — images below the fold should use `loading="lazy"`. Iframes (YouTube embeds, maps) should lazy-load too.
7. **Render-blocking resources** — move non-critical CSS to `<link rel="preload">` and defer non-critical JS.

### Speed testing tools:
- Google PageSpeed Insights (uses real user data + Lighthouse)
- WebPageTest (advanced, multi-location, throttled network testing)
- Chrome DevTools > Network tab with throttling enabled (3G/4G simulation)

---

## In-App Browser Compatibility

Warm traffic from email and social media often opens links in in-app browsers, not the system browser. These have different rendering engines and limitations.

### In-app browsers to test:
| App | Browser Engine | Known Issues |
|-----|---------------|--------------|
| Gmail (iOS) | WebKit (restricted) | Limited JavaScript, no service workers, some CSS animations break |
| Gmail (Android) | Chrome Custom Tab | Generally good, but cookies may not persist to main browser |
| Outlook (iOS/Android) | In-app WebView | Limited viewport, some layout breaks, cookie isolation |
| Instagram | In-app WebView | No address bar visible, limited navigation, some JS restricted |
| Facebook | In-app WebView | Cookie warnings may overlay content, tracking params appended |
| LinkedIn | In-app Chrome Tab | Generally good, but UTM handling can break |
| Apple Mail | Safari | Best rendering — uses full Safari engine |
| SMS links (iOS) | Safari | Opens in full Safari — best case |
| SMS links (Android) | Chrome/default browser | Opens in full browser — best case |

### In-app browser testing checklist:
- [ ] Page renders correctly (no layout breaks)
- [ ] All images load
- [ ] CTA buttons work (no JavaScript dependency for basic click)
- [ ] Forms submit successfully
- [ ] Personalization tokens render (not raw `{{first_name}}`)
- [ ] No cookie consent banner covering the entire screen
- [ ] Video plays (or gracefully shows thumbnail)
- [ ] External links open correctly (consider `target="_blank"` behavior)
- [ ] Page doesn't prompt for login when it shouldn't

---

## Mobile Form UX

Forms are where mobile conversions go to die. Every field is a friction point that costs more on mobile than desktop because typing on a phone is slower, error-prone, and frustrating.

### Field count impact on mobile conversion:
| Fields | Approximate Completion Rate Impact |
|--------|-----------------------------------|
| 1 (email only) | Baseline |
| 2 (name + email) | -5% to -10% |
| 3 (name + email + phone) | -15% to -25% |
| 4+ fields | -25% to -50%+ |

### Mobile form best practices:
1. **Minimize fields ruthlessly.** On mobile, 1-2 fields maximum for cold traffic. 2-3 for warm (and pre-fill what you can).
2. **Use correct input types.** `type="email"` for email (shows @ keyboard), `type="tel"` for phone (shows number pad), `inputmode="numeric"` for numbers.
3. **Enable autocomplete attributes.** `autocomplete="name"`, `autocomplete="email"`, `autocomplete="tel"` — let the browser fill in stored data.
4. **Full-width inputs.** Every input should span the full width minus page margins. No side-by-side fields on mobile.
5. **Visible labels above inputs.** Never use placeholder-only labels — they disappear when typing. Labels above, placeholders as hints.
6. **Generous input height.** 48-56px minimum for comfortable thumb tapping.
7. **Inline validation.** Show errors immediately after the user leaves a field, not after form submission. Use supportive language ("Please enter a valid email" not "Error: invalid input").
8. **Smart keyboard dismissal.** Tapping outside a field should dismiss the keyboard. The CTA should be visible when the keyboard is open (or use a sticky submit button).
9. **Progress indicators for multi-step.** If the form has multiple steps, show "Step 1 of 3" prominently. Each step should have 1-2 fields maximum.
10. **Pre-fill for warm leads.** If the visitor is logged in or came from a tracked email link, pre-fill every field you already have data for.

---

## Scroll Depth & Content Density

### Mobile scroll behavior:
- Mobile users scroll faster and further than desktop users
- But they also bounce faster if the first screen doesn't hook them
- Ideal mobile section length: 1-2 screens per section (not 3-4)
- Each section should make ONE point, with ONE supporting element

### Content density guidelines:
| Element | Desktop | Mobile |
|---------|---------|--------|
| Headline | 36-56px, up to 2 lines | 28-36px, up to 2 lines |
| Body paragraphs | 3-5 sentences | 2-3 sentences max |
| Bullet lists | 5-7 items | 3-5 items |
| Testimonials visible | 3 cards side by side | 1-2 stacked, or swipeable |
| Feature sections | Detailed with screenshots | Condensed with icons |
| FAQ items | All expanded or toggle | Accordion (collapsed by default) |
| Social proof logos | 6-8 in a row | 3-4 in a row, or 2x3 grid |

### Scroll depth benchmarks:
- **25% scroll** — most mobile visitors reach this. Your strongest content (after the hero) must be here.
- **50% scroll** — engaged visitors. Social proof and mid-page CTA should be here.
- **75% scroll** — highly interested. FAQ and objection handling belong here.
- **100% scroll** — intent visitors. Final CTA with urgency/guarantee.

---

## Cold vs Warm Mobile Differences

### Cold Traffic Mobile Priorities:
1. **Speed is survival.** Cold visitors from paid social have zero patience. Under 2.5s LCP or they're gone.
2. **Hero must do all the work.** The mobile first screen is your only guaranteed impression. Headline, subheadline, CTA, trust signal — all must be visible.
3. **Remove ALL navigation.** On mobile, a hamburger menu is tempting to tap. For cold traffic LPs, don't even show it.
4. **Social proof above the fold.** Even a compact "4.8 stars from 1,200 reviews" line makes a difference for cold visitors on mobile.
5. **Minimal form.** 1 field (email) for lead gen. 2 fields max. Every field on mobile costs 10-15% completion rate from cold visitors.
6. **Thumb-zone CTA.** The primary CTA should be in the natural thumb zone (bottom half of screen) or sticky at the bottom.

### Warm Traffic Mobile Priorities:
1. **In-app browser compatibility is critical.** 60-70% of warm traffic from email opens in Gmail/Outlook in-app browsers. Test in these specifically.
2. **Message match on first screen.** The email subject line's promise must be visible in the mobile hero without scrolling.
3. **Pre-fill everything.** If they clicked from a tracked email, you know who they are. Pre-fill name, email, and any other stored data.
4. **Shorter page.** Warm mobile visitors need less persuasion. Get to the offer, show the proof, present the CTA. 3-5 sections, not 8-10.
5. **Deep link behavior.** If the CTA should take them to an in-app experience (upgrade flow, account settings), make sure the deep link works from in-app browsers.
6. **Session continuity.** If they're logged in on their phone, the page should recognize them. No login prompts from email click-throughs.

---

## Mobile Scoring Rubric

Score each dimension 0-2 (0 = broken/missing, 1 = functional but not optimized, 2 = excellent).

| # | Dimension | 0 | 1 | 2 |
|---|-----------|---|---|---|
| 1 | **Viewport rendering** | Layout breaks, horizontal scroll, or elements overflow | Renders correctly but not optimized (e.g., desktop layout scaled down) | True responsive design — layout adapts intentionally to each breakpoint |
| 2 | **Above-fold completeness** | Headline or CTA not visible without scrolling | Most elements visible but CTA partially cut off or requires small scroll | Headline, subheadline, CTA, and trust signal all visible on first screen |
| 3 | **Tap target sizing** | Multiple buttons/links below 44px or with insufficient spacing | Most targets adequate, 1-2 tight spots | All interactive elements 48px+ with generous spacing |
| 4 | **Thumb-zone CTA placement** | Primary CTA in hard-to-reach zone (top of screen) only | CTA reachable but not in natural thumb zone | Primary CTA in natural thumb zone or sticky bottom bar |
| 5 | **Text readability** | Body text below 14px, requires zooming, lines too long | 16px body text but line length or contrast could improve | 16px+ body, comfortable line length (35-50 chars), strong contrast |
| 6 | **Image optimization** | Images cause layout shift, are uncompressed, or don't load | Images load but are not optimally sized/compressed for mobile | Images are responsive, compressed (WebP/AVIF), with explicit dimensions |
| 7 | **Page speed (LCP)** | LCP > 4 seconds on 4G | LCP 2.5-4 seconds | LCP < 2.5 seconds |
| 8 | **Content density** | Sections are too long, walls of text, no mobile adaptation | Some mobile optimization but sections still too dense | Short punchy sections, appropriate for mobile scroll behavior |
| 9 | **Stack ordering** | Images above headlines, CTA buried below long content sections | Mostly correct but 1-2 stacking issues | Text-first stacking, CTA prominent, logical mobile flow |
| 10 | **Form UX (if applicable)** | Wrong input types, tiny fields, too many fields, no autocomplete | Correct input types but could reduce fields or improve layout | Minimal fields, correct input types, autocomplete, full-width, pre-fill for warm |
| 11 | **In-app browser compatibility** | Page breaks in Gmail/Instagram/Facebook in-app browser | Minor rendering differences in some in-app browsers | Consistent experience across all major in-app browsers |
| 12 | **Scroll & navigation UX** | Sticky elements overlap content, no scroll indicators, broken accordions | Functional but scroll experience not polished | Smooth scroll, well-behaved sticky elements, intuitive mobile navigation |

**Total mobile score: ___ / 24**

### Score interpretation:
- **21-24: Mobile-first excellence.** This page was clearly designed mobile-first and works beautifully on all devices.
- **16-20: Solid mobile experience.** A few areas need polish but the fundamentals are strong.
- **11-15: Functional but not optimized.** The page works on mobile but isn't leveraging mobile-specific patterns. Conversion is being left on the table.
- **6-10: Significant mobile problems.** Multiple dimensions are failing. Mobile visitors are bouncing or struggling. Prioritize fixes by dimension score.
- **0-5: Mobile-hostile.** The page was designed for desktop and the mobile experience is broken. Rebuild with mobile-first approach.

---

## How to Use This Skill as an Agent

When auditing a landing page's mobile experience:

1. **Determine the primary mobile entry point.** Is the traffic from paid social (Instagram/Facebook in-app browser), email (Gmail/Outlook in-app browser), SMS (system browser), or paid search (Chrome/Safari)? This determines which rendering environment to prioritize.

2. **Audit the three viewports.** Check the page at 375px, 390px, and 428px widths. Note what breaks, what's cut off, and what looks wrong at each size.

3. **Run the first-screen test.** At each viewport, capture what's visible without scrolling. Is the headline, subheadline, CTA, and trust signal all visible? If not, what's pushing them down?

4. **Map the thumb zone.** Identify where the primary CTA sits relative to the thumb zone. Is it easy to tap one-handed?

5. **Test tap targets.** Identify every interactive element and estimate its tap area. Flag anything below 44px or with less than 8px spacing from adjacent tappable elements.

6. **Evaluate page speed.** Use PageSpeed Insights or equivalent to get Core Web Vitals. Flag LCP > 2.5s, CLS > 0.1, or total page weight > 1.5MB.

7. **Check in-app browser rendering.** If the traffic is from email or social, note any known compatibility issues with the relevant in-app browsers.

8. **Audit mobile form UX.** If there's a form, check: field count, input types, autocomplete attributes, label visibility, keyboard behavior, and pre-fill capability.

9. **Evaluate content density.** Is the content adapted for mobile reading patterns? Short sections, scannable, accordion FAQs, appropriately sized proof elements.

10. **Score using the 12-dimension rubric.** Score each dimension 0-2 with specific observations. For any dimension scoring 0 or 1, provide a specific fix with implementation details.

11. **Map to main scorecard impact.** Show how mobile improvements affect the main scorecard Section 5 (Mobile Experience, 10 pts for both cold and warm). Also note cross-impacts: mobile layout affects Section 1 (hero), mobile form UX affects Section 2 (below-fold/CTAs), and mobile speed affects Section 7 (technical).

12. **Prioritize by traffic source.** If 80% of traffic is from paid social, prioritize in-app browser compatibility and speed. If 80% is from email, prioritize in-app browser rendering and message match on first screen. If mixed, prioritize fundamentals (speed, tap targets, above-fold completeness).
