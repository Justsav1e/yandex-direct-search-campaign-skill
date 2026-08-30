---
name: yandex-direct-campaign-builder
description: >-
  Build, audit, rebuild, and optimize Yandex Direct SEARCH campaigns end-to-end: business and product discovery, campaign and landing architecture, Yandex Wordstat research, semantic clustering, keywords, local negative keywords, group/campaign negative phrases, operators, Search autotargeting, URL parameters, combinatorial search ads, manual/automatic Search bidding, moderation, Yandex Metrica, SEO/CRO readiness, launch gates, Search Terms optimization, and handoff state. Use whenever a user asks about a Yandex Direct Search campaign, search ad group, Wordstat, semantic core, negatives, search ad copy, landing mapping, or campaign handoff. This skill is Search-only: do not use it as methodology for RСЯ/Networks, product campaigns/feeds, smart banners, media/display, video, or other non-Search formats. Always verify volatile rules against current official Yandex documentation and preserve prior decisions in a state ledger.
compatibility: >-
  Model-agnostic Agent Skills format. Requires web access for current Yandex documentation and the ability to read user-provided CSV/Markdown files. File persistence is strongly recommended.
---

# Yandex Direct Campaign Builder

Build Yandex Direct campaigns as an evidence-driven system, not as a one-shot list of keywords.

## Scope: Search only

This skill is intentionally limited to **Yandex Direct Search campaigns**. It does not claim to provide a complete methodology for:

- РСЯ / Yandex Advertising Network campaigns;
- product campaigns, feeds, ecommerce/product ads, or smart banners;
- media/display or video advertising;
- other non-Search Direct formats that require their own research, creative, bidding, and optimization methodology.

If a task materially depends on one of those formats, stop and state that it is outside this skill's scope rather than silently extrapolating Search rules.

## Companion reasoning skills

This workflow is designed to compose with two external reasoning skills. They are **recommended companions, not hard dependencies**: an agent may use them when installed, or follow the equivalent phases defined in this file when they are unavailable.

