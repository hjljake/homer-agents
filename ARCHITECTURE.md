# Homer Agents — Architecture

## Agent Inventory

```
homer-agents/
├── blog-post-writer-agent/            Single agent — research + write 3 blog variants
├── cta-specialist/                    3-agent workflow — audit CTAs, research, build plan
├── upsell-advisor/                    3-agent workflow — gather context, research, deepen strategy
├── website-setup-advisor/             Single agent — platform recommendation + setup guide
│
│   LANDING PAGE SUITE (10 unified agents — each handles both cold + warm traffic)
├── lp-scorecard-analyzer/             Standalone — score LP against traffic-appropriate scorecard (100 pts)
├── lp-headline-optimizer/             Standalone — generate optimized headline/subheadline combos
├── lp-icp-optimizer/                  Standalone — audit every element against the ICP
├── lp-layout-optimizer/               Standalone — analyze structure, hierarchy, CTA rhythm
├── lp-cta-optimizer/                  Standalone — audit all CTAs, generate variants + rhythm map
├── lp-social-proof-optimizer/         Standalone — catalog proof, score, generate sourcing plan
├── lp-mobile-experience-auditor/      Standalone — deep 12-dimension mobile audit
├── lp-funnel-auditor/                 Standalone — full-funnel audit: awareness → click → LP → conversion → post-conversion
├── lp-copy-full-page-writer/          Standalone — write complete LP copy from scratch (no existing page needed)
├── lp-ab-variant-builder/             Standalone — synthesize all optimizer outputs into 2 A/B variants
```

---

## KB Data Architecture

The 10 LP agents share insights via the Knowledge Base. Each agent saves structured output with predictable titles and YAML headers. Downstream agents discover upstream data via `references.searches` (semantic search with similarity thresholds). All agents handle both cold and warm traffic via a `traffic_type` question.

**Freshness protocol:** All agents check `research_date` in YAML headers. < 30 days = fresh (use as-is). > 30 days = stale (warn user, proceed with available data). Missing = no prior analysis.

**Graceful degradation:** Every agent can run standalone. If upstream data exists in KB, it's incorporated automatically. If not, the agent falls back to a lightweight web crawl + business facts retrieval.

---

### KB Save Patterns (What Each Agent Writes)

| Agent | KB Title Pattern | YAML `type` | Key YAML Fields | Body Content |
|-------|-----------------|-------------|-----------------|--------------|
| Scorecard Analyzer | `LP Scorecard Analysis: {biz} — {cold/warm} — {date}` | `lp-scorecard-analysis` | `score`, `grade`, `traffic_source`, `page_goal`, `visitor_relationship` | Full 7-section scored critique, top strengths/issues, priority fixes |
| Headline Optimizer | `LP Headline Recommendations: {biz} — {cold/warm} — {date}` | `lp-headline-recommendations` | `source_scorecard_date` | 3-5 ranked headline/subheadline combos with projected scores |
| ICP Optimizer | `LP ICP Recommendations: {biz} — {cold/warm} — {date}` | `lp-icp-recommendations` | `icp_score` (X/10), `source_scorecard_date` | 5-dimension element-by-element audit, rewrites, personalization map |
| Layout Optimizer | `LP Layout Recommendations: {biz} — {cold/warm} — {date}` | `lp-layout-recommendations` | `layout_score` (X/16), `source_scorecard_date` | Section map, 8-dimension rubric, CTA rhythm, mobile assessment |
| CTA Optimizer | `LP CTA Recommendations: {biz} — {cold/warm} Lead — {date}` | `lp-cta-recommendations` | `source_scorecard_date` | CTA inventory, 3-5 variants, rhythm map, microcopy, competitor benchmark |
| Social Proof Optimizer | `LP Social Proof Recommendations: {biz} — {cold/warm} Lead — {date}` | `lp-social-proof-recommendations` | `current_proof_score`, `projected_proof_score` | Proof inventory, distribution map, sourcing plan, competitor analysis |
| Mobile Auditor | `LP Mobile Audit: {biz} — {cold/warm} — {date}` | `lp-mobile-recommendations` | `mobile_score` (X/24), `main_scorecard_s5_score` (X/10), `primary_mobile_entry`, `platform` | 12-dimension audit, 3-viewport analysis, speed metrics, in-app browser compatibility |
| Funnel Auditor | `Funnel Audit: {biz} — {funnel_type} — {date}` | `funnel-continuity-audit` | `funnel_score` (X/20), `leakiest_handoff`, `primary_channel`, `conversion_goal` | 5-stage funnel map, promise chain, 10-dimension rubric, stage-by-stage fixes |
| Copy Full-Page Writer | `LP Copy Draft: {biz} — {cold/warm} — {date}` | `lp-copy-draft` | `page_type`, `framework` (PAS/AIDA/BAB), `self_score` | Complete hero-to-footer copy, design notes per section, self-score |
| A/B Variant Builder | `LP Optimization Variant {A/B}: {biz} — {cold/warm} — {date}` | `landing-page-ab-variant` | `variant` (A/B), `current_score`, `estimated_new_score`, `target_sections` | Section-by-section changes, implementation checklist, A/B test setup |

