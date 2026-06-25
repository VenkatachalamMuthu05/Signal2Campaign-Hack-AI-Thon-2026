# DISCOVERY.md — Signal2Campaign AI

**Team:** Code Titans
**Challenge Track:** Challenge 2: Signal to Campaign
**Project Name:** Signal2Campaign AI
**Tagline:** *From Signal to Revenue in 90 Seconds.*
**Submission Date:** 28-06-2026
**Phase:** Week 1 — Discovery & Design

**Team Captain:** Venkatachalam Muthu (vemuthu@deloitte.com)
**Team Members:**
- Rohith V — Full Stack Developer (rohv@deloitte.com)
- Munish Mani — Frontend Developer (mumani@deloitte.com)

**Repository:** https://github.com/VenkatachalamMuthu05/Signal2Campaign-Hack-AI-Thon-2026

---

## 1. Problem Framing

Modern marketing teams sit on a paradox: they have access to more real-time signals than ever — weather APIs, traffic data, search trends, social conversations, competitor moves, local events — yet most campaign decisions are still made in weekly planning meetings, hours or days after the opportunity window has closed. By the time a Mumbai marketing manager realizes a sudden monsoon shower has spiked grocery-delivery intent by 300%, the demand surge is already over, and a competitor has already shipped the campaign.

**Target Users:**
Our primary user is the **Digital Marketing Manager at consumer brands** (quick-commerce, food-tech, e-commerce, OTT) — typically a 28–40 year old professional managing ₹5L–₹50L monthly ad budgets across Meta, Google, and push channels. They sit between brand strategy and performance marketing teams, are measured on CTR, conversion rate, and ROAS, and are under constant pressure to "react faster" without sacrificing brand voice or burning budget on poorly-timed campaigns.

**Secondary Users:** CMOs reviewing campaign approvals; Brand strategists validating tone; Growth analysts measuring ROI.

**Value Hypothesis (Testable):**
*"We believe that an AI-powered signal-to-campaign engine will reduce campaign launch time from 48 hours to under 5 minutes for digital marketing managers, increasing campaign relevance scores by 40% and capturing time-sensitive revenue opportunities currently lost to slow internal workflows."*

**Why this matters for Deloitte:** Deloitte Digital and our Marketing Transformation practice consistently advise CMOs on agility, personalization-at-scale, and AI-augmented marketing operations. Signal2Campaign AI is a tangible, demoable proof-of-concept of the "Autonomous Marketing" thesis we sell to enterprise clients.

### 🧠 How Team Code Titans Arrived at This Problem

Before locking this problem statement, our 3-person team evaluated three alternative framings during our kickoff call:

1. **AI chatbot for ad copy generation** — *Rejected by Munish.* Too crowded a category; every hackathon team builds this, and it doesn't show AI making decisions.
2. **AI influencer-matching engine** — *Rejected by Rohith.* Required scraped social data we couldn't legally source within 3 weeks, and added ToS risk.
3. **AI for real-time signal-to-campaign correlation** — ✅ **Selected by team consensus.** Aligns with Deloitte Digital's "Autonomous Marketing" thesis, demos in under 90 seconds, and shows AI making business decisions (not just generating text).

Venkatachalam (captain) pushed back on the first AI-generated suggestion ("just build a marketing chatbot") and re-anchored the team around the **decision-making AI** thesis instead of a **copywriting AI** thesis. This single reframing became our core differentiation.

---

## 2. MVP Scope

We are deliberately scoping a **narrow, deep, demoable** product over a broad shallow one. The hackathon rewards working solutions, not feature lists. With only 3 team members and ~8–10 hours/week each, ruthless prioritization is non-negotiable.

### ✅ In Scope (Must-Have for MVP)

- **Signal Dashboard:** Display 3–6 live or mock real-time signals (weather, search trends, traffic, local events) with type, severity, and timestamp.
- **Multi-Signal Correlation Engine:** AI analyzes signal combinations (not single signals) and surfaces ranked business opportunities with a relevance score (0–100).
- **AI Campaign Generator:** For a selected opportunity, generate a complete campaign kit — headline, CTA, target audience definition, channel recommendation, and reasoning.
- **Campaign Success Prediction:** Predicted CTR, conversion rate, estimated orders, and revenue ROI before approval.
- **Approval Workflow:** Marketer can edit, approve, or reject. Approved campaigns persist in a database with full audit trail.
- **Explainable AI Panel:** For every campaign, show *why* the AI made each choice (which signals weighted, by how much).

