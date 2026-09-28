# ClimateSense – Requirements Document

## 1. Functional Requirements

### 1.1 Authentication & Authorization
- FR-AUTH-01: Users can register with email and password.
- FR-AUTH-02: Users can log in with email and password.
- FR-AUTH-03: Users can log out.
- FR-AUTH-04: Forgot password and password reset via email.
- FR-AUTH-05: Session management with JWT/cookies.
- FR-AUTH-06: Protected routes – unauthenticated users are redirected to login.
- FR-AUTH-07: Role-based authorization (Individual, Org Member, Org Admin, System Admin).
- FR-AUTH-08: System Admin account is not created through public registration.
- FR-AUTH-09: Both frontend routes and backend API endpoints are protected.

### 1.2 Individual User
- FR-USER-01: Manage personal profile (name, email, avatar, location, preferences).
- FR-USER-02: Enter climate activity data (transport, energy, other).
- FR-USER-03: Calculate estimated carbon footprint.
- FR-USER-04: View personalized dashboard.
- FR-USER-05: View historical trend charts.
- FR-USER-06: View ML-powered future predictions.
- FR-USER-07: View climate risk information for a selected location.
- FR-USER-08: Receive personalized AI recommendations.
- FR-USER-09: Create and manage climate goals.
- FR-USER-10: Create and manage action plans.
- FR-USER-11: Track goal progress.
- FR-USER-12: Use AI Climate Assistant (chatbot).
- FR-USER-13: Generate personal climate reports.
- FR-USER-14: Manage notifications and preferences.
- FR-USER-15: Toggle dark/light mode.

### 1.3 Organization Member
- FR-ORGM-01: Login and manage permitted profile information.
- FR-ORGM-02: Submit permitted activity data.
- FR-ORGM-03: View permitted organization information.
- FR-ORGM-04: Participate in organization goals.
- FR-ORGM-05: Complete assigned action items.

### 1.4 Organization Admin
- FR-ORGA-01: Manage organization profile.
- FR-ORGA-02: Add/remove organization members.
- FR-ORGA-03: Assign organization roles.
- FR-ORGA-04: View organization analytics.
- FR-ORGA-05: Manage organization climate goals.
- FR-ORGA-06: Create organization action plans.
- FR-ORGA-07: Generate organization reports.

### 1.5 System Admin
- FR-ADMIN-01: Manage all users.
- FR-ADMIN-02: Manage all organizations.
- FR-ADMIN-03: Manage climate activity categories.
- FR-ADMIN-04: Manage emission factors (with source, version, notes).
- FR-ADMIN-05: Manage locations and risk data.
- FR-ADMIN-06: View platform analytics.
- FR-ADMIN-07: View all reports.
- FR-ADMIN-08: View audit logs.
- FR-ADMIN-09: Manage system settings and permissions.

### 1.6 Climate Calculator
- FR-CALC-01: Multi-step form (Transport → Energy → Other categories).
- FR-CALC-02: Use versioned emission factors from database (not hardcoded values).
- FR-CALC-03: Show category breakdown, total, units, sources.
- FR-CALC-04: Clearly label results as ESTIMATES.
- FR-CALC-05: Save assessments to database.

### 1.7 Analytics
- FR-ANAL-01: Display monthly trends (line chart).
- FR-ANAL-02: Display category breakdown (donut chart).
- FR-ANAL-03: Display historical comparison (bar chart).
- FR-ANAL-04: Support time filters: 30d, 3m, 6m, 1y, custom.
- FR-ANAL-05: Use real database data (not hardcoded).

### 1.8 AI Analysis
- FR-AI-01: Analyze user data and provide plain-language explanation.
- FR-AI-02: Identify main contributors and suggested improvements.
- FR-AI-03: Provide personalized recommendations.
- FR-AI-04: Suggest goals and actions.
- FR-AI-05: Never expose AI API key to the frontend.
- FR-AI-06: DEMO MODE if no API key is configured.

### 1.9 ML Predictions
- FR-ML-01: Train on historical activity data.
- FR-ML-02: Predict future footprint (regression/time-series).
- FR-ML-03: Display historical + predicted values on chart.
- FR-ML-04: Show trend direction and model information.
- FR-ML-05: Clearly label results as estimates/predictions.

### 1.10 Climate Risk Module
- FR-RISK-01: Users select a location.
- FR-RISK-02: Display risk indicators (heat, flood, drought, coastal, etc.).
- FR-RISK-03: Interactive Leaflet map with color-coded markers.
- FR-RISK-04: Clicking location shows detailed risk info.
- FR-RISK-05: Show data source, date, version for every dataset.
- FR-RISK-06: Use DEMO DATA until reliable external data is available.

