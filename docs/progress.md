# ClimateSense – Progress

**Last verified:** 2026-09-27 (inspection + lint fix; dev runtime check attempted)

---

## COMPLETED

- **Project documentation** — Root `README.md`, `docs/requirements.md`, `docs/architecture.md`, `docs/tasks.md`
- **Next.js app shell** — `climatesense-app/` with App Router, TypeScript, Tailwind CSS v4, Inter via `next/font`
- **Design system** — CSS variables, gradients, `.badge-demo`, dark/light tokens in `globals.css`
- **Landing page (`/`)** — All marketing sections: Hero, What Is, Why Climate, How It Works, Features, AI & ML, Climate Risk, Dashboard preview, Goals, SDG 13, CTA, Navbar, Footer
- **Landing UX** — In-page anchor navigation, mobile menu, dark/light toggle (client `dark` class on `<html>`), DEMO labels on mock previews
- **Auth route shells** — `/login` and `/register` (branded layout, back-to-home link)
- **404 page** — Custom `not-found.tsx`
- **SEO metadata** — Title/description on root layout and auth pages
- **Lint** — `npm run lint` passes (auth `Link` usage, escaped entities in landing copy)
- **CSS dev blocker (source)** — Removed duplicate Google Fonts `@import` from `globals.css` (Inter from layout only)
- **Production build** — Previously verified `npm run build` succeeds (routes: `/`, `/login`, `/register`, `/_not-found`)

---

## IN PROGRESS

- **Foundation stabilization** — Source is fixed for dev CSS; **running dev server may still be stale** (see BROKEN)
- **shadcn/ui** — Radix packages in `package.json`; no `components/ui/` or `components.json`
- **Theming** — `next-themes` installed but not used (manual toggle on landing only)
- **Accessibility** — Partial ARIA on nav/sections; no full WCAG pass
- **Next.js 16 metadata** — `viewport` / `themeColor` still on `metadata` export (build/dev warnings)

---

## BROKEN

- **Local dev server (runtime)** — Process on **port 3000** (PID 21044) did not respond to HTTP within 15–60s during this inspection; earlier dev logs showed CSS parse errors **before** the `globals.css` fix. A **single dev restart** is likely required to confirm pages in the browser (not performed per “do not restart” instruction).
- **Second `npm run dev`** — Exited immediately: “Another next dev server is already running.”

---

## NOT STARTED

- **Git repository** — No `.git` in workspace
- **Supabase / database** — No client, no `DATABASE_URL` configured (placeholders in `.env.local`)
- **Prisma** — No schema or migrations
- **Authentication (functional)** — No forms, session, logout, password reset, middleware
- **RBAC / roles** — Not implemented
- **User profiles** — Not implemented
- **Dashboard (`/dashboard`)** — No route; landing shows **mock** preview only
- **Calculator, analytics, goals, risk map, assistant, org, admin** — Not implemented
- **API routes** — No `src/app/api/`
- **AI (Gemini) / ML service** — Not implemented; no `ml-service/`
- **Recharts / Leaflet** — Dependencies only; unused in `src/`
- **Zod validation, tests, rate limiting, notifications, reports, gamification** — Not started
- **framer-motion** — In `package.json`; not used in `src/`

---

## Routes (actual)

| Route | Type | Notes |
|-------|------|--------|
| `/` | Static | Full landing page |
| `/login` | Static | Phase 2 placeholder |
| `/register` | Static | Phase 2 placeholder |
| `/dashboard` | — | **404** (no page) |
| Unknown paths | — | Custom 404 |

---

## Runtime check summary (this session)

| Check | Result |
|-------|--------|
| `npm run lint` | Pass |
| `npm run dev` | Already running on :3000; new instance blocked |
| HTTP `localhost:3000/*` | **Timeout** (could not visually verify in browser) |
| Terminal dev log | Old CSS errors; later “Compiled” + `/` metadata warnings after fix |

---

## Data labeling (landing)

Mock dashboard, AI chat, ML chart, and climate risk content are labeled **DEMO / DEMO DATA** — not connected to backend.
