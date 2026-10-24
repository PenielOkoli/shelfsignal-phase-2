# Phase 2 — requirement mapping and evidence

| Requirement | Evidence |
|---|---|
| Define structured response schema | `src/lib/schema.ts`: strict Zod response and section schemas |
| Render typed components | `src/components/plan-view.tsx`: display cards, priority table, action checklist |
| Invalid/partial/missing/unexpected fields | `decodePlan` validates envelope, whole sections, IDs, enums, bounds, and locale |
| Visible schema fallback UI | SectionFallback, full invalid panel, validation lab with six scenarios |
| Separate prose from UI data | `summary` vs `cards`, `priorities`, `actions`; independent metadata |
| Rendering edge-case tests | `tests/rendering.test.tsx`, using React server rendering |
| Locale readiness | Validated locale metadata, `lang`, Intl formatting, explicit NGN currency |
| Real AI integration | `src/lib/server/groq.ts`: Groq + AI SDK `Output.object`, strict JSON schema |
| GitHub and Vercel deliverables | Final links in `docs/deployment.md` |

## Reviewer walkthrough

1. Start on the curated sample. Confirm three product cards, a real table, and checkbox actions.
2. Open Test states → Missing cards. Verify only the card section is replaced with a fallback.
3. Select Invalid priority. Verify the table is replaced while cards remain.
4. Select Unexpected field or Truncated JSON. Verify full fallback and disabled export.
5. Select HTML-like text. Verify markup is shown literally, not executed.
6. Restore the sample. Open JSON to compare fields with the rendered UI.
7. Change locale and generate a live plan once Groq is configured. Verify matching metadata and source label.

## Verification log

Verified on 24 October 2026:

- Strict TypeScript check passed.
- All 20 automated tests passed, including actual React rendering tests.
- Local production build and Vercel production build passed.
- Live home and guide pages returned HTTP 200.
- Live API boundary checks passed for invalid input (400), foreign origin (403), wrong media type (415), oversized request (413), and missing key (503).
- Live browser review confirmed the sample plan renders cards, a table, and checkboxes. Missing cards preserve the other sections and disable export. Invalid priorities replace the table only. Unexpected fields and truncated JSON produce the full fallback.
- Live Groq production requests passed for en-NG and en-GB. Both returned valid plans with three cards, three priorities, and three actions; actual React rendering accepted the responses. See `docs/live-verification.json`. One provider failure was observed before a successful retry.
- Remaining manual QA: mobile viewport and remaining browser interactions. Browser automation became unavailable during QA, so these are not claimed as completed.

Live-model verification is recorded separately from fixture tests. A fixture is never presented as evidence of a successful model request.
