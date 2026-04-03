# On-Page SEO Technical Checklist

Use this checklist when reviewing or creating blog content for search optimization.

## Title Tag
- [ ] 50-60 characters (Google truncates at ~60)
- [ ] Primary keyword appears within the first 30 characters
- [ ] Contains a hook: number, "how to", power word, or bracket tag [2025 Guide]
- [ ] Unique across the site — no duplicate title tags

## Meta Description
- [ ] 150-155 characters (Google truncates at ~155)
- [ ] Includes primary keyword naturally
- [ ] Contains a value proposition or curiosity hook
- [ ] Includes a soft CTA ("Learn how...", "Discover why...")
- [ ] Unique across the site

## URL Structure
- [ ] Short: 3-5 words maximum
- [ ] Hyphenated, lowercase
- [ ] Contains primary keyword
- [ ] No stop words (a, the, of, in, for)
- [ ] No dates in URL (unless the content is inherently time-bound)
- Example: `/blog/saas-pricing-strategy` not `/blog/2026/04/the-ultimate-guide-to-saas-pricing-strategy`

## Header Hierarchy
- [ ] Exactly one H1 (the title)
- [ ] H2s for main sections — each targets a secondary keyword or search intent
- [ ] H3s for subsections within H2s
- [ ] No skipped levels (H2 → H3, never H2 → H4)
- [ ] At least one H2 is phrased as a question (matches People Also Ask)

## Content Body
- [ ] Primary keyword in first 100 words
- [ ] Keyword density 1-2% for primary, 0.5% for secondary
- [ ] Paragraphs 2-4 sentences max
- [ ] Bullet lists or numbered steps where applicable
- [ ] Table of contents for posts >1500 words
- [ ] No keyword stuffing — reads naturally aloud

## Internal Linking
- [ ] 2-5 internal links per 1000 words
- [ ] Anchor text is descriptive (not "click here")
- [ ] Links point to topically related content
- [ ] Most important pages get linked to most often (pillar content strategy)
- [ ] No orphan pages — every post should link to and be linked from at least one other post

## External Linking
- [ ] 1-3 external links per post
- [ ] Links to authoritative sources (.gov, .edu, industry reports, primary research)
- [ ] Opens in new tab (target="_blank")
- [ ] No links to direct competitors
- [ ] Nofollow affiliate or sponsored links

## Images & Media
- [ ] At least one image per post (hero image minimum)
- [ ] Alt text is descriptive and includes keyword where natural
- [ ] Image file names are descriptive (`saas-pricing-comparison.png` not `IMG_4521.png`)
- [ ] Images are compressed (<200KB for web)
- [ ] Lazy loading enabled for below-the-fold images

## Schema Markup (Structured Data)
- [ ] `Article` or `BlogPosting` schema on every post
- [ ] Includes: headline, author, datePublished, dateModified, image, publisher
- [ ] `FAQPage` schema if the post contains an FAQ section
- [ ] `HowTo` schema if the post is a step-by-step guide
- [ ] `BreadcrumbList` schema for navigation context
- [ ] Validate with Google's Rich Results Test before publishing

## Technical
- [ ] Page loads in <3 seconds (Core Web Vitals: LCP < 2.5s)
- [ ] Mobile-responsive layout
- [ ] Canonical URL set correctly
- [ ] No noindex tag (unless intentional)
- [ ] Open Graph and Twitter Card meta tags for social sharing
