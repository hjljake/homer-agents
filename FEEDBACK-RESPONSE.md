# Feedback Response — Homer's Agents

**To**: Simon, Eduardo
**From**: Homer
**Date**: 2026-04-09
**Re**: Response to agent review feedback (2026-04-08)

---

## Summary

All 8 feedback items have been addressed. Here's what was done and what still needs Eduardo/platform work.

| # | Item | Homer Status | Eduardo Action Needed |
|---|------|-------------|----------------------|
| 1 | Prerequisites | Done | Extend schema, wire UI |
| 2 | KB search robustness | Partial | Add page_url filter to KB search |
| 3 | question_sets pattern | Documented | Architecture decision |
| 4 | Copy Writer to LandingPage | Documented | Different integration path needed |
| 5 | Tool verification | Documented | Verify `search_web` registration |
| 6 | Deploy order | Agreed | N/A |
| 7 | Evals & testing | Done | Build test runner harness |
| 8 | Scope confirmation | Confirmed | N/A |

---

## 1. Prerequisites Field

**What Homer did**: Defined prerequisites for all 14 agents in `agent-manifest.json`, following Simon's exact table.

**Why a separate file**: The AgentDefinition schema (`agent-definition.schema.json`) may reject unknown fields inside `metadata` if `additionalProperties: false` is set. Storing in a manifest avoids AJV validation failures.

**Eduardo action**: Extend the schema to add `prerequisites` to the `metadata` object:
```json
"prerequisites": {
  "type": "object",
  "properties": {
    "recommended": { "type": "array", "items": { "type": "string" } },
    "enhancers": { "type": "array", "items": { "type": "string" } },
    "skip_message": { "type": "string" }
  }
}
```
Once the schema supports it, migrate values from `agent-manifest.json` into each agent's `metadata` block.

**UI wiring**: See Simon's spec in feedback Section 1 — banner before Tier 2 agents if scorecard missing, progress indicator before Tier 3 agents showing which optimizers have been run.

---

## 2. KB Semantic Search Robustness

**What Homer did**: Added a **KB Result Verification** instruction to every LP Suite agent's gather step. The instruction tells the agent to check `page_url` in the YAML header of any retrieved KB document against the current target URL, and discard mismatches.

This is a prompt-level guardrail — it works but depends on the LLM following the instruction.

**Eduardo action (recommended)**: Add a `page_url` metadata filter to the KB search at the platform level. The `SearchService` already supports `exclude_metadata` via JSONB operators. Extending to `include_metadata` with a `page_url` match would make this deterministic rather than prompt-dependent.

**Recommendation**: Option A (quick metadata filter) for v1, Option B (structured references) for v2.

---

## 3. question_sets Pattern Decision

**What Homer did**: No agent changes — the agents' `question_sets` format already maps cleanly to both FormTemplate and pause-step patterns.

**Decision needed from Eduardo**:
- **FormTemplate** for single agents (LP Suite, Blog Writer, Website Setup Advisor) — each agent gets a FormTemplate record, frontend renders the form, passes responses when triggering the agent
- **Pause step** for workflows (CTA Specialist, Upsell Advisor, Valuation Wizard) — already using this pattern with `ui_schema`

Homer's `question_sets` fields (`id`, `question`, `responseKey`, `format`, `required`, `options`, `placeholder`, `hint`) map to either system with minimal transformation.

---

## 4. Copy Writer Output to LandingPage

**Key finding**: `LandingPage` is **not a database model**. The platform uses `LandingPageBuilderAgent` which operates via git — it writes markdown/React files to the `amiara-marketing` repo using tools like `write_page_file`, `git_commit_and_push`, `git_create_pr`.

**Implication**: The integration path Simon proposed (post-hook creating a `LandingPage` record) doesn't apply. Instead:
- The LP Copy Writer's output (hero-to-footer copy in a document artifact) could feed into the `LandingPageBuilderAgent` as input
- This would be a new workflow: Copy Writer generates content -> user reviews -> LandingPageBuilderAgent converts it to a live page via git
- The A/B Variant Builder's two variants could each become a `LandingPageBuilderAgent` run on a separate branch

**Eduardo action**: Design the Copy Writer -> LandingPageBuilderAgent handoff. This is a workflow integration, not a JSON change.

---

## 5. Tool Name Verification

**Confirmed present in InternalToolRegistry**:
- `retrieve_reference_content`
- `manage_business_fact`
- `add_file_to_kb`
- `create_document_artifact`

**NOT found in InternalToolRegistry**:
- `search_web` — Used by all 14 agents. Not registered as an internal tool. Likely a provider/integration tool registered elsewhere.

**Eduardo action**: Verify where `search_web` is registered and confirm all agents can access it. If it's an integration tool, confirm it's available to all orgs.

---

## 6. Deploy Order

Agree with Simon's phasing:

| Phase | Agents | Rationale |
|---|---|---|
| Phase 1 | CTA Specialist, Upsell Advisor | Already CDW-shaped with pause steps. Least integration work. |
| Phase 2 | LP Scorecard Analyzer | Foundation of LP Suite. Good test of single-agent + question_sets pattern. |
| Phase 3 | LP Suite Tier 2 + Tier 3 | Roll out once Scorecard is stable and question_sets pattern is decided. |
| Phase 4 | Blog Post Writer, Website Setup Advisor | Draft status. Hold until active agents are deployed. |

