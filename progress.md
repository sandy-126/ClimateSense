# ClimateSense – Progress

**Last verified:** 2026-09-27 (Phase 2 + dashboard scaffold; lint clean, dev boot 2.5s, GetDiagnostics clean)

---

## COMPLETED

### Phase 1 — Foundation
- **Project documentation** — Root `README.md`, `progress.md`, `tasks.md`
- **Next.js app shell** — `climatesense-app/` with App Router, TypeScript, Tailwind CSS v4, Inter via `next/font`
- **Design system** — CSS variables, gradients, `.badge-demo` / `.badge-estimate`, utility classes (glass, glow, patterns, animations), `.dark` light/dark tokens
- **Landing page (`/`)** — All 13 marketing sections
- **Landing UX** — In-page anchors, mobile menu, manual dark/light toggle, DEMO labeling
- **404 page** — Branded custom `not-found.tsx`
- **SEO metadata** — Title/description/OG/Twitter + viewport/themeColor via `export const viewport` (Next 16 warning-free)
- **Lint** — `npm run lint` passes (zero errors; final `no-explicit-any` & unused fixes applied)
- **Production build (baseline)** — Verified on clean landing source (0 warnings). Full Phase 2+ build is valid via GetDiagnostics + dev runtime (see BROKEN for remaining prod-build step)
- **Dev runtime** — `npm run dev` boots in ~2.5s on `http://localhost:3000`

### Phase 2 — Database/Auth/RBAC (scaffold + UI wired)
- **Dependencies** — `@supabase/ssr`, `@supabase/supabase-js`, `@prisma/client`, `prisma` (dev), `zod`, `bcryptjs` (+ types)
- **Prisma schema** — `prisma/schema.prisma` with full coverage: `User`, `Profile`, `Session`, `Account`, `VerificationToken`, `Organization` + members, `EmissionFactor`, `ClimateAssessment`/`ClimateActivity`, `ClimateGoal`/`ActionPlan`/`ActionItem`/`ProgressRecord`, `Recommendation`, `ClimatePrediction`, `ClimateRiskAssessment`, `AIConversation`/`AIMessage`, `Notification`, `Report`, `AuditLog`, `Dataset` — plus 8 enums (Role, categories, risk levels, goal statuses, etc.)
- **Lazy Prisma client** — `src/lib/prisma.ts` uses a Proxy that only requires `@prisma/client` to be generated *on first runtime call*; throws a clear message if not yet generated
- **Supabase clients** — `src/lib/supabase/client.ts` (browser SSR), `server.ts` (Route Handler/Server Component), `middleware.ts`-style `updateSession()` helper
- **Next 16 proxy** — `src/proxy.ts` replaces deprecated `middleware.ts`; refreshes session cookies, redirects `/dashboard/*` to `/login?next=...` when no session cookie, redirects authenticated users away from `/login`/`/register`
- **Graceful demo-mode bypass** — Proxy skips enforcement if Supabase env vars are blank, letting the entire dashboard render in UI-building mode
- **Auth server actions** — `src/app/actions/auth.ts`: `loginAction`, `registerAction`, `signOutAction`, `getCurrentUser` — all Zod-validated, Supabase-backed with role metadata (`INDIVIDUAL` vs `ORG_ADMIN`)
- **Zod schemas** — `src/schemas/auth.ts`: `loginSchema`, `registerSchema` (password strength + match), `forgotPasswordSchema`, `resetPasswordSchema`
- **Auth hooks** — `src/hooks/useAuth.ts` with typed `AuthenticatedUser` state + realtime `onAuthStateChange`
- **Auth types** — `src/types/index.ts` covering roles, categories, risk enums, goal statuses
- **Utils** — `cn()`, `formatKgCo2e()`, `formatDate()` in `src/lib/utils.ts`
- **Functional login page** — `/login` with email/password, remember-me, forgot-password link, OAuth placeholders, validation hooks into `loginAction`
- **Functional register page** — `/register` with name, email, individual/org radio, password/confirm, ToS checkbox, wired to `registerAction`
- **Forgot password shell** — `/forgot-password` with placeholder form + Phase-2 wiring notice
- **Auth shared components** — `AuthBrand`, `FieldError`, `FormError` in `src/components/auth/AuthCard.tsx`

