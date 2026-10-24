# Deployment and configuration

Vercel project: `shelfsignal-phase-2`, in the existing `penielokolis-projects` team.

Verified public links and final results will be recorded after deployment.

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
