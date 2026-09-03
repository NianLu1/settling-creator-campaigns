---
name: settling-creator-campaigns
description: Use when processing creator campaign settlement workbooks containing submissions, platform links, views, tiered rewards, prize pools, or ranking awards, especially when Bilibili and Douyin data must be reconciled and written into an Excel settlement sheet.
---

# Settling Creator Campaigns

## Purpose

Turn campaign rules and submission data into an auditable settlement workbook. Preserve three layers separately: source facts, confirmed business rules, and calculated results. Never silently convert ambiguity into a payout decision.

**REQUIRED SUB-SKILL:** Use `spreadsheets:Spreadsheets` for workbook reading, editing, rendering, and verification.

## Workflow

1. Read the campaign rules before calculating. Extract eligibility, thresholds, stacking, caps, ordering, deduplication, ranking, and exclusions.
2. State the interpreted rules and ask only about unresolved items that can change payouts. Record the user's answers as authoritative for this run.
3. Inspect the workbook before editing. Identify the source sheet, output sheet, headers, data types, formulas, tables, and formatting. Use the designated source sheet as the calculation source; platform sheets are supporting sources unless the user says otherwise.
4. Normalize identifiers and platforms without changing raw cells. Distinguish numeric zero from blank, invalid, or unmatched views.
5. Resolve platform data when requested:
   - Bilibili: open the submitted page or resolve its short link, then read the page's video view count.
   - Douyin: resolve the short link to its numeric video ID, convert it to the canonical ID/link form, then match that ID to the delivery dataset link field and copy the matched view count.
   - Keep unresolved, expired, wrong-platform, and unmatched links blank and list them as exceptions. Do not invent zero.
6. Aggregate by the confirmed creator key, normally the creator-community ID. Retain platform-specific post counts and views plus combined totals.
7. Apply rewards in this order: per-platform single-item reward, highest eligible tier, prize-pool allocation, ranking reward, then total payout. Keep theoretical and actual tier amounts separate when a pool cap exists.
8. Write results into the requested output sheet, preserving an existing template. If it is empty, create one row per creator with traceable formulas and a compact methodology note.
9. Verify reconciliations, thresholds, caps, rankings, formula errors, and rendered layout. Reopen the exported workbook and verify key totals before reporting completion.

## Data Contracts

- Creator grouping key must be explicit. Do not group by display name when a stable ID exists.
- The same work posted to two platforms counts according to the user's confirmed cross-platform rule; do not assume deduplication across platforms.
- A value of `0` is known zero. Blank/non-numeric/unmatched is missing and remains unresolved.
- Repeated identical links or identical platform video IDs are potential duplicates. Retain source row numbers and flag them unless the business rule explicitly permits repetition.
- The output should expose: creator ID, creator information, first submission time, per-platform counts/views, combined counts/views, reward components, ranking basis, total, and notes/exceptions.

## Decision Points

Confirm these only when not already established by the conversation or supplied rules:

- whether reward types stack;
- whether tiers pay only the highest tier or accumulate;
- creator grouping key and cross-platform counting;
- prize-pool ordering and treatment of insufficient remaining balance;
- ranking threshold, traffic-spend deduction, and tie handling;
- whether blank views block settlement or are treated another way;
- whether eligibility/audit fields should be enforced now or deferred.

Do not re-ask questions already answered earlier in the task. Treat later user corrections as overriding earlier interpretations.

## Verification Contract

- Platform counts sum to total posts for every creator.
- Platform views sum to total views for every creator.
- Aggregated totals reconcile to included source rows.
- Blank views are not coerced to zero.
- Per-platform one-time rewards never exceed their cap.
- Tier selection follows the confirmed highest-only or cumulative rule.
- Actual tier payouts do not exceed the pool and follow the confirmed ordering.
- Ranking uses only eligible rows and applies tie rules explicitly.
- Total payout equals the sum of reward components.
- No formula errors; saved workbook reopens; all relevant sheets pass visual review.

For the reusable rules established in the originating conversation, read [references/afk-ai-campaign-rules.md](references/afk-ai-campaign-rules.md) only when the task concerns the AFK/《剑与远征》AI星河创想家计划 or asks to reuse this exact settlement logic.