### ❌ Out of Scope (Explicitly Cut, With Reasoning)

- **Real ad-platform integrations (Meta/Google Ads API):** Out of scope because OAuth + ad-account approval cycles exceed our 3-week window and would steal engineering time from differentiation features. We will *mock* the "launch" action.
- **Image/video creative generation (DALL·E, Sora):** Out of scope due to API cost, inference latency hurting demo flow, and the risk of generated visuals embarrassing us on stage. We will show *creative briefs* instead of generated assets.
- **Multi-tenant authentication/SSO:** Out of scope because the demo is single-user; auth adds 2+ days of build with zero judging upside.
- **Mobile-native apps (iOS/Android):** Out of scope because a responsive web app demos perfectly on a projector and on judges' laptops.
- **Real competitor ad scraping:** Out of scope due to ToS/legal risk; we will use synthetic competitor signals.

### 🚀 Roadmap (If We Had More Time — R2/R3)

- **R2:** Real Meta/Google Ads API integration with one-click launch
- **R2:** Brand-voice training from uploaded historical campaigns
- **R3:** Autonomous mode (AI launches low-risk campaigns under rules)
- **R3:** Multi-tenant SaaS with workspaces and role-based access

---

## 3. MVP Backlog

12 user stories, prioritized by Must-Have (MH) / Should-Have (SH) / Won't-Have-This-Round (WH). Ownership assigned across our 3-person team to balance frontend (Munish), full-stack (Rohith), and architecture/AI (Venkatachalam).

### MH-1 — View Active Signals
**Story:** As a marketing manager, I want to see all active real-time signals on a dashboard, so that I can spot opportunities at a glance.
**Owner:** Munish (Frontend)
**Acceptance Criteria:**
- Dashboard loads in <2 seconds
- Shows minimum 3 signal types (weather, trend, traffic)
- Each signal card shows: type, title, location, timestamp, severity
**Test Approach:** Unit test for `/api/signals` returns valid Zod-validated shape; visual regression test for card layout.
**Priority:** Must-Have

### MH-2 — Multi-Signal Correlation
**Story:** As a marketing manager, I want the AI to combine multiple signals into a single opportunity, so that I see business outcomes, not raw data.
**Owner:** Venkatachalam (AI/Architecture)
**Acceptance Criteria:**
- AI accepts 2+ signals as input
- Returns a relevance score 0–100
- Returns plain-English reasoning (≥30 words)
**Test Approach:** Integration test calling Groq with 3 known signal combos; assert JSON schema and score range.
**Priority:** Must-Have

### MH-3 — Generate Campaign Kit
**Story:** As a marketing manager, I want the AI to auto-generate a complete campaign, so that I don't write copy from scratch.
**Owner:** Venkatachalam + Rohith
**Acceptance Criteria:**
- Output includes headline, CTA, audience, channel(s)
- Generation streams to UI (live text)
- Total time <4 seconds
**Test Approach:** Manual demo test across 3 scenarios; Zod validation on AI response shape.
**Priority:** Must-Have

### MH-4 — Predict Campaign Success
**Story:** As a marketing manager, I want predicted CTR / conversion / revenue before I approve, so that I can de-risk my decision.
**Owner:** Rohith (Full Stack)
**Acceptance Criteria:**
- Predicted metrics shown alongside generated campaign
- Confidence percentage visible
- ROI calculation shown
**Test Approach:** Snapshot test on prediction component; review numbers across 3 scenarios.
**Priority:** Must-Have

### MH-5 — Approve & Persist Campaign
**Story:** As a marketing manager, I want to approve a campaign and save it, so that there's an auditable record.
**Owner:** Rohith (Full Stack)
**Acceptance Criteria:**
- "Approve" button writes to Postgres
- Toast confirmation appears
- Campaign appears in History view
**Test Approach:** Integration test with test Supabase project; assert row inserted with all fields.
**Priority:** Must-Have

### MH-6 — View Campaign History
**Story:** As a marketing manager, I want to see all past campaigns, so that I have an audit trail.
**Owner:** Munish + Rohith
**Acceptance Criteria:**
- History page lists all approved campaigns
- Sortable by date
- Click-through to detail view
**Test Approach:** Knex query test on `campaigns` table; UI snapshot.
**Priority:** Must-Have

