# ShelfSignal — Structured Outputs & AI-Driven UI

**Less guesswork. More shelf appeal.** ShelfSignal is a new merchandising-planning product for independent retailers. It is separate from Gatherwell and CoinPilot.

The Phase 2 submission demonstrates a strict output schema, typed React components, explicit validation/fallback states, rendering tests, locale metadata, and a server-only Groq integration through the Vercel AI SDK.

## Submission

**Repository:** https://github.com/PenielOkoli/shelfsignal-phase-2

**Live app:** https://shelfsignal-phase-2.vercel.app

Deployment and live Groq generation are verified. Both supported locales produced valid plans that rendered through the actual React components. See [deployment status](docs/deployment.md) and [live verification evidence](docs/live-verification.json).

- [Output schema](src/lib/schema.ts)
- [Typed UI components](src/components/plan-view.tsx)
- [Interactive studio and fallback-state lab](src/components/studio.tsx)
- [Schema and boundary tests](tests/schema.test.ts)
- [Rendering edge-case tests](tests/rendering.test.tsx)
- [Architecture and data-flow notes](docs/architecture.md)
- [Assessment checklist and evidence](docs/assessment.md)
- [New product brief](docs/product-brief.md)
- [Security and operational limits](docs/security.md)

## Try it

1. Review the initial **Sample data** plan. It is curated fixture data, not a model result.
2. Edit the shop brief or choose a preset.
3. Click **Generate with Groq**. With a configured key, this makes a real model request and replaces the plan only after validation.
4. Review display cards, the catalog-backed priority table, and the action checklist.
5. Open **Test states** and select missing cards, invalid priority, unexpected field, truncated JSON, or HTML-like text.
6. Open **JSON** to inspect the response. Export is enabled only for a completely validated plan; the export records whether its source is sample, test, or Groq.

The checklist is in-memory session state. No external store, database, purchases, or inventory mutations are connected. Catalog stock and prices are sample facts owned by the application.

## Run locally

Requires Node.js 22.x and npm.

```sh
npm ci
# Copy .env.example to .env.local and add GROQ_API_KEY for live generation.
npm run dev
```

The sample and validation lab work without an API key. Missing configuration produces a visible error when live generation is requested; the app never silently substitutes a sample for live AI.

```sh
npm run typecheck
npm test
npm run build
```

`npm run check` runs all three. The test suite includes actual React rendering via `renderToStaticMarkup`, not only schema checks.

## Configure Groq

Add `GROQ_API_KEY` to the **Production** environment in Vercel project settings and redeploy. The default model is `openai/gpt-oss-20b`, served by Groq. `GROQ_MODEL` can override it with another Groq model that supports strict structured outputs. Set `AI_ENABLED=false` to disable live requests.

The provider key stays in a `server-only` module. There is no `NEXT_PUBLIC_` key, no API-key form in the public UI, and no provider secret in source control. The application uses `generateText` with `Output.object({ schema: planSchema })` and Groq strict JSON schema mode.

## What this proves

The model is asked for a machine-readable contract, not prose that is later split with regular expressions. Narrative text lives under `summary`; rendering data lives under `cards`, `priorities`, and `actions`; metadata lives under `schemaVersion`, `locale`, and `currency`. React components receive validated inferred types. Partial or invalid content is represented as a state, not cast into a trusted object.

Shape validation cannot guarantee factual correctness or commercial usefulness. Recommendations require human review. Read the documented limits before treating the public learning prototype as a production system.