**Not in this review** (future phases): Instagram Content Specialist (adds Meta API tools + OAuth), Valuation Wizard (active, uses standard tools).

---

## 7. Evals & Quality Testing

**What Homer provided**:

### A. Validation blocks (input_rules + output_rules + quality_checks)
Added to all 14 agents. These are built into the agent JSON using the schema's existing `validation` field.

- **9 LP Suite agents** got full validation: input_rules (url, traffic_type, traffic_source, goal), output_rules (min_length 1500-3000), and quality_checks (agent-specific structural checks)
- **LP Copy Writer** already had validation — unchanged
- **CTA Specialist** (3 sub-agents): output_rules added
- **Upsell Advisor** (3 sub-agents): output_rules added
- **Blog Writer, Website Setup Advisor**: already had validation — unchanged

### B. Resource bounds
Defined in `agent-manifest.json` for all 14 agents: `expected_token_range`, `expected_tool_calls`, `expected_duration_seconds`, `max_web_searches`.

### C. Test fixtures
Created in `evals/` directory — one fixture file per agent (2-3 test cases each) plus a chain test file:

| File | Test Cases | What It Tests |
|---|---|---|
| `lp-scorecard-analyzer.fixture.json` | 3 | Cold SaaS, warm email, cold ecommerce |
| `lp-headline-optimizer.fixture.json` | 2 | With scorecard, standalone |
| `lp-icp-optimizer.fixture.json` | 2 | Cold, warm |
| `lp-layout-optimizer.fixture.json` | 2 | With scorecard, standalone |
| `lp-cta-optimizer.fixture.json` | 2 | Cold, warm |
| `lp-social-proof-optimizer.fixture.json` | 2 | No existing proof, existing proof |
| `lp-mobile-experience-auditor.fixture.json` | 2 | With layout recs, standalone |
| `lp-funnel-auditor.fixture.json` | 2 | Full upstream, standalone |
| `lp-copy-full-page-writer.fixture.json` | 2 | All optimizers, standalone |
| `lp-ab-variant-builder.fixture.json` | 3 | 0/3/7 upstream (degradation) |
| `lp-chain-tests.fixture.json` | 4 | Inter-agent KB data flow |
| `cta-specialist.fixture.json` | 2 | Ecommerce, SaaS |
| `upsell-advisor.fixture.json` | 2 | Digital, physical products |
| `blog-post-writer.fixture.json` | 2 | Existing blog, no blog |
| `website-setup-advisor.fixture.json` | 2 | No website, needs blog |

### D. Guardrail definitions
Created `evals/guardrails.md` — per-agent failure mode tables with detection logic and severity levels. Covers universal failures (runaway tokens, empty output, missing KB save) and agent-specific failures (wrong scorecard applied, hallucinated content, missing dimensions, cross-page contamination).

### E. Inter-agent data flow tests
Included in `lp-chain-tests.fixture.json` — 4 tests covering Simon's exact spec.

**Eduardo action**: Build the test runner harness that:
1. Runs each agent against its fixtures
2. Checks output against `output_must_contain` / `output_must_not_contain`
3. Verifies KB saves against `kb_save_check`
4. Runs `quality_checks` prompts from the validation block
5. Compares execution metrics against `resource_bounds`

---

## 8. Scope Confirmation

Confirmed — no changes needed:
- Agents are content/analysis only — no direct website modification
- No new API integrations beyond existing KB, web search, business facts
- No new models or migrations — agents fit into existing AgentDefinition + Workflow models
- Skills are markdown prompt fragments, no code execution

**Note for future**: The Instagram agents (not in this review) add `initiate_integration_setup` and 5 Meta API tools (`meta_instagram_get_profile`, `meta_instagram_get_profile_insights`, `meta_instagram_list_media`, `meta_instagram_get_media_insights`, `meta_instagram_get_audience_demographics`). These expand the tool scope and require Meta OAuth integration.

---

## Files Changed / Created

### Modified (validation blocks + KB verification prompt):
- `lp-suite/lp-scorecard-analyzer/lp-scorecard-analyzer.json`
- `lp-suite/lp-headline-optimizer/lp-headline-optimizer.json`
- `lp-suite/lp-icp-optimizer/lp-icp-optimizer.json`
- `lp-suite/lp-layout-optimizer/lp-layout-optimizer.json`
- `lp-suite/lp-cta-optimizer/lp-cta-optimizer.json`
- `lp-suite/lp-social-proof-optimizer/lp-social-proof-optimizer.json`
- `lp-suite/lp-mobile-experience-auditor/lp-mobile-experience-auditor.json`
- `lp-suite/lp-copy-full-page-writer/lp-copy-full-page-writer.json` (KB verification only)
- `lp-suite/lp-funnel-auditor/lp-funnel-auditor.json`
- `lp-suite/lp-ab-variant-builder/lp-ab-variant-builder.json`
- `cta-specialist/cta-specialist-agents.json` (validation only)
- `upsell-advisor/upsell-advisor-agents.json` (validation only)

### Created:
- `agent-manifest.json` — prerequisites + resource bounds for all 14 agents
- `FEEDBACK-RESPONSE.md` — this document
- `evals/guardrails.md` — failure mode definitions
- `evals/*.fixture.json` — 15 test fixture files
