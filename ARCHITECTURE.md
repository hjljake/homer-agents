# Homer Agents — Architecture

## Agent Inventory

```
homer-agents/
├── blog-post-writer-agent/       Single agent — research + write 3 blog variants
├── cta-specialist/                3-agent workflow — audit CTAs, research, build plan
├── upsell-advisor/                3-agent workflow — gather context, research, deepen strategy
├── website-setup-advisor/         Single agent — platform recommendation + setup guide
├── cold-lead-lp-optimizer/        5-agent workflow — score, optimize, build A/B variants
└── warm-lead-lp-optimizer/        5-agent workflow — score, optimize, build A/B variants
```

---

## Cold Lead LP Optimizer — Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                    COLD LEAD LP OPTIMIZER                           │
│                                                                     │
│  User Input: URL(s), screenshots, traffic source, page goal         │
└─────────────────────┬───────────────────────────────────────────────┘
                      │
                      ▼
        ┌─────────────────────────┐
        │   1. LP ANALYZER        │
        │                         │
        │  • Crawls landing page  │
        │  • Pulls KB context     │
        │  • Applies Cold Lead    │
        │    Scorecard (100 pts)  │
        │  • Scores all 7 sections│
        │  • Saves analysis to KB │
        │                         │
        │  Skills:                │
        │  └ cold-lead-scorecard  │
        └────────────┬────────────┘
                     │
                     │  scorecard_results
                     │  overall_score
                     │  top_strengths
                     │  top_issues
                     ▼
        ┌─────────────────────────┐
        │   2. CONFIRM SCORECARD  │
        │        (pause)          │
        │                         │
        │  User reviews scores    │
        │  ┌───────────────────┐  │
        │  │ ✓ Accurate?       │  │
        │  │ ✎ Corrections     │  │
        │  │ ★ Priority areas  │  │
        │  │ ⚙ Constraints     │  │
        │  └───────────────────┘  │
        └────────────┬────────────┘
                     │
                     │  confirmed scorecard
                     │  user priorities
                     │  constraints
                     ▼
    ┌────────────────────────────────────────────────────┐
    │            3 OPTIMIZER SUBAGENTS                    │
    │         (run sequentially after confirm)            │
    │                                                    │
    │  ┌──────────────────┐                              │
    │  │  3a. HEADER       │                              │
    │  │  OPTIMIZER        │                              │
    │  │                   │                              │
    │  │  • Evaluates      │                              │
    │  │    headline &     │                              │
    │  │    subheadline    │                              │
    │  │  • Researches     │                              │
    │  │    competitor     │                              │
    │  │    headlines      │                              │
    │  │  • Generates 3-5  │                              │
    │  │    alternatives   │                              │
    │  │    with projected │                              │
    │  │    score lift     │                              │
    │  │                   │                              │
    │  │  Skills:          │                              │
    │  │  ├ header-subhead │                              │
    │  │  └ cold-scorecard │                              │
    │  │                   │                              │
    │  │  Output:          │                              │
    │  │  header_          │                              │
    │  │  recommendations  │                              │
    │  └────────┬──────────┘                              │
    │           │                                         │
    │           ▼                                         │
    │  ┌──────────────────┐                              │
    │  │  3b. ICP          │                              │
    │  │  POSITIONING      │                              │
    │  │  OPTIMIZER        │                              │
    │  │                   │                              │
    │  │  • Defines the    │                              │
    │  │    target ICP     │                              │
    │  │  • Audits every   │                              │
    │  │    element against│                              │
    │  │    5 dimensions:  │                              │
    │  │    - Language      │                              │
    │  │    - Specificity   │                              │
    │  │    - Self-select   │                              │
    │  │    - Proof align   │                              │
    │  │    - Objections    │                              │
    │  │  • Rewrites all   │                              │
    │  │    misaligned copy │                              │
    │  │                   │                              │
    │  │  Skills:          │                              │
    │  │  ├ icp-positioning│                              │
    │  │  └ cold-scorecard │                              │
    │  │                   │                              │
    │  │  Output:          │                              │
    │  │  icp_             │                              │
    │  │  recommendations  │                              │
    │  └────────┬──────────┘                              │
    │           │                                         │
    │           ▼                                         │
    │  ┌──────────────────┐                              │
    │  │  3c. LAYOUT       │                              │
    │  │  OPTIMIZER        │                              │
    │  │                   │                              │
    │  │  • Maps current   │                              │
    │  │    section order  │                              │
    │  │  • Squint test    │                              │
    │  │  • Above-fold     │                              │
    │  │    audit          │                              │
    │  │  • CTA rhythm     │                              │
    │  │  • Whitespace     │                              │
    │  │  • Distraction    │                              │
    │  │    audit          │                              │
    │  │  • Mobile stack   │                              │
    │  │  • Proposes new   │                              │
    │  │    section order  │                              │
    │  │                   │                              │
    │  │  Skills:          │                              │
    │  │  ├ layout-optim   │                              │
    │  │  └ cold-scorecard │                              │
    │  │                   │                              │
    │  │  Output:          │                              │
    │  │  layout_          │                              │
    │  │  recommendations  │                              │
    │  └────────┬──────────┘                              │
    │           │                                         │
    └───────────┼─────────────────────────────────────────┘
                │
                │  All 3 optimizer outputs
                ▼
        ┌─────────────────────────┐
        │  4. A/B VARIANT         │
        │  BUILDER                │
        │                         │
        │  Receives:              │
        │  • Confirmed scorecard  │
        │  • Header recs          │
        │  • ICP recs             │
        │  • Layout recs          │
        │  • Competitive scan     │
        │                         │
        │  Produces:              │
        │  ┌───────────────────┐  │
        │  │ VARIANT A:        │  │
        │  │ "Incremental"     │  │
        │  │                   │  │
        │  │ Best headline     │  │
        │  │ + top ICP fixes   │  │
        │  │ + minor layout    │  │
        │  │   tweaks          │  │
        │  │                   │  │
        │  │ Effort: 1-2 days  │  │
        │  │ Lift: 10-30%      │  │
        │  └───────────────────┘  │
        │  ┌───────────────────┐  │
        │  │ VARIANT B:        │  │
        │  │ "Structural       │  │
        │  │  Rethink"         │  │
        │  │                   │  │
        │  │ Ambitious headline│  │
        │  │ + full ICP repos  │  │
        │  │ + section reorder │  │
        │  │ + new sections    │  │
        │  │                   │  │
        │  │ Effort: 3-7 days  │  │
        │  │ Lift: 20-60%      │  │
        │  └───────────────────┘  │
        │                         │
        │  Saves to KB:           │
        │  • Variant A doc        │
        │  • Variant B doc        │
        │  • Side-by-side compare │
        └─────────────────────────┘