All YAML headers also include: `type`, `lead_type` (or `traffic_type`), `research_date`, `page_url` (or `landing_page_url`).

---

### KB Read Patterns (What Each Agent Searches For)

#### Shared Context Searches (business data, not agent outputs)

Every agent needs organizational context. These searches ground the analysis in the specific business:

| Search ID | Query | Similarity | Used By |
|-----------|-------|-----------|---------|
| `business-profile` | "business profile products services industry" | 0.6 | All 10 agents |
| `customer-profiles` | "customer profile ideal customer persona buying behavior" | 0.6 | All 10 agents |
| `strategist-report` | "business strategy report analysis" | 0.6 | 9 of 10 (not CTA Optimizer) |
| `brand-guidelines` | "brand guidelines visual identity voice tone" | 0.6 | 9 of 10 (not Mobile Auditor) |

#### Agent-to-Agent KB Reads (the data flow)

This matrix shows which agent outputs each agent searches for:

```
                            SEARCHES FOR (reads from KB)
                   ┌──────┬──────┬─────┬──────┬─────┬──────┬──────┬──────┬─────┬─────┐
                   │Score │Head  │ICP  │Layout│CTA  │Proof │Mobile│Funnel│Copy │A/B  │
                   │card  │line  │     │      │     │      │      │      │Draft│Var. │
  ┌────────────────┼──────┼──────┼─────┼──────┼─────┼──────┼──────┼──────┼─────┼─────┤
  │Scorecard Anlzr │ self │      │     │      │     │      │      │      │     │     │
  │Headline Opt    │  ●   │      │     │      │     │      │      │      │     │     │
  │ICP Optimizer   │  ●   │      │     │      │     │      │      │      │     │     │
  │Layout Opt      │  ●   │      │     │      │     │      │      │      │     │     │
  │CTA Optimizer   │  ●   │      │     │      │     │      │      │      │     │     │
  │Social Proof Opt│  ●   │      │     │      │     │      │      │      │     │     │
W │Mobile Auditor  │  ●   │      │     │  ●   │     │      │      │      │     │     │
R │Funnel Auditor  │  ●   │  ●   │  ●  │  ●   │  ●  │  ●   │  ●   │      │  ●  │  ●  │
I │Copy Writer     │  ●   │  ●   │  ●  │  ●   │  ●  │  ●   │      │  ●   │     │     │
T │A/B Var Builder │  ●   │  ●   │  ●  │  ●   │  ●  │  ●   │  ●   │  ●   │  ●  │     │
E └────────────────┴──────┴──────┴─────┴──────┴─────┴──────┴──────┴──────┴─────┴─────┘
S                    ALL    3      3     4      3     3      2      2      2     1
                   read
                   this
```

**Read counts (how many agents consume each output):**
- Scorecard: **9** (every other agent) — the universal foundation
- Headline: **3** (A/B Builder, Funnel Auditor, Copy Writer)
- ICP: **3** (A/B Builder, Funnel Auditor, Copy Writer)
- Layout: **4** (A/B Builder, Funnel Auditor, Copy Writer, Mobile Auditor)
- CTA: **3** (A/B Builder, Funnel Auditor, Copy Writer)
- Social Proof: **3** (A/B Builder, Funnel Auditor, Copy Writer)
- Mobile: **2** (A/B Builder, Funnel Auditor)
- Funnel Audit: **2** (A/B Builder, Copy Writer)
- Copy Draft: **2** (A/B Builder, Funnel Auditor)
- A/B Variants: **1** (Funnel Auditor)

---

### Complete KB Data Flow Diagram