### SH-7 — Explainable AI Panel
**Story:** As a marketing manager, I want to see *why* the AI generated this campaign, so that I trust it.
**Owner:** Venkatachalam
**Acceptance Criteria:**
- Shows weighted factors (e.g., rain +35%, search +28%)
- Sits within the campaign view
**Test Approach:** Visual review across 3 scenarios.
**Priority:** Should-Have

### SH-8 — Edit Campaign Before Approval
**Story:** As a marketing manager, I want to edit AI-generated copy, so that I can tweak the brand voice.
**Owner:** Munish
**Acceptance Criteria:**
- All fields editable
- Validation prevents empty fields
- Edits saved on approval
**Test Approach:** Form input test; Zod client-side validation test.
**Priority:** Should-Have

### SH-9 — Hyperlocal Pulse Map
**Story:** As a marketing manager, I want a map of India showing live opportunities by city, so that I can target hyperlocally.
**Owner:** Munish
**Acceptance Criteria:**
- Map shows ≥5 cities
- Color-coded by urgency
- Hover reveals city signal summary
**Test Approach:** Visual review; manual interaction test.
**Priority:** Should-Have

### SH-10 — Anti-Campaign Detector
**Story:** As a marketing manager, I want the AI to block campaigns during crises (e.g., floods, tragedies), so that we don't damage the brand.
**Owner:** Venkatachalam
**Acceptance Criteria:**
- Negative-event signals flagged
- Generation blocked or rewritten with empathy
**Test Approach:** Test with synthetic crisis signal; assert generation is paused or rephrased.
**Priority:** Should-Have

### WH-11 — Voice Command Interface
**Story:** As a marketing manager, I want to speak commands to the AI, so that I can work hands-free.
**Acceptance Criteria:** Web Speech API integration; voice triggers campaign generation.
**Test Approach:** Manual demo test.
**Priority:** Won't-Have (stretch goal for Week 3 if time allows)

### WH-12 — PDF Export
**Story:** As a marketing manager, I want to export the campaign as PDF, so that I can share with stakeholders.
**Acceptance Criteria:** One-click export; styled PDF.
**Test Approach:** Manual file inspection.
**Priority:** Won't-Have (stretch goal)

---

## 4. High-Level Design

### Architecture Diagram

```mermaid
flowchart TB
    User[👤 Marketing Manager<br/>Browser]

    subgraph Frontend["🎨 Frontend - Vercel Edge"]
        NextUI[Next.js 14 App Router<br/>React 18 + TypeScript<br/>Tailwind CSS + shadcn/ui]
    end

    subgraph Backend["⚙️ Backend - Next.js API Routes Serverless"]
        SignalsAPI["/api/signals"]
        AnalyzeAPI["/api/analyze"]
        GenerateAPI["/api/generate"]
        CampaignsAPI["/api/campaigns"]
        Zod[Zod Validation Layer]
    end

    subgraph AI["🤖 AI Layer"]
        Groq[Groq Llama 3.1 70B<br/>Primary LLM]
        OpenAI[OpenAI gpt-4o-mini<br/>Fallback]
        VercelAI[Vercel AI SDK<br/>Streaming]
    end

    subgraph Data["📊 Data Sources"]
        MockJSON[Mock Signals JSON<br/>Week 2]
        Weather[OpenWeather API<br/>Week 3]
        Trends[Google Trends<br/>Week 3]
    end

    subgraph DB["🗄️ Persistence"]
        Supabase[(Supabase PostgreSQL)]
        Knex[Knex.js Query Builder]
    end

    User --> NextUI
    NextUI -->|HTTPS| SignalsAPI
    NextUI -->|HTTPS| AnalyzeAPI
    NextUI -->|HTTPS| GenerateAPI
    NextUI -->|HTTPS| CampaignsAPI

    SignalsAPI --> Zod
    AnalyzeAPI --> Zod
    GenerateAPI --> Zod
    CampaignsAPI --> Zod

    SignalsAPI --> MockJSON
    SignalsAPI --> Weather
    SignalsAPI --> Trends

    AnalyzeAPI --> Groq
    GenerateAPI --> Groq
    GenerateAPI --> VercelAI
    Groq -.fallback.-> OpenAI

    CampaignsAPI --> Knex
    Knex --> Supabase
