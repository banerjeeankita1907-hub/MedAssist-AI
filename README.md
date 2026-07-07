# MedAssist AI — Voice-First Health Triage Assistant


## Project Title
**MedAssist AI — Voice-First AI Triage for the Last Mile of Healthcare**

## Problem Statement
In rural and low-connectivity regions, one doctor often serves thousands of people. Patients travel hours for basic triage advice, low-literacy users struggle with English-only tools, and community health workers (ASHA/ANM-type roles) lack a fast decision-support tool. The result: delayed care, unnecessary clinic overcrowding, and preventable emergencies that go unrecognized until too late.

## Proposed Solution
MedAssist AI is a multilingual, voice-first symptom triage assistant. A patient (or a health worker on their behalf) describes a symptom in plain language or speech. An adaptive questioning engine asks 1–3 targeted follow-up questions, applies a **safety-first escalation rule** (the system can only raise urgency, never lower it, when a red-flag symptom is detected), and returns one of three plain-language outcomes:
- 🟢 Manageable at home, with monitoring guidance
- 🟠 Visit a clinic soon
- 🔴 Seek emergency care immediately

A companion **worker dashboard** gives community health workers a live view of triage volume, flagged emergencies, and top reported symptoms in their coverage area — the data layer that turns this from a chatbot into a public-health tool.

## Technology Stack
| Layer | This prototype | Production-scale plan |
|---|---|---|
| Frontend | Single-file responsive HTML/CSS/JS (no build step, opens directly in any browser) | React + Tailwind, packaged as an installable PWA |
| AI / reasoning | Deterministic adaptive-questioning engine with red-flag keyword detection (transparent, auditable logic — see `index.html`) | LLM-assisted symptom reasoning (e.g. Claude API) layered *behind* the same hard-coded safety rules, for richer free-text understanding |
| Voice input | Browser-native Web Speech API (real, working — try the mic button in Chrome) | Whisper-based STT for regional-language accuracy on low-end phones |
| Data viz | Chart.js (CDN) | Same, fed by a real Postgres-backed event store |
| Backend (planned) | — | Node.js/Express REST API, PostgreSQL for session logs, Redis cache |
| Deployment (planned) | — | Docker containers on AWS/GCP; offline-first via service workers for 2G areas |

## What Actually Works Right Now (not a mockup)
- Full chat-based triage flow with branching logic across 4 symptom categories
- Free-text symptom detection (typing "my father has a fever and cough" routes correctly)
- Red-flag safety escalation, both from guided choices and free text
- Real voice input via the Web Speech API (works in Chrome/Edge)
- Language switcher (English / Hindi / Bengali greeting + placeholder text — structure ready for full i18n)
- Live dashboard: KPIs, a 7-day trend line chart, a top-symptoms bar chart, and a session log table — all driven from the actual sessions you run in the demo

## How to Run
No installation needed:
1. Open `index.html` in any modern browser (Chrome recommended for voice input).
2. Click **Try Triage** and walk through a symptom scenario.
3. Click **Worker Dashboard** to see your session reflected in the charts and log.

## Startup Innovation Angle
- **Free for patients** — removes the biggest adoption barrier in underserved communities.
- **Revenue from B2G/B2B**: subscription dashboards for clinics, NGOs, and state health departments; anonymized, aggregated symptom-trend data licensed for public-health early-warning (e.g. flu/dengue clustering).
- **Distribution**: partner with existing community health worker networks rather than requiring app-store discovery — works as a shared link/PWA on the phone they already carry.

## Evaluation Criteria Mapping
- **Innovation**: safety-first "AI can escalate, never de-escalate" rule + voice-first design for low-literacy users.
- **Technical Approach**: clean separation of a deterministic safety layer from a future LLM reasoning layer — auditable by design, a real requirement for medical tools.
- **Problem Solving**: directly targets the access gap between symptom onset and specialist availability.
- **User Experience**: calm color language, large tap targets, multilingual, mobile-first responsive layout.
- **Presentation**: see the accompanying slide deck, `MedAssist_AI_Pitch_Deck.pptx`.
