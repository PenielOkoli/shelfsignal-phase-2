# Deployment and configuration

Vercel project: `shelfsignal-phase-2`, in the existing `penielokolis-projects` team.

- Repository: https://github.com/PenielOkoli/shelfsignal-phase-2
- Live production app: https://shelfsignal-phase-2.vercel.app
- Environment settings: https://vercel.com/penielokolis-projects/shelfsignal-phase-2/settings/environment-variables

Verified on 24 October 2026: Vercel production build succeeded; home and guide return HTTP 200. GROQ_MODEL=openai/gpt-oss-20b and AI_ENABLED=true are saved in Production, Preview, and Development. GROQ_API_KEY is still awaiting owner entry. Redeployment and real model verification will follow key setup.

The deployed API correctly returns 400 for invalid input, 403 for a foreign Origin, 415 for non-JSON input, 413 for an oversized request, and 503 for missing provider configuration.

## Enable Groq

1. Open the project's Vercel Settings → Environment Variables.
2. Add `GROQ_API_KEY` to Production. Do not prefix it with `NEXT_PUBLIC_`.
3. Optionally set `GROQ_MODEL=openai/gpt-oss-20b`; this is already the default.
4. Redeploy. The server-rendered configuration indicator should read “Groq connected”.
5. Generate a plan and confirm the result is labeled “Groq output” and “Schema verified”.

Keep the key out of chat, screenshots, source code, and public forms. Adding the environment variable without redeploying does not update an existing deployment's environment.

## Reproduce

Import the repository into Vercel using the Next.js preset, repository root, Node.js 22.x, `npm ci`, and `npm run build`. Do not use static export: `/api/plan` requires the server runtime.

The sample plan and fault lab work before the key is configured. Actual live AI validation remains pending until a key is configured and a successful model request is observed. A sample response is never evidence that a live model call succeeded.
