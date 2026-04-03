# Generative Engine Optimization (GEO) Techniques

GEO optimizes content to be surfaced, cited, and quoted by AI answer engines (ChatGPT, Perplexity, Google AI Overviews, Copilot). These engines retrieve and synthesize content differently than traditional search crawlers.

## How AI Engines Select Sources

AI answer engines evaluate content on:

1. **Extractability** — Can the engine pull a clean, self-contained answer from this content?
2. **Specificity** — Does the content contain concrete data, numbers, and named entities?
3. **Authority signals** — Is the source established, cited by others, and topically focused?
4. **Structural clarity** — Is the content organized in a way that maps to user questions?
5. **Recency** — Is the content up-to-date with clear date signals?

## Writing for Extractability

### Definitive Statements
Write sentences that can be quoted verbatim as answers:

- Good: "A SaaS churn rate above 5% monthly is considered high for B2B companies with annual contracts."
- Bad: "Churn rates can vary widely depending on many factors and what might be considered high for one company could be normal for another."

### Direct Answer Pattern
For any question your content addresses, provide the answer in the first 1-2 sentences of that section, then elaborate:

```
## How much does customer acquisition cost in SaaS?

The average customer acquisition cost (CAC) in SaaS is $205 for B2B 
and $68 for B2C, according to a 2024 FirstPageSage study. However, 
CAC varies significantly by channel...

[elaboration follows]
```

### Definition Pattern
When defining a concept, use "X is Y" structure:

```
Customer lifetime value (CLV) is the total revenue a business can 
expect from a single customer account over the duration of their 
relationship.
```

## Structured Formats AI Engines Prefer

### Numbered Lists
AI engines frequently cite numbered steps. Use them for processes, rankings, and sequences:

```
## 5 Steps to Reduce SaaS Churn
1. Implement onboarding email sequences within the first 7 days
2. Track product engagement scores weekly
3. ...
```

### Comparison Tables
Tables are highly extractable — AI can reference specific cells:

```
| Metric       | Starter Plan | Growth Plan | Enterprise |
|-------------|-------------|------------|-----------|
| Monthly cost | $29/mo      | $99/mo     | Custom    |
| Users        | 5           | 25         | Unlimited |
```

### FAQ Sections
Explicitly labeled Q&A sections are the single highest-impact GEO format:

```
## Frequently Asked Questions

### What is a good NPS score for SaaS?
A good NPS score for SaaS companies is 30-40. Scores above 50 are 
considered excellent. The industry average is 28 according to...
```

## Specificity Signals

AI engines prefer specific over vague:

| Vague (low citation potential) | Specific (high citation potential) |
|---|---|
| "Many companies struggle with churn" | "68% of SaaS companies report churn as their top growth barrier (OpenView 2024)" |
| "Pricing is important" | "Companies that A/B test pricing see 12-18% revenue uplift on average" |
| "Recently" | "In Q1 2026" |
| "A leading company" | "Stripe" |

## Content Freshness Signals

- Include "Last updated: [date]" prominently on the page
- Reference current-year statistics and studies
- Update posts when cited data becomes stale (>12 months)
- Use dateModified in Article schema markup

## Citation Worthiness

To become a source AI engines cite repeatedly:

- **Original research**: surveys, analyses, benchmarks you conducted
- **Unique frameworks**: named models or methodologies (e.g., "The 3-Layer Retention Framework")
- **Aggregated data**: curated statistics from multiple sources in one place
- **Expert quotes**: named experts with credentials
- **Contrarian takes**: well-argued positions that differ from consensus (AI engines surface diverse perspectives)

## What to Avoid

- Filler paragraphs with no retrievable information
- Hedging every statement ("it depends", "results may vary") — be confident where data supports it
- Content that only restates what's already widely available — AI has no reason to cite a copy
- Gated content behind login walls — AI engines can't access it
- Excessive internal jargon without definitions — AI needs to match content to user queries