```

---

## Warm Lead LP Optimizer — Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                    WARM LEAD LP OPTIMIZER                            │
│                                                                     │
│  User Input: URL(s), screenshots, traffic source, referring         │
│              message, visitor relationship, page goal                │
└─────────────────────┬───────────────────────────────────────────────┘
                      │
                      ▼
        ┌─────────────────────────┐
        │   1. LP ANALYZER        │
        │                         │
        │  • Crawls landing page  │
        │  • Pulls KB context     │
        │  • Evaluates MESSAGE    │
        │    MATCH (critical)     │
        │  • Applies Warm Lead    │
        │    Scorecard (100 pts)  │
        │  • Scores all 7 sections│
        │  • Saves analysis to KB │
        │                         │
        │  Skills:                │
        │  └ warm-lead-scorecard  │
        └────────────┬────────────┘
                     │
                     │  scorecard + message_match_assessment
                     ▼
        ┌─────────────────────────┐
        │   2. CONFIRM SCORECARD  │
        │        (pause)          │
        │                         │
        │  Shows message match    │
        │  assessment first       │
        │  ┌───────────────────┐  │
        │  │ ✓ Accurate?       │  │
        │  │ ✎ Corrections     │  │
        │  │ ★ Priority areas  │  │
        │  │ ⚙ Constraints     │  │
        │  └───────────────────┘  │
        └────────────┬────────────┘
                     │
                     ▼
    ┌────────────────────────────────────────────────────┐
    │            3 OPTIMIZER SUBAGENTS                    │
    │                                                    │
    │  ┌──────────────────┐                              │
    │  │  3a. HEADER       │  Focus: message match,      │
    │  │  OPTIMIZER        │  relationship acknowledgment,│
    │  │  (warm-specific)  │  offer-first language        │
    │  └────────┬──────────┘                              │
    │           ▼                                         │
    │  ┌──────────────────┐                              │
    │  │  3b. ICP          │  Focus: segment-specific     │
    │  │  POSITIONING      │  messaging, personalization  │
    │  │  (warm-specific)  │  opportunities, relationship │
    │  │                   │  acknowledgment              │
    │  └────────┬──────────┘                              │
    │           ▼                                         │
    │  ┌──────────────────┐                              │
    │  │  3c. LAYOUT       │  Focus: offer-first layout,  │
    │  │  OPTIMIZER        │  friction reduction,         │
    │  │  (warm-specific)  │  comparison sections,        │
    │  │                   │  channel consistency          │
    │  └────────┬──────────┘                              │
    └───────────┼─────────────────────────────────────────┘
                │
                ▼
        ┌─────────────────────────┐
        │  4. A/B VARIANT         │
        │  BUILDER                │
        │                         │
        │  Variant A: Incremental │
        │  + message match fix    │
        │  + personalization adds │
        │  + friction reduction   │
        │                         │
        │  Variant B: Structural  │
        │  + full ICP reposition  │
        │  + warm-traffic layout  │
        │  + all personalization  │
        │  + comparison sections  │
        └─────────────────────────┘
```

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
  From Analyzer ──▶ │  scorecard_results                   │
                    │  overall_score                        │
                    │  business_context                     │
                    │  page_url / traffic_source / goal     │
                    │                                       │
  From Confirm ──▶  │  score_corrections                   │
     (pause)        │  priority_sections                   │
                    │  optimization_constraints             │
                    │                                       │
  From Header  ──▶  │  header_recommendations              │
  Optimizer         │  (3-5 ranked headline/subhead combos) │
                    │                                       │
  From ICP     ──▶  │  icp_recommendations                 │
  Optimizer         │  (element-by-element rewrites)        │
                    │                                       │
  From Layout  ──▶  │  layout_recommendations              │
  Optimizer         │  (section reorder + wireframes)       │
                    │                                       │
  Own research ──▶  │  competitive_scan                    │
                    │  (2-3 competitor page analysis)       │
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
