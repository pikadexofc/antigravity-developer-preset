---
name: vercel-deploy
description: Vercel deployment workflow skill. Use when deploying projects to Vercel, managing environment variables, setting up project config, running previews, or troubleshooting deployment failures. Covers CLI, env hygiene, and rollback.
---

## Commands
```powershell
npx vercel              # preview deploy
npx vercel --prod       # production deploy
npx vercel link         # link project
npx vercel env pull .env.local  # sync env vars
npx vercel ls           # list deployments
npx vercel promote <url>  # rollback: promote old deploy to prod
$env:NITRO_PRESET="vercel"; npm run build  # Nuxt/Nitro
```

## Env Convention
| File | Commit? | Use |
|---|---|---|
| `.env.local` | ❌ | Local secrets |
| `.env.production` | ✅ non-secrets | Build-time public vars |
| Vercel Dashboard | — | All production secrets |

## Pre-Deploy Checklist
- [ ] Secrets in Vercel dashboard, not in code
- [ ] `vercel.json` added if custom routes/headers needed
- [ ] `npm run build` passes locally

## Troubleshooting
| Symptom | Fix |
|---|---|
| Build fails, works locally | `vercel env pull` → compare vars |
| 404 on routes | Add `{"rewrites":[{"source":"/(.*)","destination":"/"}]}` to `vercel.json` |
| Function timeout | Increase limit in `vercel.json` or optimize |
| Env not updating | Redeploy with `--force` |
