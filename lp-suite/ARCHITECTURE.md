# Homer Agents — Architecture

## Agent Inventory

```
homer-agents/
├── blog-post-writer-agent/            Single agent — research + write 3 blog variants
├── cta-specialist/                    3-agent workflow — audit CTAs, research, build plan
├── upsell-advisor/                    3-agent workflow — gather context, research, deepen strategy
├── website-setup-advisor/             Single agent — platform recommendation + setup guide
│
│   LANDING PAGE SUITE (9 unified agents — each handles both cold + warm traffic)
├── lp-scorecard-analyzer/             Standalone — score LP against traffic-appropriate scorecard (100 pts)
├── lp-headline-optimizer/             Standalone — generate optimized headline/subheadline combos
├── lp-icp-optimizer/                  Standalone — audit every element against the ICP
├── lp-layout-optimizer/               Standalone — analyze structure, hierarchy, CTA rhythm
├── lp-cta-optimizer/                  Standalone — audit all CTAs, generate variants + rhythm map
├── lp-social-proof-optimizer/         Standalone — catalog proof, score, generate sourcing plan
├── lp-mobile-experience-auditor/      Standalone — deep 12-dimension mobile audit
├── lp-copy-full-page-writer/          Standalone — write complete LP copy from scratch (no existing page needed)
├── lp-ab-variant-builder/             Standalone — synthesize all optimizer outputs into 2 A/B variants
```

---

## Standalone LP Agents — KB Data Flow

The 9 LP agents share data via the Knowledge Base. Each agent saves structured output with predictable titles and YAML headers. Downstream agents discover upstream data via `references.searches`. All agents handle both cold and warm traffic via a `traffic_type` question.

```
┌─────────────────────────────────────────────────────────────────────┐
│                  STANDALONE LP AGENT DATA FLOW                      │
│           (each agent handles both cold and warm traffic)           │
│                                                                     │
│  Each agent runs independently. Users see them as separate tools.   │
│  Behind the scenes, they discover each other's outputs via KB.      │
└─────────────────────────────────────────────────────────────────────┘

  ┌──────────────────────┐
  │  SCORECARD ANALYZER  │  Fully standalone — no upstream dependency
  │                      │
  │  User provides:      │
  │  • LP URL            │
  │  • Traffic type      │
  │  • Traffic source    │
  │  • Page goal         │
  │                      │
  │  Saves to KB:        │
  │  "LP Scorecard       │
  │   Analysis: {biz}    │
  │   — {lead_type}      │
  │   — {date}"          │
  │                      │
  │  YAML: type:         │
  │  lp-scorecard-       │
  │  analysis            │
  └──────────┬───────────┘
             │
             │  KB semantic search
             │  (automatic discovery)
             ▼
  ┌───────────────────────────────────────────────────────────────────┐
  │                    6 OPTIMIZER AGENTS                              │
  │              (each runs independently)                            │
  │                                                                   │
  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐            │
  │  │ HEADLINE │ │ ICP      │ │ LAYOUT   │ │ CTA      │            │
  │  │ OPTIMIZER│ │ OPTIMIZER│ │ OPTIMIZER│ │ OPTIMIZER│            │
  │  └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘            │
  │       │            │            │            │                   │
  │  ┌──────────┐ ┌──────────┐                                       │
  │  │ SOCIAL   │ │ MOBILE   │                                       │
  │  │ PROOF    │ │ EXPERIENCE│  ← Also searches for layout recs    │
  │  │ OPTIMIZER│ │ AUDITOR  │                                       │
  │  └────┬─────┘ └────┬─────┘                                       │
  │       │            │                                             │
  │  Each searches KB for scorecard. Fallback: lightweight crawl.    │
  │  Each saves structured recommendations to KB.                    │
  └───────┼────────────┼─────────────────────────────────────────────┘
          │            │
          │  KB semantic searches (all 7 upstream sources)
          ▼            ▼
  ┌──────────────────────────────────────────────────────┐
  │  A/B VARIANT BUILDER                                  │
  │                                                       │
  │  Searches KB for ALL 7 upstream outputs:              │
  │  scorecard, headline, ICP, layout, CTA,               │
  │  social proof, mobile                                 │
  │                                                       │
  │  Graceful degradation:                                │
  │  • All found → full synthesis                         │
  │  • Partial → synthesis + lightweight fills            │
  │  • None found → advisory to run Scorecard Analyzer    │
  │                                                       │
  │  Saves: Variant A + Variant B + comparison to KB      │
  └──────────────────────────────────────────────────────┘

  ┌──────────────────────────────────────────────────────┐
  │  COPY FULL-PAGE WRITER (standalone, separate path)    │
  │                                                       │
  │  No upstream dependency — for NEW pages (no URL).     │
  │  Takes business info, ICP, offer, traffic type.       │
  │  Writes complete LP copy, self-scores against         │
  │  the traffic-appropriate scorecard.                   │
  └──────────────────────────────────────────────────────┘
```

### KB Title Patterns & YAML Headers

