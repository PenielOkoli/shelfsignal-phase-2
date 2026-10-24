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

Results will be recorded after the build, tests, browser QA, and deployment complete. Live-model verification is separately identified so a fixture cannot be mistaken for model output.
