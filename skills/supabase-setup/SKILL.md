---
name: supabase-setup
description: Supabase project setup and integration skill. Use when scaffolding Supabase auth, database schema, Row Level Security (RLS), storage buckets, edge functions, or connecting Supabase to a frontend (Next.js, Vite, Nuxt). Covers CLI workflow, type generation, and local dev setup.
---

## Init
```powershell
supabase init
supabase link --project-ref <ref>
supabase db pull
supabase start  # requires Docker
supabase gen types typescript --linked > src/types/supabase.ts
```

## Client (TypeScript)
```typescript
import { createClient } from '@supabase/supabase-js'
import type { Database } from '@/types/supabase'
export const supabase = createClient<Database>(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
)
```

## Auth
```typescript
supabase.auth.signUp({ email, password })
supabase.auth.signInWithPassword({ email, password })
supabase.auth.getSession()
supabase.auth.signOut()
```

## RLS (every table)
- [ ] `ALTER TABLE <t> ENABLE ROW LEVEL SECURITY;`
- [ ] SELECT: own rows only | INSERT/UPDATE/DELETE: `auth.uid() = user_id`
- [ ] Service role bypasses RLS — never expose to client

## Migrations
```powershell
supabase migration new <name>
supabase db reset   # apply locally
supabase db push    # push to remote
```

## Storage
```typescript
await supabase.storage.from('bucket').upload('path', file, { upsert: true })
supabase.storage.from('bucket').getPublicUrl('path')
```

## Env
| Var | Where |
|---|---|
| `NEXT_PUBLIC_SUPABASE_URL` | `.env.local` + Vercel |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | `.env.local` + Vercel |
| `SUPABASE_SERVICE_ROLE_KEY` | Vercel only — never client-side |
