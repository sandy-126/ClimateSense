# ClimateSense – System Architecture Document

## 1. High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT BROWSER                          │
│                                                                 │
│   Next.js Frontend (React, TypeScript, Tailwind, shadcn/ui)    │
│                                                                 │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐   │
│   │  Public     │  │  Auth       │  │  Protected          │   │
│   │  Pages      │  │  Pages      │  │  Dashboard Pages    │   │
│   │  (Landing)  │  │  (Login/    │  │  (Individual/Org/   │   │
│   │             │  │   Register) │  │   Admin)            │   │
│   └─────────────┘  └─────────────┘  └─────────────────────┘   │
└─────────────────────────────┬───────────────────────────────────┘
                              │ HTTPS
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    NEXT.JS API ROUTES                           │
│                    (Backend / BFF Layer)                        │
│                                                                 │
│  /api/auth/...         Authentication endpoints                 │
│  /api/users/...        User management                          │
│  /api/calculator/...   Climate calculator                       │
│  /api/analytics/...    Analytics data                           │
│  /api/goals/...        Goals & action plans                     │
│  /api/ai/...           AI analysis & assistant                  │
│  /api/predictions/...  ML prediction proxy                      │
│  /api/risk/...         Climate risk data                        │
│  /api/reports/...      Report generation                        │
│  /api/admin/...        Admin management                         │
│  /api/notifications/.. Notifications                            │
│  /api/organizations/.. Organization management                  │
└──────────────────────────────┬──────────────────────────────────┘
                               │
              ┌────────────────┼─────────────────┐
              │                │                 │
              ▼                ▼                 ▼
┌─────────────────┐  ┌────────────────┐  ┌──────────────────┐
│    SUPABASE     │  │   AI SERVICE   │  │   ML SERVICE     │
│                 │  │                │  │                  │
│  PostgreSQL DB  │  │  Google Gemini │  │  FastAPI         │
│  Supabase Auth  │  │  (via backend) │  │  Python          │
│  Storage        │  │                │  │  scikit-learn    │
│  Row Level Sec  │  │  Analysis      │  │  pandas/numpy    │
│                 │  │  Recommend.    │  │                  │
│                 │  │  AI Assistant  │  │  Predictions     │
└─────────────────┘  └────────────────┘  └──────────────────┘
```

---

## 2. Frontend Architecture

### 2.1 Next.js App Router Structure

```
src/app/
├── (public)/                 # No auth required
│   ├── page.tsx              # Landing page (/)
│   ├── about/page.tsx        # About page
│   └── layout.tsx
│
├── (auth)/                   # Auth pages, redirect if logged in
│   ├── login/page.tsx
│   ├── register/page.tsx
│   ├── forgot-password/page.tsx
│   ├── reset-password/page.tsx
│   └── layout.tsx
│
├── (dashboard)/              # Protected, requires auth
│   ├── dashboard/page.tsx    # Individual dashboard
│   ├── calculator/page.tsx   # Climate calculator
│   ├── analytics/page.tsx    # Analytics & charts
│   ├── predictions/page.tsx  # ML predictions
│   ├── risk/page.tsx         # Climate risk map
│   ├── goals/page.tsx        # Goals management
│   ├── goals/[id]/page.tsx   # Goal detail
│   ├── actions/page.tsx      # Action plans
│   ├── assistant/page.tsx    # AI Climate Assistant
│   ├── reports/page.tsx      # Reports
│   ├── profile/page.tsx      # User profile
│   ├── settings/page.tsx     # Settings
│   └── layout.tsx            # Dashboard layout (sidebar + topnav)
│
├── (org)/                    # Organization pages
│   ├── org/[id]/
│   │   ├── dashboard/page.tsx
│   │   ├── members/page.tsx
│   │   ├── goals/page.tsx
│   │   ├── analytics/page.tsx
│   │   └── reports/page.tsx
│   └── layout.tsx
│
├── (admin)/                  # System admin pages
│   ├── admin/
│   │   ├── dashboard/page.tsx
│   │   ├── users/page.tsx
│   │   ├── organizations/page.tsx
│   │   ├── emission-factors/page.tsx
│   │   ├── locations/page.tsx
│   │   ├── risk-data/page.tsx
│   │   ├── reports/page.tsx
│   │   ├── analytics/page.tsx
│   │   ├── audit-logs/page.tsx
│   │   └── settings/page.tsx
│   └── layout.tsx
│
└── api/                      # API routes
```

### 2.2 Component Architecture

```
src/components/
├── ui/                       # shadcn/ui primitives
├── layout/
│   ├── Navbar.tsx            # Public top navigation
│   ├── Sidebar.tsx           # Dashboard sidebar
│   ├── TopBar.tsx            # Dashboard top bar
│   ├── MobileNav.tsx         # Mobile navigation drawer
│   ├── Footer.tsx            # Public footer
│   └── DashboardLayout.tsx   # Dashboard wrapper
├── dashboard/
│   ├── ClimateScoreCard.tsx
│   ├── FootprintCard.tsx
│   ├── ContributorsCard.tsx
│   ├── TrendChart.tsx
│   ├── PredictionCard.tsx
│   ├── GoalProgressCard.tsx
│   ├── RecommendationCard.tsx
│   └── QuickActionsCard.tsx
├── calculator/
│   ├── CalculatorStepper.tsx
│   ├── TransportStep.tsx
│   ├── EnergyStep.tsx
│   ├── OtherStep.tsx
│   └── ResultsPanel.tsx
├── analytics/
│   ├── TrendLineChart.tsx
│   ├── CategoryDonutChart.tsx
│   ├── HistoricalBarChart.tsx
│   ├── AreaChart.tsx
│   └── FilterBar.tsx
├── goals/
│   ├── GoalCard.tsx
│   ├── GoalForm.tsx
│   ├── GoalProgressBar.tsx
│   └── ActionItemList.tsx
├── map/
│   ├── ClimateMap.tsx
│   ├── RiskMarker.tsx
│   ├── RiskPopup.tsx
│   └── MapLegend.tsx
├── ai/
│   ├── ChatWindow.tsx
│   ├── ChatMessage.tsx
│   ├── ChatInput.tsx
│   └── RecommendationPanel.tsx
└── shared/
    ├── DemoDataBadge.tsx     # "DEMO DATA" label
    ├── EstimateBadge.tsx     # "ESTIMATE" label
    ├── DataSourceTag.tsx     # Shows data source info
    ├── LoadingSpinner.tsx
    ├── EmptyState.tsx
    ├── ErrorState.tsx
    └── PageHeader.tsx
