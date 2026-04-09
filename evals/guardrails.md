# Agent Guardrails — Failure Mode Definitions

Defines what "gone wrong" looks like for each agent so the platform can detect it programmatically.

---

## Universal Failure Modes (All Agents)

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Runaway token usage** | `token_count` exceeds `resource_bounds.expected_token_range[1]` from agent-manifest.json | Medium |
| **Excessive tool calls** | `tool_call_count` exceeds `resource_bounds.expected_tool_calls[1]` | Medium |
| **Timeout exceeded** | `duration_ms` exceeds `metadata.config.timeout` | Medium |
| **Empty output** | Output content is null, empty, or below `output_rules.min_length` | Critical |
| **Missing KB save** | Agent completes but `artifacts_created` does not include expected KB document type | Medium |
| **Generic advice** | Output contains vague phrases without specific copy (e.g., "improve your headline" without the actual new headline) | Medium |

**Detection**: The platform's `PersonaExecution` model already tracks `duration_ms`, `actions_taken`, and `artifacts_created`. Wire guardrail checks into the execution completion flow.

---

## LP Scorecard Analyzer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Wrong scorecard applied** | Cold output contains "message match assessment" or warm scoring weights; Warm output is missing "message match assessment" | Critical |
| **Hallucinated page content** | Agent describes page elements that don't exist on the URL (requires page re-crawl to verify) | High |
| **Incomplete scoring** | Fewer than 7 scored sections in output | High |
| **Score math error** | Section scores don't sum to the stated overall_score | Medium |
| **Missing priority fixes** | Fewer than 3 priority fixes with specific copy suggestions | Medium |

---

## LP Headline Optimizer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Insufficient variants** | Fewer than 3 headline/subheadline combos in output | High |
| **Missing projected scores** | Variants don't include current and projected score comparisons | Medium |
| **Wrong scorecard consumed** | Consumed a scorecard for a different page_url (detected by KB verification prompt) | High |

---

## LP ICP Optimizer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Incomplete dimension audit** | Fewer than 5 ICP dimensions scored (Language Match, Specificity, Self-Selection, Proof Alignment, Objection Mapping) | High |
| **Missing ICP score** | No overall ICP positioning score (X/10) in output | Medium |
| **Generic rewrites** | Rewrites describe what to do instead of providing exact replacement copy | Medium |

---

## LP Layout Optimizer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Incomplete rubric** | Fewer than 8 layout dimensions scored | High |
| **Missing section map** | No current section map of the page | Medium |
| **No section order recommendation** | No proposed optimal section order for the traffic type | Medium |

---

## LP CTA Optimizer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Missing CTA inventory** | No audit of existing CTAs on the page | High |
| **Insufficient variants** | Fewer than 3 CTA variants | High |
| **Missing rhythm map** | No CTA rhythm map showing placement across page | Medium |
| **Wrong commitment calibration** | Cold traffic page gets "Buy Now" recommendations without flagging risk | Medium |

---

## LP Social Proof Optimizer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Missing proof inventory** | No catalog of existing proof elements | High |
| **Missing distribution map** | No current/recommended proof distribution map | Medium |
| **Missing sourcing plan** | No plan for obtaining proof the business doesn't have | Medium |

---

## LP Mobile Experience Auditor

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Incomplete dimension audit** | Fewer than 12 mobile dimensions scored | High |
| **Missing viewport analysis** | Fewer than 3 viewports analyzed (small phone, mid phone, large phone) | High |
| **Missing in-app browser assessment** | No analysis of in-app browser rendering for the stated mobile entry point | Medium |
| **Vague CSS recommendations** | Fix suggestions lack specific pixel sizes, CSS properties, or hex codes | Medium |

---

## LP Funnel Auditor

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Missing stages** | Fewer than 5 funnel stages audited (Awareness, Click, Landing Page, Conversion, Post-Conversion) | Critical |
| **Incomplete rubric** | Fewer than 10 funnel continuity dimensions scored | High |
| **Missing leakiest handoff** | No identification of the single biggest conversion leak | High |
| **Ignored upstream data** | KB had LP suite analyses but Funnel Auditor didn't reference them | Medium |

---

## LP A/B Variant Builder

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Missing variant** | Output doesn't contain both Variant A and Variant B | Critical |
| **Identical variants** | Variant A and B have substantially the same changes (defeats the purpose) | High |
| **Missing implementation checklists** | Either variant lacks actionable implementation steps | Medium |
| **Wrong degradation mode** | Claims "full" mode when upstream data is actually missing | Medium |
| **Unattributed recommendations** | Recommendations don't cite which optimizer they came from (when available) | Low |

---

## LP Copy Full-Page Writer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Wrong framework** | Uses PAS for warm traffic or AIDA for cold without justification | Medium |
| **Missing sections** | Output doesn't cover hero through footer | High |
| **No self-score** | Missing self-assessment against the traffic-appropriate scorecard | Medium |
| **Ignored optimizer inputs** | KB had optimizer outputs but copy doesn't reflect them | Medium |

---

## CTA Specialist (Workflow)

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Workflow step failure** | A step fails and downstream steps receive empty input | High |
| **Generic industry research** | Industry researcher doesn't name specific competitors | Medium |
| **Implementation plan too vague** | Plan lacks specific code/copy/placement instructions | Medium |

---

## Upsell Advisor (Workflow)

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **No AOV context** | Context gatherer didn't establish current AOV or order patterns | Medium |
| **Generic strategies** | Strategies don't reference specific products or price points | Medium |
| **Workflow step failure** | Same as CTA Specialist | High |

---

## Blog Post Writer

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Style mismatch** | User has existing blog but output doesn't match established voice/style | Medium |
| **SEO missing** | No keyword integration or meta description | Medium |
| **Output too short** | Below 500 words (output_rules min_length) | High |

---

## Website Setup Advisor

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Wrong platform recommended** | Recommends platform that doesn't support stated requirements (e.g., no ecommerce on a platform without it) | High |
| **Technical jargon** | Uses developer terms for a non-technical audience | Medium |
| **Output too short** | Below 500 words | High |

---

## Inter-Agent Data Flow Failures

These are systemic failures in the LP Suite's KB-based data flow:

| Failure Mode | How to Detect | Severity |
|---|---|---|
| **Cross-page contamination** | Agent consumes a KB document for Page A when analyzing Page B | Critical |
| **Stale data used silently** | Agent uses data > 30 days old without warning the user | Medium |
| **Broken chain** | Scorecard saved but downstream agent can't find it via semantic search | High |
| **Duplicate KB documents** | Multiple scorecards for the same page/traffic_type/date | Low |

---

## Recommended Detection Implementation

1. **Post-execution hook**: After each agent completes, run the `quality_checks` prompts defined in the agent's `validation` block. These are LLM-graded structural checks.

2. **Programmatic checks**: Compare `PersonaExecution` metrics against `resource_bounds` from `agent-manifest.json`. Flag anomalies.

3. **KB integrity checks**: After any LP Suite agent saves to KB, verify the YAML header has the expected `type` and required fields. This is a simple string/regex check, not an LLM call.

4. **Chain verification**: For the chain tests in `lp-chain-tests.fixture.json`, run agents in sequence and verify each downstream agent's output references the upstream agent's output (check for `source_scorecard_date` or similar cross-references).