| Agent | KB Title Pattern | YAML `type` |
|-------|-----------------|-------------|
| Scorecard Analyzer | `LP Scorecard Analysis: {biz} — {cold/warm} — {date}` | `lp-scorecard-analysis` |
| Headline Optimizer | `LP Headline Recommendations: {biz} — {cold/warm} — {date}` | `lp-headline-recommendations` |
| ICP Optimizer | `LP ICP Recommendations: {biz} — {cold/warm} — {date}` | `lp-icp-recommendations` |
| Layout Optimizer | `LP Layout Recommendations: {biz} — {cold/warm} — {date}` | `lp-layout-recommendations` |
| CTA Optimizer | `LP CTA Recommendations: {biz} — {cold/warm} Lead — {date}` | `lp-cta-recommendations` |
| Social Proof Optimizer | `LP Social Proof Recommendations: {biz} — {cold/warm} Lead — {date}` | `lp-social-proof-recommendations` |
| Mobile Experience Auditor | `LP Mobile Audit: {biz} — {cold/warm} — {date}` | `lp-mobile-recommendations` |
| Copy Full-Page Writer | `LP Copy Draft: {biz} — {cold/warm} — {date}` | `lp-copy-draft` |
| A/B Variant Builder | `LP Optimization Variant {A/B}: {biz} — {cold/warm} — {date}` | `landing-page-ab-variant` |

All YAML headers include: `type`, `lead_type`, `research_date`, `page_url`. Freshness threshold: 30 days.

---

## Scorecard Point Allocation Comparison

```
                        COLD LEAD          WARM LEAD
                     ┌────────────┐     ┌────────────┐
  Hero Section       │████████ 30 │     │█████  20   │
                     ├────────────┤     ├────────────┤
  Below-the-Fold     │████   15   │     │█████  20   │
                     ├────────────┤     ├────────────┤
  Social Proof       │█████  20   │     │███   10    │
                     ├────────────┤     ├────────────┤
  Offer Clarity      │███   10    │     │█████  20   │
                     ├────────────┤     ├────────────┤
  Mobile Experience  │███   10    │     │███   10    │
                     ├────────────┤     ├────────────┤
  Brand & Design     │███   10    │     │███   10    │
                     ├────────────┤     ├────────────┤
  Technical & Trust  │██    5     │     │███   10    │
                     └────────────┘     └────────────┘
                     Total: 100         Total: 100

  Cold = Trust-heavy (hero 30 + proof 20 = 50% of score)
  Warm = Offer-heavy (offer 20 + below-fold 20 = 40% of score)
```

---

## Optimizer Subagent Skill Matrix

```
                          Header/    ICP         Layout
                          Subhead    Positioning  Optimization
                          ────────   ──────────   ────────────
  Headline formulas         ●
  Subheadline patterns      ●
  Cold vs warm copy         ●           ●            ●
  Before/after examples     ●
  Testing hierarchy         ●
  ICP alignment audit                   ●
  Language match                        ●
  Self-selection                        ●
  Proof alignment                       ●
  Objection mapping                     ●
  Page flow frameworks                               ●
  Visual hierarchy                                   ●
  Section ordering                                   ●
  CTA rhythm                                         ●
  Whitespace specs                                   ●
  Mobile stacking                                    ●
  Distraction audit                                  ●
```

---

## Data Flow: What Feeds Into the A/B Variant Builder

```
                    ┌─────────────────────────────────────┐
                    │          A/B VARIANT BUILDER          │
                    │                                       │
  From KB:          │                                       │
  Scorecard    ──▶  │  scorecard_results                   │
  Analyzer          │  overall_score                        │
  (semantic search) │  business_context                     │
                    │  page_url / traffic_source / goal     │
                    │                                       │
  From user    ──▶  │  score_corrections                   │
  (question_sets)   │  priority_sections                   │
                    │  optimization_constraints             │
                    │                                       │
  From KB:          │                                       │
  Headline     ──▶  │  header_recommendations              │
  Optimizer         │  (3-5 ranked headline/subhead combos) │
  (semantic search) │                                       │
                    │                                       │
  From KB:          │                                       │
  ICP          ──▶  │  icp_recommendations                 │
  Optimizer         │  (element-by-element rewrites)        │
  (semantic search) │                                       │
                    │                                       │
  From KB:          │                                       │
  Layout       ──▶  │  layout_recommendations              │
  Optimizer         │  (section reorder + wireframes)       │
  (semantic search) │                                       │
                    │                                       │
  Own research ──▶  │  competitive_scan                    │
                    │  (2-3 competitor page analysis)       │
                    │                                       │
                    │  Graceful degradation:                │
                    │  Uses whatever KB data is available.  │
                    │  Missing outputs → lightweight fills. │
                    │  Nothing found → advisory message.    │
                    │                                       │
                    │          ┌──────────┐ ┌──────────┐   │
                    │          │VARIANT A │ │VARIANT B │   │
                    │          │Increment │ │Structural│   │
                    │          └──────────┘ └──────────┘   │
                    │              │             │          │
                    │              ▼             ▼          │
                    │         Saved to KB + Artifact        │
                    └─────────────────────────────────────┘
```