### 1.11 Goals & Action Plans
- FR-GOAL-01: Create/edit/delete goals with name, category, target, dates, status.
- FR-GOAL-02: Track progress toward goals.
- FR-GOAL-03: Create action plans linked to goals.
- FR-GOAL-04: Mark actions complete/skipped/in-progress.
- FR-GOAL-05: Goal statuses: Not Started, Active, At Risk, Completed.

### 1.12 AI Climate Assistant
- FR-CHAT-01: Conversational chatbot called ClimateSense AI.
- FR-CHAT-02: Answers climate-related questions with context from user data.
- FR-CHAT-03: Store conversation history (AIConversation, AIMessage).
- FR-CHAT-04: Never expose API keys to the frontend.
- FR-CHAT-05: DEMO MODE with clear indicator if no key configured.

### 1.13 Reports
- FR-RPT-01: Generate professional PDF reports.
- FR-RPT-02: Individual report: profile, assessment, footprint, trends, goals, recommendations.
- FR-RPT-03: Organization report: org info, impact, trends, goals, progress, recommendations.

### 1.14 Notifications
- FR-NOTIF-01: Goal reminders, report ready, risk updates, action reminders.
- FR-NOTIF-02: Users can manage notification preferences.
- FR-NOTIF-03: Notification center in top navigation.

### 1.15 Gamification
- FR-GAME-01: Climate points system.
- FR-GAME-02: Badges and achievements.
- FR-GAME-03: Action streak tracking.
- FR-GAME-04: No misleading environmental impact claims.

---

## 2. Non-Functional Requirements

### 2.1 Performance
- NFR-PERF-01: Pages load within 3 seconds on standard connection.
- NFR-PERF-02: API responses within 1 second for standard queries.
- NFR-PERF-03: ML predictions within 5 seconds.

### 2.2 Security
- NFR-SEC-01: All secrets stored in environment variables.
- NFR-SEC-02: Input validation on all forms (Zod).
- NFR-SEC-03: SQL injection protection via Prisma ORM.
- NFR-SEC-04: XSS protection.
- NFR-SEC-05: CORS configuration.
- NFR-SEC-06: API rate limiting.
- NFR-SEC-07: Audit logging for sensitive operations.
- NFR-SEC-08: Strict organization-level data isolation.

### 2.3 Accessibility
- NFR-ACC-01: Keyboard navigable.
- NFR-ACC-02: Screen-reader-friendly labels and ARIA attributes.
- NFR-ACC-03: Good color contrast (WCAG 2.1 AA).
- NFR-ACC-04: Visible focus states.
- NFR-ACC-05: Semantic HTML5.
- NFR-ACC-06: Alt text on all images.
- NFR-ACC-07: Reduced motion support.

### 2.4 Responsiveness
- NFR-RESP-01: Fully responsive on desktop, laptop, tablet, mobile.
- NFR-RESP-02: Sidebar becomes mobile navigation on small screens.
- NFR-RESP-03: Charts and tables usable on small screens.

### 2.5 Reliability
- NFR-REL-01: Graceful error handling on every page.
- NFR-REL-02: No raw stack traces displayed to users.
- NFR-REL-03: Loading and empty state handling.

### 2.6 Scientific Integrity
- NFR-SCI-01: Never invent emission factors, risk scores, or climate statistics.
- NFR-SCI-02: All demo data clearly labeled as DEMO/SAMPLE.
- NFR-SCI-03: Sources, versions, methodology visible for all data.
- NFR-SCI-04: Calculator results clearly labeled as ESTIMATES.
- NFR-SCI-05: Predictions clearly labeled as ESTIMATES, not guarantees.

---

## 3. Data Requirements

### 3.1 Emission Factors
- DR-EF-01: Stored in database with category, factor, unit, source, source URL, version, date, notes.
- DR-EF-02: Based on credible publicly available sources (IPCC, EPA, DEFRA, IEA, etc.).
- DR-EF-03: Admin-manageable.

### 3.2 Climate Risk Data
- DR-RISK-01: Initially populated with clearly labeled DEMO DATA.
- DR-RISK-02: Structured to accept replacement with real public datasets later.
- DR-RISK-03: Every data point has source, date, version, description, unit.

### 3.3 Database
- DR-DB-01: Proper relational schema with foreign keys, indexes, timestamps, constraints.
- DR-DB-02: Audit log table for sensitive operations.
- DR-DB-03: Soft delete where appropriate.

---

## 4. Deployment Requirements
- DEPL-01: Web app deployable to Vercel.
- DEPL-02: Database on Supabase.
- DEPL-03: ML service deployable to Render/Railway.
- DEPL-04: Separate .env.example with all required variable names (no values).
- DEPL-05: Build passes without errors.