```
═══════════════════════════════════════════════════════════════════════════
                     KNOWLEDGE BASE — CENTRAL DATA STORE
    All agents read/write via semantic search with YAML-typed documents.
    Each arrow (──▶) represents a references.searches entry.
═══════════════════════════════════════════════════════════════════════════


  ┌─────────────────────────────────────────────────────────────────────┐
  │                     SHARED BUSINESS CONTEXT                         │
  │  (read by all agents — not produced by LP suite)                    │
  │                                                                     │
  │  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌───────────┐ │
  │  │  Business     │ │  Customer    │ │  Strategist  │ │   Brand   │ │
  │  │  Profile      │ │  Profiles    │ │  Report      │ │   Guide   │ │
  │  │  (industry,   │ │  (ICP, pain  │ │  (strategy,  │ │   (voice, │ │
  │  │   products,   │ │   points,    │ │   position,  │ │    tone,  │ │
  │  │   services)   │ │   behavior)  │ │   landscape) │ │    visual)│ │
  │  └──────┬────────┘ └──────┬───────┘ └──────┬───────┘ └─────┬─────┘ │
  │         │                 │                │               │       │
  │         └────────────┬────┴────────┬───────┴───────┬───────┘       │
  │                      │             │               │               │
  │                      ▼             ▼               ▼               │
  │              ALL 10 AGENTS READ THESE ON EVERY RUN                 │
  └─────────────────────────────────────────────────────────────────────┘


  ═══════════════════════════════════════════════════════════════════════
  TIER 1: FOUNDATION — No agent dependencies, produces data for all
  ═══════════════════════════════════════════════════════════════════════

  ┌─────────────────────────────────────────────────────────────────────┐
  │  SCORECARD ANALYZER                                                 │
  │  "Landing Page Health Check"                                        │
  │                                                                     │
  │  Reads:  business context only (no agent deps)                      │
  │  Crawls: landing page URL via search_web                            │
  │  Scores: 7-section, 100-point scorecard (cold or warm)              │
  │                                                                     │
  │  Saves:  lp-scorecard-analysis                                      │
  │          ├─ scorecard_results (section-by-section scores)           │
  │          ├─ business_context (synthesized from KB + crawl)          │
  │          ├─ overall_score + grade                                   │
  │          ├─ top_strengths (3)                                       │
  │          ├─ top_issues (3) + priority_fixes                         │
  │          └─ message_match_assessment (warm only)                    │
  │                                                                     │
  │  Consumed by: ALL other 9 agents                                    │
  └────────────────────────────────┬────────────────────────────────────┘
                                   │
          ┌────────────────────────┼────────────────────────┐
          │                        │                        │
          ▼                        ▼                        ▼

  ═══════════════════════════════════════════════════════════════════════
  TIER 2: OPTIMIZERS — Read scorecard, produce specialized recommendations
  ═══════════════════════════════════════════════════════════════════════

  ┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
  │ HEADLINE         │ │ ICP              │ │ LAYOUT           │
  │ OPTIMIZER        │ │ OPTIMIZER        │ │ OPTIMIZER        │
  │                  │ │                  │ │                  │
  │ Reads:           │ │ Reads:           │ │ Reads:           │
  │  scorecard ──▶   │ │  scorecard ──▶   │ │  scorecard ──▶   │
  │                  │ │                  │ │                  │
  │ Saves:           │ │ Saves:           │ │ Saves:           │
  │  lp-headline-    │ │  lp-icp-         │ │  lp-layout-      │
  │  recommendations │ │  recommendations │ │  recommendations │
  │  (3-5 combos     │ │  (5-dim audit,   │ │  (8-dim rubric,  │
  │   ranked by lift)│ │   element-by-    │ │   section reorder│
  │                  │ │   element)       │ │   CTA rhythm)    │
  └────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘
           │                    │                     │
           │                    │                     │
  ┌────────┴─────────┐ ┌───────┴──────────┐ ┌───────┴──────────┐
  │ CTA              │ │ SOCIAL PROOF     │ │ MOBILE           │
  │ OPTIMIZER        │ │ OPTIMIZER        │ │ AUDITOR          │
  │                  │ │                  │ │                  │
  │ Reads:           │ │ Reads:           │ │ Reads:           │
  │  scorecard ──▶   │ │  scorecard ──▶   │ │  scorecard ──▶   │
  │                  │ │                  │ │  layout recs ──▶ │
  │ Saves:           │ │ Saves:           │ │                  │
  │  lp-cta-         │ │  lp-social-proof-│ │ Saves:           │
  │  recommendations │ │  recommendations │ │  lp-mobile-      │
  │  (CTA inventory, │ │  (proof catalog, │ │  recommendations │
  │   3-5 variants,  │ │   distribution   │ │  (12-dim rubric, │
  │   rhythm map)    │ │   map, sourcing  │ │   3 viewports,   │
  │                  │ │   plan)          │ │   speed, in-app) │
  └────────┬─────────┘ └────────┬─────────┘ └────────┬─────────┘
           │                    │                     │
           └────────────────────┼─────────────────────┘
                                │
                                ▼

  ═══════════════════════════════════════════════════════════════════════
  TIER 3: SYNTHESIZERS — Read all upstream outputs, produce final deliverables
  ═══════════════════════════════════════════════════════════════════════

  ┌─────────────────────────────────────────────────────────────────────┐
  │  A/B VARIANT BUILDER                                                │
  │  "Split Test Blueprint"                                             │
  │                                                                     │
  │  Reads from KB (10 sources):                                        │
  │    scorecard ──────────▶ ┐                                          │
  │    headline recs ──────▶ │                                          │
  │    ICP recs ───────────▶ │                                          │
  │    layout recs ────────▶ ├──▶ Synthesize into 2 implementable      │
  │    CTA recs ───────────▶ │    A/B test variants                     │
  │    social proof recs ──▶ │                                          │
  │    mobile recs ────────▶ │    Variant A: Incremental (10-30% lift) │
  │    funnel audit ───────▶ │    Variant B: Structural (20-60% lift)  │
  │    copy draft ─────────▶ │                                          │
  │    brand guidelines ───▶ ┘                                          │
  │                                                                     │
  │  Graceful degradation:                                              │
  │    All found → full synthesis                                       │
  │    Partial → synthesis + lightweight fills for gaps                  │
  │    None → advisory to run Scorecard Analyzer first                  │
  │                                                                     │
  │  Saves: landing-page-ab-variant (×2) + document artifact            │
  └─────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────┐
  │  FUNNEL AUDITOR                                                     │
  │  "Full-Funnel Conversion Auditor"                                   │
  │                                                                     │
  │  Reads from KB (12 sources):                                        │
  │    scorecard ──────────▶ ┐                                          │
  │    headline recs ──────▶ │                                          │
  │    ICP recs ───────────▶ │                                          │
  │    layout recs ────────▶ │  Incorporates into Stage 3 (LP) of      │
  │    CTA recs ───────────▶ ├──▶ the 5-stage funnel audit              │
  │    social proof recs ──▶ │                                          │
  │    mobile recs ────────▶ │  Also audits Stages 1,2,4,5 from        │
  │    copy draft ─────────▶ │  user-provided ad copy, conversion       │
  │    A/B variants ───────▶ │  steps, and post-conversion details      │
  │    brand guidelines ───▶ ┘                                          │
  │                                                                     │
  │  Scores: 10-dimension funnel continuity rubric (X/20)               │
  │  Identifies: leakiest handoff + stage-by-stage fixes                │
  │                                                                     │
  │  Saves: funnel-continuity-audit + document artifact                 │
  └─────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────┐
  │  COPY FULL-PAGE WRITER                                              │
  │  "Landing Page Copywriter"                                          │
  │                                                                     │
  │  Reads from KB (9 sources):                                         │
  │    scorecard ──────────▶ ┐                                          │
  │    headline recs ──────▶ │  If prior optimizer work exists for      │
  │    ICP recs ───────────▶ │  a competitor or similar page,           │
  │    layout recs ────────▶ ├──▶ incorporates those insights into      │
  │    CTA recs ───────────▶ │  the new page draft                      │
  │    social proof recs ──▶ │                                          │
  │    funnel audit ───────▶ │  Also works fully standalone with        │
  │    prior LP analyses ──▶ │  just user inputs (no URL needed)        │
  │    brand guidelines ───▶ ┘                                          │
  │                                                                     │
  │  Writes: Complete LP copy (hero → footer), self-scores              │
  │  Saves: lp-copy-draft + document artifact                           │
  └─────────────────────────────────────────────────────────────────────┘


  ═══════════════════════════════════════════════════════════════════════
  FULL SUITE DEPENDENCY GRAPH (all KB reads summarized)
  ═══════════════════════════════════════════════════════════════════════

  TIER 1                TIER 2                        TIER 3
  (foundation)          (optimizers)                  (synthesizers)

  ┌──────────┐
  │SCORECARD │═══════▶ Headline Opt ─────────────▶ ┌──────────────┐
  │ANALYZER  │═══════▶ ICP Optimizer ────────────▶ │              │
  │          │═══════▶ Layout Optimizer ──────────▶ │  A/B VARIANT │
  │          │═══════▶ CTA Optimizer ────────────▶ │  BUILDER     │
  │          │═══════▶ Social Proof Opt ─────────▶ │              │
  │          │═══════▶ Mobile Auditor ───────────▶ │  (reads 10   │
  │          │════╗                                │   KB sources) │
  │          │    ║    Layout Opt ────────────────▶ │              │
  │          │    ║         │                       └──────┬───────┘
  │          │    ║         └──────▶ Mobile Auditor        │
  │          │    ║                                        │
  │          │    ╠══════════════════════════════════════▶ ┌──────────────┐
  │          │    ║    All 7 optimizer outputs ──────────▶ │              │
  │          │    ║    A/B Variants ─────────────────────▶ │  FUNNEL      │
  │          │    ║    Copy Draft ───────────────────────▶ │  AUDITOR     │
  │          │    ║    Brand Guidelines ─────────────────▶ │              │
  │          │    ║                                        │  (reads 12   │
  │          │    ║                                        │   KB sources) │
  │          │    ║                                        └──────────────┘
  │          │    ║
  │          │    ╠══════════════════════════════════════▶ ┌──────────────┐
  │          │    ║    All 6 optimizer outputs ──────────▶ │              │
  │          │    ║    Funnel Audit ─────────────────────▶ │  COPY WRITER │
  │          │    ║    Brand Guidelines ─────────────────▶ │              │
  │          │    ║    Prior LP analyses ────────────────▶ │  (reads 9    │
  │          │    ║                                        │   KB sources) │
  └──────────┘    ║                                        └──────────────┘
                  ║
                  ╚═══▶ (also read by A/B Builder,
                         Funnel Auditor, Copy Writer)
```

