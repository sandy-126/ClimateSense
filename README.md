# 🌍 ClimateSense
### AI-Powered Climate Impact, Risk & Action Management Platform

> **UN SDG 13 – Climate Action** | Major College Project

---

## 📌 Problem Statement

Climate change is accelerating. Individuals and organizations struggle to:
- Measure their actual climate/environmental impact.
- Understand which activities contribute most to their footprint.
- Predict future impact trends.
- Access climate risk information for their location.
- Take structured, data-driven action toward sustainability goals.

## 🔴 Existing Problems

- Most carbon calculators are overly simplistic, with no historical analysis.
- Existing tools provide no personalized AI-driven recommendations.
- No unified platform exists for measuring → understanding → predicting → acting → tracking.
- Climate risk information is scattered across multiple sources.
- Organizations lack tools to manage collective climate goals.

## ✅ Proposed Solution

**ClimateSense** is a full-stack, AI-powered web platform that guides users through a complete climate action journey:

```
MEASURE → UNDERSTAND → PREDICT → ACT → TRACK → IMPROVE
```

---

## 🎯 Objectives

1. Provide a structured, multi-step climate impact calculator.
2. Deliver AI-powered analysis, explanations, and recommendations.
3. Predict future climate impact using Machine Learning.
4. Display location-based climate risk on an interactive map.
5. Enable users to set goals, create action plans, and track progress.
6. Support organizations with role-based dashboards and analytics.
7. Generate professional PDF climate reports.
8. Provide a conversational AI Climate Assistant.
9. Support role-based access: Individual, Org Member, Org Admin, System Admin.

---

## 🧩 Features

| Module | Description |
|--------|-------------|
| 🌡️ Climate Calculator | Multi-step footprint estimator (transport, energy, other) |
| 📊 Analytics Dashboard | Historical trends, category breakdown, charts |
| 🤖 AI Analysis | Personalized explanations and recommendations |
| 🔮 ML Predictions | Regression/time-series footprint forecasting |
| 🗺️ Climate Risk Map | Interactive Leaflet map with risk indicators |
| 🎯 Goals & Plans | Goal creation, action plans, progress tracking |
| 💬 AI Assistant | ClimateSense AI chatbot with context awareness |
| 🏢 Organization Module | Multi-user orgs with admin controls |
| 👑 Admin Dashboard | Platform-wide management, audit logs |
| 📄 Reports | Professional PDF report generation |
| 🔔 Notifications | Goal reminders, risk updates, system alerts |
| 🏆 Gamification | Climate points, badges, achievements |

---

## 🏗️ Architecture

```
User Browser
     ↓
Next.js Frontend (TypeScript + Tailwind CSS + shadcn/ui)
     ↓
Next.js API Routes (Backend)
     ↓
Supabase PostgreSQL (Database + Auth + Storage)
     ↓
     ├── AI Service (LLM API via secure backend)
     │       └── Recommendations / Assistant / Analysis
     └── ML Service (FastAPI + Python)
             └── Predictions / Trend Analysis

External Climate Data APIs
     └── Climate Risk Module
```

---

## 🛠️ Technology Stack

### Frontend
- **Framework**: Next.js 14+ (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **UI Components**: shadcn/ui
- **Charts**: Recharts
- **Maps**: Leaflet + OpenStreetMap
- **State**: React hooks + Context API

### Backend
- **API**: Next.js API Routes (Route Handlers)
- **ORM**: Prisma
- **Validation**: Zod

### Database & Auth
- **Database**: Supabase PostgreSQL
- **Auth**: Supabase Auth
- **Storage**: Supabase Storage

### AI/ML
- **AI**: Google Gemini API (via secure backend)
- **ML Framework**: Python + scikit-learn + pandas + numpy
- **ML API**: FastAPI

### DevOps
- **Version Control**: Git + GitHub
- **Web Deployment**: Vercel
- **DB/Auth**: Supabase
- **ML Deployment**: Render / Railway

---

## 📁 Project Structure

```
climatesense/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── (auth)/             # Auth pages (login, register, etc.)
│   │   ├── (dashboard)/        # Protected dashboard pages
│   │   ├── (public)/           # Public pages (landing, about)
│   │   ├── api/                # API route handlers
│   │   └── layout.tsx
│   ├── components/
│   │   ├── ui/                 # shadcn/ui base components
│   │   ├── layout/             # Layout components (nav, sidebar, footer)
│   │   ├── dashboard/          # Dashboard-specific components
│   │   ├── calculator/         # Climate calculator components
│   │   ├── analytics/          # Chart/analytics components
│   │   ├── goals/              # Goals & action plan components
│   │   ├── map/                # Leaflet map components
│   │   ├── ai/                 # AI assistant components
│   │   └── shared/             # Reusable shared components
│   ├── lib/
│   │   ├── supabase/           # Supabase client utilities
│   │   ├── prisma/             # Prisma client
│   │   ├── ai/                 # AI service utilities
│   │   ├── ml/                 # ML API client
│   │   └── utils/              # General utilities
│   ├── hooks/                  # Custom React hooks
│   ├── services/               # Business logic services
│   ├── types/                  # TypeScript type definitions
│   ├── schemas/                # Zod validation schemas
│   └── styles/                 # Global styles
├── prisma/
│   ├── schema.prisma           # Database schema
│   └── seed.ts                 # Database seed data
├── ml-service/                 # Python FastAPI ML service
│   ├── main.py
│   ├── models/
│   ├── services/
│   └── requirements.txt
├── public/                     # Static assets
├── docs/                       # Documentation
│   ├── architecture.md
│   ├── requirements.md
│   ├── progress.md
│   └── tasks.md
└── .env.local                  # Environment variables (never commit)
```

---

## 🔐 User Roles

| Role | Description |
|------|-------------|
| **Individual User** | Full personal climate management |
| **Organization Member** | Participates in org goals, submits data |
| **Organization Admin** | Manages org, members, goals, reports |
| **System Admin** | Platform-wide administration |

---

## ⚙️ Environment Variables

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Database
DATABASE_URL=

# AI
GEMINI_API_KEY=

# Auth
NEXTAUTH_SECRET=
NEXTAUTH_URL=

# ML Service
ML_SERVICE_URL=
```

---

## 🚀 Installation & Running Locally

### Prerequisites
- Node.js 18+
- Python 3.10+
- Git

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/climatesense.git
cd climatesense
```

### 2. Install dependencies
```bash
npm install
```

### 3. Configure environment variables
```bash
cp .env.example .env.local
# Edit .env.local with your values
```

### 4. Set up the database
```bash
npx prisma generate
npx prisma db push
npx prisma db seed
```

### 5. Run the development server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### 6. Run the ML service (separate terminal)
```bash
cd ml-service
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

---

## 🧪 Testing
```bash
npm run test
npm run test:e2e
```

---

## 📦 Deployment

- **Frontend + API**: Vercel (`vercel deploy`)
- **Database + Auth**: Supabase (managed)
- **ML Service**: Render / Railway

---

## 🌐 SDG 13 Connection

ClimateSense directly supports **UN Sustainable Development Goal 13 – Climate Action**:

- **13.1** – Strengthen resilience through climate risk information
- **13.2** – Integrate climate measures into personal and organizational planning
- **13.3** – Build knowledge through AI-powered education and recommendations

---

## 🎓 College Project Information

- **Domain**: Environmental Technology / AI/ML / Web Development
- **SDG**: UN SDG 13 – Climate Action
- **Type**: Full-Stack Web Application with AI/ML Integration

---

## 📄 License

MIT License – For educational and non-commercial use.