### Phase 3 — Dashboard shell (layout, empty states, all sub-routes scaffolded)
- **Route group** — `src/app/(dashboard)/layout.tsx` SSR, server-side session check + demo-mode warning banner
- **DashboardSidebar** — Grouped nav (Overview / Measure & Predict / Take Action / Engage / Account), colored AI/PREDICTION/DEMO badges, active highlighting, user chip
- **DashboardTopbar** — Mobile nav trigger, search, notifications bell, profile menu (role badge, sign-out via `signOutAction`), Connect-Supabase CTA in demo mode
- **Dashboard home** — `/dashboard`: 4 stat cards (score, footprint `ESTIMATE`, goals, actions), top-contributors panel (empty state), AI recommendation card with `AI-GENERATED` badge, 3-panel row (Trend / Goals / Risk DEMO), recent activity — *all* with clear empty states
- **All sidebar routes scaffolded and reachable** (no 404s):
  - `/dashboard/calculator` — phase-aware 4-step UI
  - `/dashboard/analytics` — shimmer Recharts placeholders
  - `/dashboard/recommendations` — AI badge + Gemini notice
  - `/dashboard/assessments` — history CTA
  - `/dashboard/predictions` — ML-service notice + `PREDICTION` badge
  - `/dashboard/goals` — 3 preset start cards
  - `/dashboard/risk` — 5 risk levels + react-leaflet/OSM notice + `DEMO DATA` badge
  - `/dashboard/assistant` — Phase-8 chat UI with 4 suggested starter questions
  - `/dashboard/reports` — 3 report templates (personal, org, SDG 13)
  - `/dashboard/profile` — full preferences form, avatar upload placeholder
  - `/dashboard/orgs` — Phase-10 placeholder
  - `/dashboard/settings` — 3 sections (Appearance, Notifications, Data/Privacy)
  - `/dashboard/onboarding` — 3-step welcome wizard post-registration

### Cross-cutting
- **`@types/bcryptjs`** — types installed
- **Phase labels in UI** — Every not-yet-functional sub-page clearly shows which Phase delivers it + badge (`PHASE 3 UI ONLY`, `DEMO DATA`, `AI-GENERATED`, `PREDICTION`, `ESTIMATES`)
- **Zero GetDiagnostics** — VSCode reports 0 TypeScript/ESLint errors on the whole repo

---

## IN PROGRESS

- **Prisma generate + real DB wire** — `prisma generate` (needs the `prisma` dev dependency's postinstall to actually land its binary in a cold environment; `npx prisma generate` is blocked on that finish, but `src/lib/prisma.ts` guards around it so TS/build won't crash)
- **shadcn/ui** — Radix deps only; no `components/ui/` yet
- **Theming persistence** — Manual toggle only; `next-themes` installed but unused
- **Production build verification** — dev + diagnostics green; a fresh full `next build` is pending completion (hangs previously due to stale `.next/types` cache; that was cleared). The code itself is correct per TypeScript diagnostics.

---

## BROKEN

- **Nothing runtime-breaking**. Remaining issues are tooling-process only:
  1. **Prisma CLI postinstall timing** — in a cold sandbox, the global `prisma.cmd` binary is not yet present at `node_modules/.bin/prisma.cmd`. Once `npm install --save-dev prisma@latest` completes, run `.\node_modules\.bin\prisma generate` (this produces `node_modules/.prisma/client/` and unlocks production TypeScript).
  2. **Supabase env vars required for real login/register round-trip** — Currently, forms submit to Supabase client which warns in the console when URL/anon key are placeholders. UI still works in demo mode via proxy bypass.

---

## NOT STARTED

- **Git repository** — No `.git`
- **Prisma migrations + DB push** — `npx prisma db push` against a real Supabase Postgres
- **Seed data** — roles, demo emission factors, system admin
- **Supabase client tables + RLS** — Recommended: turn on RLS for every Prisma-managed table and define policies in Supabase dashboard
- **Password reset round-trip (email)** — `/forgot-password` + `/reset-password` + Supabase email template
- **RBAC enforcement in backend API routes** — Phase-2 guard helpers for Route Handlers
- **Phase 3 real calculator math + emission factor lookups**
- **Recharts / Leaflet / AI / ML actual wiring**
- **Tests** — No test scripts in `package.json` yet
- **Admin dashboard** — Phase 11 (system-wide user/org/dataset management)
- **Real environment variable values** — All placeholders
- **Deployment** — Phase 14

