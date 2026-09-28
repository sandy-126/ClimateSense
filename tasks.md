# ClimateSense – Task List (Simplified Scope)

Status legend: **COMPLETED** | **IN PROGRESS** | **BROKEN** | **NOT STARTED**

**Last updated:** 2026-09-27 (Simplified to demo-ready college project; Prisma removed, using static data)

---

## Cross-cutting fixes (COMPLETED)

| Task | Status | Notes |
|------|--------|-------|
| Remove duplicate Google Fonts `@import` in `globals.css` | ✅ **COMPLETED** | Use `next/font` only |
| Fix ESLint errors (login/register Link, unescaped entities) | ✅ **COMPLETED** | `npm run lint` passes |
| Move `viewport` / `themeColor` to `export const viewport` (Next 16) | ✅ **COMPLETED** | Build is warning-free |
| Migrate deprecated `middleware.ts` → `proxy.ts` (Next 16) | ✅ **COMPLETED** | `src/proxy.ts` |
| Fix TypeScript errors (React 19 form actions, Zod v4, cookies) | ✅ **COMPLETED** | All errors resolved |
| Remove Prisma dependency (using static data) | ✅ **COMPLETED** | Mock prisma.ts for compatibility |

---

## PHASE 1: Project setup, architecture, landing page & design system

> ✅ **COMPLETED**

- [x] README, progress, tasks
- [x] `.env.example` (root) + `.env.local` template in app
- [x] Next.js 16 + TypeScript + App Router
- [x] Tailwind CSS v4
- [x] Design system (tokens, utilities, badges, patterns, animations)
- [x] `LandingNavbar` + `LandingFooter`
- [x] All 13 landing sections (DEMO labels where applicable)
- [x] `npm run lint` passes
- [x] `npm run build` passes (baseline landing-only)
- [x] `npm run dev` boots in ~2.5s
- [x] Landing responsive layout + mobile menu

---

## PHASE 2: Authentication (Simplified - Demo Mode)

> ✅ **COMPLETED** — Auth UI wired to Supabase, but demo mode works without env vars

### Auth utilities + proxy (code complete)
- [x] **COMPLETED** — `src/lib/supabase/client.ts`, `server.ts` (async cookies)
- [x] **COMPLETED** — `src/proxy.ts` with session cookie refresh + protected redirects + demo-mode bypass

### Functional auth pages (UI complete)
- [x] **COMPLETED** — `/login` page with email/password form
- [x] **COMPLETED** — `/register` page with name + individual/org radio + password strength
- [x] **NOTE** — Forms work in demo mode; real auth requires Supabase env vars

### User profiles (UI shell complete)
- [x] **COMPLETED** — `/dashboard/profile` form with sections

---

## PHASE 3: Climate Calculator (STATIC DATA)

> 🔄 **IN PROGRESS** — Building functional calculator with static emission factors

### Dashboard route & layout
- [x] **COMPLETED** — Route group `(dashboard)` layout + `DashboardSidebar` + `DashboardTopbar`
- [x] **COMPLETED** — `/dashboard` landing page with stat cards and demo-mode banner

### Multi-step climate calculator
- [x] **COMPLETED** — Route `/dashboard/calculator` with 4 step indicator
- [ ] **IN PROGRESS** — Create static emission factors dataset (JSON/TS)
- [ ] **NOT STARTED** — Transport step with real fields (car, public transit, flights)
- [ ] **NOT STARTED** — Energy step (electricity, gas usage)
- [ ] **NOT STARTED** — Diet step (meat, vegetarian, etc.)
- [ ] **NOT STARTED** — Shopping step (clothing, electronics)
- [ ] **NOT STARTED** — Calculation logic using static factors
- [ ] **NOT STARTED** — Results display with breakdown by category
- [ ] **NOT STARTED** — Save to localStorage (demo persistence)

---

## PHASE 4: Analytics (STATIC DATA)

> ⏳ **NOT STARTED** — Charts using demo data

