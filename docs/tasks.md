# ClimateSense – Task List

Status legend: **COMPLETED** | **IN PROGRESS** | **BROKEN** | **NOT STARTED**

**Last updated:** 2026-09-27 (post-inspection)

---

## Cross-cutting fixes (before / during Phase 2)

| Task | Status | Notes |
|------|--------|-------|
| Remove or reorder Google Fonts `@import` in `globals.css` (use `next/font` only) | **BROKEN** | Blocks `npm run dev` / Turbopack |
| Fix ESLint errors (login/register `Link`, unescaped entities) | **BROKEN** | `npm run lint` fails |
| Move `viewport` / `themeColor` to `generateViewport` (Next 16) | **IN PROGRESS** | Build warnings only |
| Initialize git repository (if desired) | **NOT STARTED** | Claimed in Phase 1 log but missing |
| Complete shadcn/ui init + base components OR document custom UI approach | **IN PROGRESS** | Radix deps only |
| Wire `next-themes` OR keep documented manual theme approach | **IN PROGRESS** | Manual toggle on landing today |

---

## PHASE 1: Project setup, architecture, landing page & design system

> **COMPLETED** (see caveats in `docs/progress.md`)

### Setup & docs
- [x] **COMPLETED** — README, requirements, architecture, progress, tasks
- [x] **COMPLETED** — `.env.example` (root)

### App initialization
- [x] **COMPLETED** — Next.js + TypeScript + App Router (`climatesense-app/`)
- [x] **COMPLETED** — Tailwind CSS v4
- [~] **IN PROGRESS** — shadcn/ui (dependencies only)
- [~] **IN PROGRESS** — next-themes (package only)
- [x] **COMPLETED** — `.env.local` template in app
- [ ] **NOT STARTED** — Git repo / first commit (not found in workspace)

### Design system
- [x] **COMPLETED** — Color tokens, typography (Inter via next/font + duplicate CSS import)
- [x] **COMPLETED** — `LandingNavbar`, `LandingFooter`

### Landing page sections
- [x] **COMPLETED** — All 13 marketing sections with DEMO labeling where appropriate

### Phase 1 verification
- [x] **COMPLETED** — `npm run build` succeeds
- [ ] **BROKEN** — `npm run dev` (CSS `@import` order)
- [ ] **BROKEN** — `npm run lint` clean
- [x] **COMPLETED** — Landing content and responsive layout (via production build)

---

## PHASE 2: Database, authentication, roles & RBAC

> **NOT STARTED**

### Database setup
- [ ] **NOT STARTED** — Supabase project
- [ ] **NOT STARTED** — Prisma + `DATABASE_URL`
- [ ] **NOT STARTED** — Full Prisma schema per architecture
- [ ] **NOT STARTED** — Migrations / `db push`
- [ ] **NOT STARTED** — RLS policies
- [ ] **NOT STARTED** — Seed (roles, emission factors demo, system admin)

### Authentication
- [ ] **NOT STARTED** — Supabase Auth client utilities
- [~] **IN PROGRESS** — Registration page (placeholder UI only)
- [~] **IN PROGRESS** — Login page (placeholder UI only)
- [ ] **NOT STARTED** — Logout
- [ ] **NOT STARTED** — Forgot / reset password
- [ ] **NOT STARTED** — Session cookies / SSR session
- [ ] **NOT STARTED** — Middleware for protected routes

### User roles & RBAC
- [ ] **NOT STARTED** — Role enum + assignment on signup
- [ ] **NOT STARTED** — API route guards
- [ ] **NOT STARTED** — Frontend route guards
- [ ] **NOT STARTED** — System admin seed (no public registration)

### User profiles
- [ ] **NOT STARTED** — Profile page + edit
- [ ] **NOT STARTED** — Avatar upload
- [ ] **NOT STARTED** — Location + preferences

### Phase 2 verification
- [ ] **NOT STARTED** — End-to-end register / login / logout / protected routes

---

## PHASE 3: Individual dashboard & climate calculator

> **NOT STARTED**

- [ ] **NOT STARTED** — Dashboard layout (sidebar + topbar)
- [ ] **NOT STARTED** — Dashboard widgets (real DB data)
- [ ] **NOT STARTED** — Multi-step calculator + emission factors from DB
- [ ] **NOT STARTED** — Save assessments; ESTIMATE labeling

---

## PHASE 4: Analytics & charts

> **NOT STARTED**

- [ ] **NOT STARTED** — Analytics page + Recharts
- [ ] **NOT STARTED** — `/api/analytics` + time filters

---

## PHASE 5: Goals, action plans & progress tracking

> **NOT STARTED**

- [ ] **NOT STARTED** — CRUD goals, action plans, progress records

---

## PHASE 6: ML prediction service

> **NOT STARTED**

- [ ] **NOT STARTED** — `ml-service/` FastAPI project
- [ ] **NOT STARTED** — `/api/predictions` proxy
- [ ] **NOT STARTED** — Predictions UI with PREDICTION labels

---

## PHASE 7: AI recommendations

> **NOT STARTED**

- [ ] **NOT STARTED** — `/api/ai/analyze` + Gemini + DEMO mode without key

---

## PHASE 8: AI Climate Assistant

> **NOT STARTED**

- [ ] **NOT STARTED** — Chat UI + `/api/ai/chat` + conversation storage

---

## PHASE 9: Climate risk module & interactive map

> **NOT STARTED**

- [ ] **NOT STARTED** — Leaflet map page + DEMO dataset from DB
- [~] **IN PROGRESS** — Landing marketing section with DEMO MAP (not functional map)

---

## PHASE 10: Organization dashboard & management

> **NOT STARTED**

---

## PHASE 11: Admin dashboard & audit logs

> **NOT STARTED**

---

## PHASE 12: Reports, notifications & gamification

> **NOT STARTED**

---

## PHASE 13: Accessibility, security, testing & polish

> **NOT STARTED** (partial a11y on landing only)

- [ ] **NOT STARTED** — Unit / API / e2e tests (`npm run test` scripts missing)
- [ ] **NOT STARTED** — Rate limiting, CORS, audit logging

---

## PHASE 14: Deployment

> **NOT STARTED**

---

## Immediate next actions (continuation plan)

1. **BROKEN → COMPLETED:** Fix `globals.css` font import so dev server runs.
2. **BROKEN → COMPLETED:** Fix ESLint issues on auth + landing pages.
3. **NOT STARTED → IN PROGRESS:** Phase 2 — Supabase, Prisma schema, real login/register, middleware.
4. Incrementally build Phase 3+ only after Phase 2 verification passes.

Do **not** duplicate landing mockups as fake dashboard APIs; wire real data from Phase 2 onward.