---

### Recommended Usage Sequences

**Optimize an existing page (full suite):**
```
1. Scorecard Analyzer        → foundation scores + business context
2. Run in any order:         → each reads scorecard from KB
   • Headline Optimizer
   • ICP Optimizer
   • Layout Optimizer
   • CTA Optimizer
   • Social Proof Optimizer
   • Mobile Auditor
3. A/B Variant Builder       → synthesizes all into implementable variants
```

**Audit the full funnel:**
```
1. Scorecard Analyzer        → (optional, enriches Stage 3)
2. Any optimizers             → (optional, enriches Stage 3)
3. Funnel Auditor            → maps all 5 stages, reads whatever exists
```

**Write a new page from scratch:**
```
1. Copy Full-Page Writer     → works standalone, or reads prior analyses
2. Scorecard Analyzer        → score the draft (treat the page as live)
3. Optimizers as needed      → refine specific elements
4. A/B Variant Builder       → generate test variants from the draft
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

## Skill Matrix

```
                    Header/ ICP      Layout   CTA      Social   Mobile   Funnel
                    Subhead Position Opt      Opt      Proof    Exp      Continuity
                    ─────── ──────── ──────── ──────── ──────── ──────── ──────────
Headline formulas     ●
Subheadline ptns      ●
Cold vs warm copy     ●       ●        ●
Before/after ex       ●
Testing hierarchy     ●
ICP alignment                 ●
Language match                ●
Self-selection                ●
Proof alignment               ●
Objection mapping             ●
Page flow fworks                       ●
Visual hierarchy                       ●
Section ordering                       ●
CTA rhythm                             ●                                 
Whitespace specs                       ●
Mobile stacking                        ●                ●
Distraction audit                      ●
CTA copy formulas                               ●
Commitment ladder                               ●
CTA audit checklist                             ●
Proof scoring rubric                                     ●
Proof distribution                                       ●
Proof sourcing                                           ●
Viewport rendering                                                ●
Thumb zone map                                                    ●
Tap target specs                                                  ●
Page speed / CWV                                                  ●
In-app browser compat                                             ●
Mobile form UX                                                    ●
Message continuity                                                         ●
Emotional arc                                                              ●
Promise escalation                                                         ●
Trust accumulation                                                         ●
Handoff quality                                                            ●
Funnel leak diagnosis                                                      ●
```

**Agents using each skill:**
- `cold-lead-landing-page-scorecard` — All 10 agents
- `warm-lead-landing-page-scorecard` — All 10 agents
- `lp-header-subheader-optimization` — Headline Optimizer, Copy Writer
- `lp-icp-positioning` — ICP Optimizer, Copy Writer
- `lp-layout-optimization` — Layout Optimizer, Copy Writer
- `cta-optimization` — CTA Optimizer, Copy Writer
- `lp-social-proof-engineering` — Social Proof Optimizer
- `lp-mobile-experience` — Mobile Auditor
- `funnel-continuity-audit` — Funnel Auditor