```

---

## 3. Backend Architecture (Next.js API Routes)

### 3.1 API Route Structure

```
src/app/api/
├── auth/
│   ├── session/route.ts
│   └── profile/route.ts
├── users/
│   ├── route.ts             # GET /api/users (admin)
│   └── [id]/route.ts        # GET/PUT/DELETE specific user
├── calculator/
│   └── route.ts             # POST /api/calculator (save assessment)
├── emission-factors/
│   └── route.ts             # GET /api/emission-factors
├── analytics/
│   └── route.ts             # GET /api/analytics?userId=...&period=...
├── predictions/
│   └── route.ts             # GET /api/predictions (proxy to ML service)
├── risk/
│   ├── route.ts             # GET /api/risk (list locations)
│   └── [locationId]/route.ts
├── goals/
│   ├── route.ts             # GET/POST /api/goals
│   └── [id]/route.ts        # GET/PUT/DELETE /api/goals/:id
├── actions/
│   ├── route.ts
│   └── [id]/route.ts
├── ai/
│   ├── analyze/route.ts     # POST - AI analysis
│   └── chat/route.ts        # POST - AI assistant chat
├── organizations/
│   ├── route.ts
│   └── [id]/
│       ├── route.ts
│       ├── members/route.ts
│       └── goals/route.ts
├── reports/
│   ├── route.ts
│   └── [id]/route.ts
├── notifications/
│   └── route.ts
└── admin/
    ├── users/route.ts
    ├── organizations/route.ts
    ├── emission-factors/route.ts
    ├── locations/route.ts
    ├── risk-data/route.ts
    ├── audit-logs/route.ts
    └── settings/route.ts
```

### 3.2 Middleware

```
src/middleware.ts
- Authentication check for protected routes
- Role-based route protection
- API request logging
```

---

## 4. Database Schema

### 4.1 Core Tables

```sql
-- Users (managed by Supabase Auth, extended by profiles)
users (Supabase auth.users)
  id, email, created_at, ...

profiles
  id, user_id (FK→auth.users), full_name, avatar_url,
  location_id (FK), role, bio, phone,
  notification_prefs (JSONB), privacy_settings (JSONB),
  climate_points, created_at, updated_at

roles
  id, name, description, created_at

user_roles
  id, user_id (FK), role_id (FK), created_at

-- Organizations
organizations
  id, name, slug, description, logo_url, type,
  location_id (FK), settings (JSONB), created_at, updated_at

organization_members
  id, org_id (FK), user_id (FK), role, permissions (JSONB),
  joined_at, status

-- Locations & Risk
locations
  id, name, country, region, city, coordinates (POINT),
  created_at, updated_at

climate_risks
  id, location_id (FK), risk_type, severity, value, unit,
  source, source_url, dataset_version, data_date,
  description, notes, is_demo, created_at, updated_at

-- Emission Factors
emission_factors
  id, category, sub_category, factor, unit, source,
  source_url, version, effective_date, notes,
  is_active, created_at, updated_at

-- Climate Activities & Assessments
climate_assessments
  id, user_id (FK), org_id (FK nullable), period_start,
  period_end, total_co2e, status, notes, created_at

climate_activities
  id, assessment_id (FK), category, sub_category,
  emission_factor_id (FK), quantity, unit, co2e_value,
  calculation_details (JSONB), created_at

