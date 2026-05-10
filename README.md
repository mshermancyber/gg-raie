# GG-RAIE
### Generative Governance-Risk AI Engine

> A 2LoD AI governance risk assessment platform for financial services. Combines structured model intake with agentic AI reasoning to evaluate training data lineage, explainability, bias controls, regulatory alignment, and human oversight — producing risk-tiered findings, SR 11-7 challenge questions, and exportable PDF assessment packets.

---

## Overview

GG-RAIE simulates the workflow of a Second Line of Defense AI governance review. A risk analyst submits an AI/ML system for assessment — providing details on model purpose, training data, explainability methods, human oversight controls, and regulatory alignment — and GG-RAIE produces a structured risk opinion backed by agentic reasoning against applicable regulatory frameworks.

The platform is model-agnostic and backend-agnostic. It runs against a local llama.cpp instance for air-gapped or homelab environments and falls back to any OpenAI-compatible API endpoint via a single environment variable switch.

---

## Key Features

**Structured Model Intake**
A four-section governance questionnaire covering model identity, data governance, explainability and oversight, and regulatory and validation status. Pre-loaded with 10 mock scenarios spanning the full risk spectrum — from clean internal analytics models to unvalidated consumer credit decisioning systems with live regulatory exposure.

**Agentic 2LoD Review**
Paste any artifact — model card, architecture notes, control evidence, incident summary, or policy text — and the AI agent reasons through it step by step. Each reasoning step surfaces an observation, a risk inference, and a specific concern where applicable. Evidence present and missing are enumerated. Control concerns are assigned severity ratings with regulatory references.

**Risk Report**
Six-dimension risk assessment covering data governance, model explainability, bias and fairness, human oversight, regulatory alignment, and incident and drift monitoring. Each dimension is independently rated LOW / ELEVATED / HIGH / UNACCEPTABLE. Overall risk tier, escalation determination, 2LoD challenge questions, and recommended actions are produced in full.

**PDF Export**
Styled assessment packet exported directly from the browser via jsPDF. Dark-themed header with model name and overall risk tier badge, dimension grid, challenge questions, control concerns with severity coloring, and page-numbered footer. Formatted for senior stakeholder consumption.

**JSON Import / Export**
Save and reload any intake form as JSON for reuse across sessions. Export the full assessment packet — intake data, AI analysis, and agent review — as a single JSON for archival or re-presentation without re-running the model.

**Backend Indicator**
Live header badge shows which AI backend is active (local llama.cpp or API fallback) and the loaded model name.

---

## Regulatory Frameworks Applied

| Framework | Application |
|---|---|
| SR 11-7 | Model risk management — development, validation, ongoing monitoring |
| OCC 2011-12 | Model governance and controls |
| ECOA / Regulation B | Adverse action, disparate impact, fair lending |
| FCRA Section 615(a) | Adverse action notice requirements |
| CFPB Bulletin 2022-03 | Algorithmic fairness in consumer decisioning |
| FFIEC BSA/AML Examination Manual | AML model governance |
| NIST AI RMF 1.0 | GOVERN, MAP, MEASURE, MANAGE functions |
| Basel III / CECL | Credit risk and capital model requirements |
| NYC Local Law 144 | Bias audit requirements for automated employment decisions |
| SEC / FINRA Reg BI | Suitability and fiduciary obligations for investment models |

---

## Mock Scenarios

Ten pre-loaded scenarios are included covering different model types, business lines, and risk outcomes. Load any from the intake tab without typing a single field.