1. **Brainstorm Diverge-Converge** — use for semantic exploration, gap-finding, ad-angle brainstorming, clustering, and disciplined convergence.
   - Skill: [`brainstorm-diverge-converge`](https://github.com/lyndonkl/claude/blob/main/skills/brainstorm-diverge-converge/SKILL.md)
   - Source repository: <https://github.com/lyndonkl/claude>
2. **First Principles Thinking** — use before architecture/splitting decisions and whenever inherited assumptions may be driving campaign structure, landing creation, keyword expansion, or exclusions.
   - Skill: [`first-principles-skill`](https://github.com/awesome-skills/first-principles-skill/blob/main/SKILL.md)
   - Source repository: <https://github.com/awesome-skills/first-principles-skill>

### Invocation policy

- Before **Phase 2 — Architecture**, apply First Principles Thinking: identify the actual business objective, challenge inherited campaign/page structure, separate facts from assumptions, and reason upward from user intent and business constraints.
- During **Phase 5 — Diverge** and **Phase 7 — Converge**, apply Brainstorm Diverge-Converge. Divergence must generate genuinely different semantic concepts rather than permutations; convergence must preserve unresolved candidates and state why each survivor/rejection was chosen.
- During **Phase 11 — Ads**, use another short diverge → cluster → converge pass for headlines/text angles.
- If the companion skill is installed and the agent/harness supports skill composition, read/invoke it. If not, do **not** block the workflow: execute the equivalent method specified here.
- Never let a companion skill override verified Yandex rules, business facts, user corrections, or the campaign state ledger.

## Non-negotiable operating principles

1. Start from business truth. Never invent products, prices, guarantees, delivery areas, deadlines, certifications, materials, or capabilities.
2. Verify current Yandex behavior before volatile decisions. Prefer official Yandex Direct, Wordstat, Metrica, Webmaster, and Yandex Business documentation.
3. Cite sources for factual claims about Yandex rules, limits, operators, formats, strategy behavior, moderation, URL parameters, analytics, or SEO.
4. Treat current UI validation as operational evidence. If current official docs and the live interface appear to disagree, explicitly flag the conflict and do not force syntax the interface rejects.
5. Preserve state. Never silently forget or overwrite a previously accepted decision.
6. Separate fact, inference, hypothesis, temporary decision, and final decision.
7. One ad group represents one independent search intent, not one keyword and not one product card.
8. Do not create new landing pages merely because a keyword exists. Require intent/data/CRO/SEO justification.
9. Do not expand a semantic core by mechanically permuting words. Explore genuinely different ways users conceptualize the product.
10. After launch, Search Terms become the primary source of truth for semantic cleanup and expansion.

## Required context recovery

Before making a decision in an ongoing campaign:

1. Read the current conversation and all relevant handoff/state files.
2. Recover the latest accepted campaign settings, group registry, URLs, analytics goals, exclusions, unresolved questions, and temporary workarounds.
3. If the user references prior work that is not visible, retrieve it from available memory/files before asking them to repeat it.
4. Before changing a previous decision, state what the prior decision was and why new evidence justifies changing it.
5. At the end of each meaningful phase, update the state ledger/handoff.

Use `references/state-ledger.md` and `assets/campaign-handoff-template.md`.

## Phase 0 — Refresh sources

Before campaign architecture or when returning after a material break, refresh the relevant official documentation.

At minimum verify when relevant:

- EPK / campaign creation and current ad formats;
- manual and automatic strategies;
- keywords and semantic matching;
- negative keywords and negative phrases;
- operators;
- autotargeting and its categories;
- campaign/group/ad URL parameter hierarchy;
- ad text limits and moderation;
- Wordstat Top queries, Similar queries, operators, regions, device filters;
- Metrica goals and UTM reporting;
- Webmaster canonical, indexing, region/local signals when landing decisions are involved.

Do not treat cached reference files as authoritative for volatile limits. They are a checklist and a last-verified snapshot only.

## Phase 1 — Product and business discovery

Establish what is actually being advertised before touching keywords.

Collect or verify:

- exact products/services and boundaries between them;
- what is not sold;
- service geography and whether extended geo targeting is appropriate;
- B2C/B2B segments and whether their intents materially differ;
- average order, margin or target CPL/CPA when available;
- operational capacity, schedule, lead handling hours, and seasonality;
- current website/page structure;
- existing landing states, query-parameter states, catalogs, forms, phone and messengers;
- true competitive advantages and claims that can be substantiated;
- available photos/projects/proof;
- legal/moderation restrictions for the category;
- analytics counter, macro conversion, micro conversions, call tracking, CRM/offline conversion availability;
- historical Direct data, but label it as baseline rather than destiny.

Do not proceed on an ambiguous product boundary. Resolve whether two phrases describe the same capability, a different use case, or a genuinely different product.

## Phase 2 — Architecture from first principles

Decide campaigns, groups, and landing mapping before final semantics.

### Split into separate campaigns when a real control boundary exists

Examples:

- different business objective;
- different geography;
- different strategy or billing logic;
- materially different budget/risk envelope;
- different schedule/capacity;
- brand vs generic vs competitor test;
- an intentionally isolated experiment.

Do not split only because keyword wording differs.

### Split into separate groups when search intent is independently actionable

A group deserves separation when several of these are true:

- the user means a distinct product/job-to-be-done;
- it deserves different ad language;
- it maps to a different landing state or first screen;
- it needs different negatives/autotargeting controls;
- it may justify a different bid;
- post-launch Search Terms should be evaluated independently.

### Split landing pages only with evidence

Prefer the smallest site architecture that can honestly satisfy the intents.

Possible mapping:

- one existing page for multiple tightly related groups;
- one page with intent-aware query parameter state;
- a dedicated landing only when the intent/content depth, conversion behavior, SEO evidence, or user experience actually demands it.

Do not create dozens of SEO pages before demand is validated.

## Phase 3 — Measurement and landing readiness

Before launch, verify the landing and analytics layer. Read `references/landing-seo-cro-analytics.md`.

Minimum launch gate:

- destination returns correctly and works on mobile;
- first screen matches the group intent and ad promise;
- the promoted product/service actually appears on the destination;
- canonical/robots/indexing behavior is intentional;
- dynamic landing state, if used, is tested with UTM parameters present;
- forms and messenger/phone actions work;
- macro conversion fires correctly in Metrica;
- UTM attribution is testable;
- contact data and regional signals are accurate;
- no unsupported advertising claim is present.

Keep a campaign draft/off until critical landing and analytics checks pass.

## Phase 4 — Wordstat round 1

Research before writing final keywords.

### Build seed roots

Generate broad but meaningful roots from:

- the product's ordinary customer name;
- professional/industry names users may know;
- direct synonyms;
- core use cases/locations of use;
- alternative jobs-to-be-done;
- adjacent terms that may reveal a hidden intent.

Do not generate dozens of trivial permutations such as `product city`, `product price`, `product order` as separate research roots when the base Wordstat root will already reveal those tails.

### Request/export data

For each meaningful root, use Wordstat with the actual campaign region and a deliberate device filter. Save the exported CSV files.

Prefer both:

- Top queries;
- Similar queries.

For every imported Wordstat file, record:

- seed query;
- Top vs Similar;
- date range;
- region;
- device filter;
- file name/reference.

Never pretend to have read an attachment that has not actually been inspected.

Optional helper: `scripts/wordstat_index.py`.

## Phase 5 — Diverge

Use divergent brainstorming to find semantic gaps, not word-order variants.

Ask:

- What else does the customer call this product?
- What problem are they solving?
- What physical place/use case changes the language?
- What construction/type/material term might indicate the same purchase?
- What adjacent query could conceal valuable demand?
- What competitor/retail/informational meanings contaminate the root?

Tag each candidate as:

- core product name;
- synonym;
- use case;
- construction/material modifier;
- commercial modifier;
- adjacent hypothesis;
- likely noise.

## Phase 6 — Wordstat round 2

Only re-query genuinely new semantic roots discovered during divergence or Similar queries.

Use research negatives in Wordstat when a valuable root is buried under an unrelated meaning, but keep them conservative. The goal is discovery, not premature exclusion.

Do not confuse Wordstat research negatives with final Direct negatives.

## Phase 7 — Converge

Reduce the semantic field to a compact root core.

A final keyword should normally survive these tests:

1. It represents a real way users name the offered product/service or a strategically useful intent.
2. It has enough evidence to justify explicit control.
3. It is not merely a predictable tail already captured by a broader root.
4. It is not so broad that negatives cannot make it commercially coherent.
5. It can share the group's ad and landing intent without misleading users.

Do not add `city`, `price`, `buy`, `order`, `custom`, dimensions, colors, or similar tails as separate keys by default. Add them only when they need their own control, ad/landing, bid, or measurement.

Do not sum overlapping Wordstat counts and present the result as unique demand.

## Phase 8 — Keywords and local negative keywords

Produce the final root list first.

Then decide whether any individual keyword needs local `-word` exclusions.

Use a local negative keyword only when:

- the unwanted meaning is specific to that root;
- the same word could be valuable in another root/group;
- the exclusion is safe as a single word.

If the exclusion should apply to the whole group, use group negative phrases instead of repeating it on every keyword.

Do not decorate every keyword with negatives merely for appearance.

## Phase 9 — Negative phrases

Build negatives at the narrowest correct scope:

- keyword-local: root-specific ambiguity;
- group: common noise for this intent and protection for group-level targeting/autotargeting;
- campaign: truly global exclusions shared by every group.

Prefer intent-specific negative phrases over dangerous single-word exclusions.

Do not automatically negative these commercial/research modifiers without evidence:

`price`, `cost`, `buy`, `order`, `custom`, `installation`, `mounting`, `photos`, `sizes`, `reviews`.

A user searching these may be highly commercial.

### Operator rules

Always refresh the official operator documentation before complex syntax. The conservative working rules are:

- `-` excludes a word/phrase according to current Direct/Wordstat rules;
- `!` fixes the word form;
- `+` fixes a stop-word when its presence changes meaning;
- `""` fixes the number of words and prevents additional words;
- `[]` fixes word order; Wordstat/Direct documentation states that stop-words are considered inside the bracketed order;
- `()` and `|` group alternatives where supported.

Compatibility rule for generated negatives: **do not place `+` inside `[]`**. Square brackets already account for stop-words in the ordered sequence, and some current UI fields may reject or mishandle the combined form. If both behaviors appear necessary, rewrite the phrase or verify the exact syntax in the live interface before saving.

Use `[]` only when word order is essential to distinguish a bad intent from a good one. Do not bracket every negative phrase.

Read `references/semantics-negatives-operators.md` before producing complex negatives.

## Phase 10 — Autotargeting

Verify current EPK requirements and categories from official docs.

For a new Search campaign where control and query learning are priorities, start conservatively unless the project gives evidence for broader categories. Typical conservative logic may include target/narrow categories and exclude broad/alternative/adjacent categories, but never copy this as a universal preset.

Check whether group/campaign negatives apply to the selected autotargeting behavior in current documentation.

Under manual bidding, explicitly review the autotargeting bid rather than assuming it is harmless.

## Phase 11 — Ads: brainstorm then converge

Verify the current EPK ad format before writing copy.

For combinatorial ads:

1. Brainstorm more candidates than required.
2. Cover different angles rather than superficial rewrites:
   - exact product;
   - synonym/customer language;
   - use case;
   - custom manufacturing/service process;
   - geography;
   - verified advantage/proof;
   - low-friction CTA.
3. Converge to the current maximum useful set supported by Direct.
4. Ensure every selected headline can pair sensibly with every selected text.
5. Check character and punctuation limits programmatically or manually.
6. Keep the promoted object explicit.
7. Never invent comparative/superlative claims, price floors, deadlines, guarantees, certifications, or discounts.
8. Ensure the landing page supports every material claim.

## Phase 12 — URLs and parameter hierarchy

Verify the current Yandex priority rules before implementation.

Prefer a clean hierarchy:

- campaign-level parameters for common UTM/dynamic tracking;
- group/ad URL-parameter fields empty unless a deliberate override is required;
- business routing parameters such as `service=` in the actual landing URL when they control page state;
- canonical pointing to the intended clean canonical URL when query states should not become separate SEO pages.

Remember that URL-parameter blocks can override same-named parameters already present in the ad link, and ad-level settings outrank group-level settings, which outrank campaign-level settings under current EPK rules.

Never conflate an analytics parameter with a landing-state parameter.

## Phase 13 — Bids, budget, geo, schedule

Choose strategy from business conditions, not habit.

Manual Search bidding is a strong candidate when:

- the campaign is new;
- high-quality macro-conversion volume is low;
- query control/learning is a priority;
- the operator can review Search Terms and bids frequently.

Automatic strategies may be better when reliable conversion volume, values, budgets, and tracking support them.

For manual bidding:

- derive a sustainable CPC from business economics and expected CVR where possible;
- treat the configured bid as a ceiling/control, not a target actual CPC;
- avoid chasing the highest traffic tier merely for position;
- set schedules from lead handling/capacity, not arbitrary convention;
- keep geo choices aligned with actual service ability.

## Phase 14 — Moderation preflight

Before sending ads to moderation, verify current rules and check:

- object of promotion is clear;
- ad, keywords, and destination are mutually relevant;
- destination works and contains the promoted offer;
- claims are factual and supportable;
- comparative/superlative claims have required substantiation;
- restricted-category documents/warnings are handled when applicable;
- display link is relevant;
- images and text meet current technical restrictions;
- contact information is used only where current rules allow it.

## Phase 15 — Launch gate

Do not launch merely because the campaign form is complete.

Require explicit pass/fail for:

- product truth;
- landing relevance;
- URL state;
- UTM attribution;
- macro conversion;
- form/phone/messenger flow;
- geo/schedule;
- bids/budget;
- negatives;
- autotargeting;
- moderation risks;
- mobile experience.

## Phase 16 — Post-launch learning loop

Review Search Terms frequently at the beginning.

Classify each meaningful query:

- strong target -> keep; consider explicit keyword/bid if it deserves control;
- target but weak economics -> evaluate bid/ad/landing before excluding;
- irrelevant -> add the narrowest safe negative at keyword/group/campaign scope;
- competitor -> do not auto-negative; judge spend and lead quality;
- new intent -> research before splitting a group or creating a landing;
- repeated high-volume intent -> consider dedicated ad/landing state only when evidence supports it.

Do not optimize only for CTR. Prioritize qualified leads, CPA/CPL, conversion quality, and business outcomes.

## Mandatory deliverables

For a complete campaign, produce and maintain:

1. Campaign brief and verified business facts.
2. Campaign architecture and reasoning.
3. Landing/analytics readiness audit.
4. Wordstat source index.
5. Per-group research notes: round 1, divergence, round 2, convergence.
6. Final keywords including any root-specific negative words.
7. Group/campaign negative phrases with rationale for dangerous exclusions.
8. Autotargeting settings and rationale.
9. Final destination URL, display link, and URL-parameter plan.
10. Ad brainstorm and final selected headlines/texts.
11. Bid/budget/schedule/geo logic.
12. Moderation preflight.
13. Launch checklist.
14. State ledger/handoff with open questions and next action.

Use `assets/group-workbook-template.md` for each group.

## Response discipline

- Be verbally precise.
- Quote exact settings/strings when the user is entering them into Direct.
- Do not silently simplify a previously accepted list.
- Do not say a group is final while a named candidate is still pending research.
- When the user corrects a UI/operator detail, preserve that correction in project state and verify it against current docs before future reuse.
- If uncertain, say what is known, what is inferred, and exactly what data is needed next.
- Prefer a small correct semantic core over a large decorative list.