transportation_activities
  id, activity_id (FK), transport_type, distance_km,
  fuel_type, fuel_amount_liters, passengers, notes

energy_activities
  id, activity_id (FK), energy_type, consumption_kwh,
  renewable_percentage, provider, notes

-- Predictions
climate_predictions
  id, user_id (FK), org_id (FK nullable), prediction_date,
  predicted_co2e, model_version, confidence_interval,
  historical_data (JSONB), prediction_details (JSONB),
  created_at

-- Goals & Actions
climate_goals
  id, user_id (FK), org_id (FK nullable), name, description,
  category, target_value, target_unit, baseline_value,
  start_date, end_date, status, progress_percentage,
  created_at, updated_at

action_plans
  id, goal_id (FK), user_id (FK), org_id (FK nullable),
  name, description, created_at, updated_at

action_items
  id, plan_id (FK), title, description, status,
  due_date, completed_at, order_index, created_at, updated_at

progress_records
  id, goal_id (FK), recorded_value, recorded_at, notes, created_at

-- AI
recommendations
  id, user_id (FK), org_id (FK nullable), content,
  category, priority, status, source_assessment_id (FK),
  created_at, expires_at

ai_conversations
  id, user_id (FK), title, created_at, updated_at

ai_messages
  id, conversation_id (FK), role, content, metadata (JSONB),
  created_at

-- Notifications
notifications
  id, user_id (FK), type, title, message, is_read,
  action_url, metadata (JSONB), created_at

-- Reports
reports
  id, user_id (FK), org_id (FK nullable), type, title,
  status, file_url, metadata (JSONB), created_at

-- Audit
audit_logs
  id, user_id (FK nullable), action, entity_type,
  entity_id, old_value (JSONB), new_value (JSONB),
  ip_address, user_agent, created_at

-- Gamification
user_badges
  id, user_id (FK), badge_type, earned_at, metadata (JSONB)

action_streaks
  id, user_id (FK), current_streak, longest_streak,
  last_action_date, updated_at
```

---

## 5. ML Service Architecture

```
ml-service/
├── main.py                   # FastAPI app entry point
├── routers/
│   └── predictions.py        # /predict endpoint
├── models/
│   └── footprint_predictor.py # Model class
├── services/
│   └── prediction_service.py  # Business logic
├── schemas/
│   └── prediction.py          # Pydantic models
├── data/
│   └── model_artifacts/       # Saved model files
├── requirements.txt
└── Dockerfile
```

### ML Endpoints
- `POST /predict` – Predict future footprint from historical data
- `GET /health` – Health check
- `GET /model-info` – Model version and evaluation metrics

---

## 6. Security Architecture

### 6.1 Authentication Flow

```
1. User submits credentials (email + password)
2. Supabase Auth validates and issues JWT
3. JWT stored in httpOnly cookie (Next.js middleware)
4. Every API request includes JWT in Authorization header
5. API routes verify JWT with Supabase service role
6. Role checked against required permission for each route
```

### 6.2 Row Level Security (Supabase)
- Users can only read/write their own data.
- Org members can only read org data for their org.
- System admins bypass RLS via service role key (server-side only).

### 6.3 API Protection
- All API routes validate authentication.
- Input validated with Zod schemas.
- Rate limiting on auth and AI endpoints.
- CORS configured for production domain only.

---

## 7. Data Flow – Climate Calculator

```
User fills multi-step form
          ↓
Frontend validation (Zod)
          ↓
POST /api/calculator
          ↓
API validates user session
          ↓
Fetch current emission_factors from DB
          ↓
Calculate: quantity × emission_factor = CO2e
          ↓
Save climate_assessment + climate_activities to DB
          ↓
Return breakdown: total, by category, sources, factor version
          ↓
Frontend displays clearly labeled ESTIMATE with source info
```

---

## 8. Data Flow – AI Analysis

```
User requests analysis
          ↓
GET /api/ai/analyze
          ↓
Server fetches user's recent assessments from DB
          ↓
Constructs prompt with context (no raw PII in prompt)
          ↓
Calls AI API (Google Gemini) server-side only
          ↓
Parses response, stores recommendation to DB
          ↓
Returns structured recommendation to frontend
          ↓
Frontend displays with "AI-Generated" badge
```

---

## 9. Deployment Architecture

```
PRODUCTION

Vercel (Edge Network)
    Next.js App
    - Static pages served from CDN
    - API routes on serverless functions
    - Environment variables in Vercel dashboard

Supabase (Managed)
    - PostgreSQL database
    - Auth service
    - Storage bucket
    - RLS policies

Render/Railway
    - FastAPI ML service
    - Docker container
    - Persistent model storage
```

---

## 10. Environment Configuration

```
Development:  .env.local
Production:   Vercel + Render environment variable dashboards

Never committed to version control:
  - Any API keys
  - Database URLs
  - Service role keys
  - Auth secrets
```