| # | Model | Business Line | Expected Tier |
|---|---|---|---|
| 01 | Digital Lending Decisioning Model v2.3 | Consumer Banking | UNACCEPTABLE |
| 02 | Fraud Detection Neural Network v4.1 | Payments | HIGH |
| 03 | AML Transaction Monitoring Model v7.0 | Financial Crimes | ELEVATED |
| 04 | Mortgage Underwriting Assistant v1.2 | Retail Banking | HIGH |
| 05 | Customer Churn Prediction Model v3.0 | Retail Analytics | LOW |
| 06 | Commercial Credit Risk Rating Model v5.2 | Commercial Banking | ELEVATED |
| 07 | Wealth Management Robo-Advisor v2.0 | Wealth Management | HIGH |
| 08 | HR Talent Screening Model v1.0 | Human Resources | UNACCEPTABLE |
| 09 | Liquidity Risk Forecasting Model v6.1 | Treasury | ELEVATED |
| 10 | Customer Service Chatbot NLP Model v3.5 | Digital Experience | LOW |

---

## Tech Stack

- **Frontend:** React 18 + Vite
- **AI Backend:** Local llama.cpp (OpenAI-compatible `/v1` endpoint) — tested against `Qwen3-35B-A3B Q4_K_M`
- **Fallback:** Any OpenAI-compatible API endpoint (Anthropic, OpenAI, etc.)
- **PDF Export:** jsPDF (browser-native, no server required)
- **Styling:** CSS custom properties, Space Mono + DM Sans

---

## Setup

```bash
git clone https://github.com/mshermancyber/gg-raie
cd gg-raie
npm install
cp .env.example .env
# Edit .env with your backend details
npm run dev
```

Open `http://localhost:5173`

---

## Environment Variables

```bash
# Local llama.cpp backend
LOCAL_AI_BASE_URL=http://YOUR_HOST:PORT/v1
LOCAL_AI_MODEL=your-model-filename.gguf

# Fallback (any OpenAI-compatible endpoint)
FALLBACK_AI_BASE_URL=https://api.anthropic.com/v1
FALLBACK_AI_MODEL=claude-sonnet-4-20250514
FALLBACK_AI_API_KEY=your_api_key_here

# Active backend: "local" or "fallback"
AI_BACKEND=local
```

The `.env` file is gitignored. Never commit API keys. Use `.env.example` as the template.

---

## Architecture

```
src/
├── components/
│   ├── IntakeForm.jsx       # Four-section governance questionnaire + mock picker + JSON import
│   ├── AgentReviewer.jsx    # Artifact paste → agentic reasoning trace + control concerns
│   ├── RiskReport.jsx       # Dimension grid + challenge questions + PDF/JSON export
│   └── BackendBadge.jsx     # Live backend/model indicator
├── lib/
│   ├── aiClient.js          # Backend-agnostic chat completion client (reads from .env)
│   ├── prompts.js           # All system and user prompts — intake analysis + agent reasoning
│   ├── exportPdf.js         # jsPDF report generation
│   └── mockScenarios.json   # 10 pre-loaded intake scenarios
└── App.jsx                  # Three-tab shell: Intake → Agentic Review → Risk Report
```

All AI configuration is injected at build time from `.env` via Vite's `define` block. No hardcoded endpoints, model names, or API keys anywhere in the source.

---

## Portfolio Context

Built to demonstrate Second Line of Defense technology and AI governance competencies including:

- SR 11-7 model risk management applied to AI/ML systems
- AI governance, ethical considerations, and explainability in risk management
- Agentic AI for automated risk investigation and monitoring
- 2LoD challenge function — control gap identification, escalation determination
- KPI/KRI production and senior stakeholder reporting
- Regulatory alignment across ECOA, FCRA, CFPB, NIST AI RMF, Basel III

---

## Author

**Mark Sherman** · Senior Cybersecurity & Risk Professional · 19 years Tier 1 financial services

[![LinkedIn](https://img.shields.io/badge/LinkedIn-mshermancyber-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/mshermancyber)
[![GitHub](https://img.shields.io/badge/GitHub-mshermancyber-181717?style=flat&logo=github)](https://github.com/mshermancyber)

---

*GG-RAIE is a portfolio and demonstration tool. Mock scenarios and sample outputs are fictional and do not represent any real institution, model, or assessment.*