- [x] **COMPLETED** — `/dashboard/analytics` page with shimmer placeholders
- [ ] **NOT STARTED** — Recharts: footprint breakdown by category (pie chart)
- [ ] **NOT STARTED** — Recharts: monthly trend (line chart with demo data)
- [ ] **NOT STARTED** — Category comparison (bar chart)

---

## PHASE 5: Climate Goals (STATIC DATA)

> ⏳ **NOT STARTED** — Goal management with demo data

- [x] **COMPLETED** — `/dashboard/goals` page with 3 preset quick-start cards
- [ ] **NOT STARTED** — Goal creation form (target reduction, deadline)
- [ ] **NOT STARTED** — Progress tracking with visual indicators
- [ ] **NOT STARTED** — Save to localStorage

---

## PHASE 6: Action Recommendations (RULE-BASED)

> ⏳ **NOT STARTED** — Simple rule-based recommendations

- [x] **COMPLETED** — `/dashboard/recommendations` page with AI badge (will change to RULE-BASED)
- [ ] **NOT STARTED** — Rule-based recommendation engine (if transport high → suggest public transit)
- [ ] **NOT STARTED** — Static recommendation library
- [ ] **NOT STARTED** — Remove AI/ML references

---

## PHASE 7: Progress Tracking

> ⏳ **NOT STARTED** — Simple progress visualization

- [ ] **NOT STARTED** — Progress timeline view
- [ ] **NOT STARTED** — Milestone tracking
- [ ] **NOT STARTED** — Achievement badges (static)

---

## PHASE 8: Climate Risk (STATIC DATA)

> ⏳ **NOT STARTED** — Static risk data with map placeholder

- [x] **COMPLETED** — `/dashboard/risk` page with map placeholder + 5 risk summary cards
- [ ] **NOT STARTED** — Static risk dataset by region
- [ ] **NOT STARTED** — Leaflet map with demo markers
- [ ] **NOT STARTED** — Risk level indicators

---

## PHASE 9: Organization Dashboard (DEMO DATA)

> ⏳ **NOT STARTED** — Demo org dashboard with sample data

- [x] **COMPLETED** — `/dashboard/orgs` placeholder page
- [ ] **NOT STARTED** — Organization overview with demo stats
- [ ] **NOT STARTED** — Team members list (demo data)
- [ ] **NOT STARTED** — Aggregate footprint display (demo)

---

## PHASE 10: Admin Dashboard (DEMO DATA)

> ⏳ **NOT STARTED** — Demo admin panel with sample data

- [ ] **NOT STARTED** — User management table (demo data)
- [ ] **NOT STARTED** — System statistics (demo)
- [ ] **NOT STARTED** — Settings panel

---

## PHASE 11: Reports/Summary

> ✅ **COMPLETED** — `/dashboard/reports` with 3 templates
- [ ] **NOT STARTED** — Generate simple HTML report
- [ ] **NOT STARTED** — Print-friendly layout

---

## PHASE 12: Final Polish

> ⏳ **NOT STARTED**

- [ ] **NOT STARTED** — Remove/hide AI/ML sections (assistant, predictions)
- [ ] **NOT STARTED** — Update all badges to DEMO/ESTIMATE
- [ ] **NOT STARTED** — Responsive design testing
- [ ] **NOT STARTED** — Navigation flow testing

---

## REMOVED FEATURES (Out of Scope)

- ❌ AI Climate Assistant (`/dashboard/assistant`)
- ❌ ML Predictions (`/dashboard/predictions`)
- ❌ Real-time climate APIs
- ❌ Gamification system
- ❌ Complex notifications
- ❌ Real database (using localStorage/static data)
- ❌ External ML services

---

## Immediate next actions

1. ✅ **COMPLETED** — Fix TypeScript/lint errors
2. ✅ **COMPLETED** — Remove Prisma dependency
3. 🔄 **IN PROGRESS** — Build Climate Calculator with static emission factors
4. ⏳ **NEXT** — Build Results page
5. ⏳ **THEN** — Build Analytics with charts
6. ⏳ **THEN** — Build Goals, Recommendations, Progress, Risk, Org, Admin, Reports
7. ⏳ **FINALLY** — Remove AI/ML sections, final polish, testing