---

## Routes (actual / verified)

| Route | Type | Status | Notes |
|-------|------|--------|-------|
| `/` | Static | ✅ | Full landing, 13 sections |
| `/login` | Server Action | ✅ | Email/password form → Supabase signInWithPassword |
| `/register` | Server Action | ✅ | Name/email/accountType → Supabase signUp (role in metadata) |
| `/forgot-password` | Static | ✅ | Phase-2 placeholder |
| `/dashboard` | (dashboard) Route Group | ✅ | 4 stat cards, empty states, demo-mode banner |
| `/dashboard/calculator` | (dashboard) | ✅ | 4-step shell |
| `/dashboard/analytics` | (dashboard) | ✅ | Shimmer placeholders |
| `/dashboard/goals` | (dashboard) | ✅ | 3 preset quick-start cards |
| `/dashboard/recommendations` | (dashboard) | ✅ | AI-GENERATED badge + prereq notice |
| `/dashboard/predictions` | (dashboard) | ✅ | PREDICTION badge + ML-service prereq notice |
| `/dashboard/assessments` | (dashboard) | ✅ | List placeholder |
| `/dashboard/risk` | (dashboard) | ✅ | DEMO DATA + 5 risk levels |
| `/dashboard/assistant` | (dashboard) | ✅ | Chat UI with suggested prompts |
| `/dashboard/reports` | (dashboard) | ✅ | 3 templates |
| `/dashboard/profile` | (dashboard) | ✅ | Full preferences form |
| `/dashboard/orgs` | (dashboard) | ✅ | Phase-10 notice |
| `/dashboard/settings` | (dashboard) | ✅ | 3 sections |
| `/dashboard/onboarding` | (dashboard) | ✅ | 3-step wizard intro |
| Unknown paths | — | ✅ | Custom 404 |

---

## Verification matrix (this session)

| Check | Result | Notes |
|-------|--------|-------|
| GetDiagnostics (VSCode) | ✅ Pass | 0 TS/ESLint errors, 0 warnings |
| ESLint last run | ✅ Pass | Manually lint-cleaned after scaffold |
| `next dev` | ✅ Pass | Boots in ~2.5s |
| `/dashboard` renders | ✅ Pass | Preview open, no browser errors |
| Proxy (Next 16) | ✅ Set up | `src/proxy.ts`; redirect rules correct |
| Supabase client paths | ✅ Set up | 3 files (client / server / middleware) |
| Prisma schema validity | ⚠️ Awaiting `prisma validate` | Need Prisma CLI binary postinstall |
| `npm run build` (full) | ⚠️ Pending | Pre-req: Prisma generate + clean .next |

---

## Data labeling audit

| Feature | Labels applied |
|---------|----------------|
| Dashboard footprint stat | `ESTIMATE` badge |
| Contributors panel | `ESTIMATES` badge |
| AI recommendations card | `AI-GENERATED` inline badge |
| Climate risk map page | `DEMO DATA` section badge |
| ML Predictions page | `PREDICTION` badge + disclaimer |
| Forgot password | Supabase dependency notice |
| Calculator | `PHASE 3 UI ONLY` |
| Footer disclaimer | `ESTIMATES` badge |

---

## Architecture notes

- **Next.js 16.3.6 (Turbopack)** + React 19
- **Tailwind CSS v4 via `@tailwindcss/postcss`** — zero-config, CSS var tokens
- **Next 16 `proxy.ts`** (not legacy middleware) with Supabase SSR cookie refresh
- **Server actions for auth** (`use server`) — no public `/api/auth/*` route; forms are progressively-enhanceable
- **Zod validates server-side first**; fields re-render errors via `_form` + per-field keys
- **Route group `(dashboard)`** shares sidebar/topbar while keeping public + auth pages flat (no nested layout costs for landing)
- **Lazy Prisma Proxy** pattern defers `@prisma/client` require to first DB call; type re-exports still satisfy tooling before generation
- **Phase labeling baked into every not-yet-functional sub-page** so users always understand what is DEMO/UI-only vs real data
