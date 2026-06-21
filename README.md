# Komplain.AI

AI-powered complaint resolution MVP for e-commerce support teams, built for UMHackathon 2026. Komplain.AI turns raw customer complaints into structured intake data, order-aware reasoning, optional visual evidence analysis, bilingual reply drafts, and an auditable multi-agent trace for human review.

## Why I Built This

Support teams often receive messy, emotional, mixed-language complaints with missing order context or unclear visual evidence. Komplain.AI explores how an AI-assisted workflow can help operators triage complaints faster without fully automating risky refund or reship decisions.

## Features

- Complaint intake for English, Bahasa Malaysia, and Manglish text.
- Optional order ID input and order lookup against local JSON demo data.
- Multi-agent pipeline: intake, context, optional vision, reasoning, response, and supervisor review.
- Optional JPG, PNG, or WebP evidence upload with a 5MB limit.
- Decision categories: `REFUND`, `RESHIP`, `CLARIFY`, `ESCALATE`, and `DISMISS`.
- English and Bahasa Malaysia reply drafts for operator review.
- Agent trace events with latency, token counts, execution mode, provider metadata, and fallback reason.
- Estimated cost calculation in Malaysian Ringgit.
- Static React dashboard with live case log, resolution card, edit/copy reply flow, and trace visualization.
- Postman collections and pytest coverage for backend, storage, agents, LLM behavior, and image-upload paths.

## Tech Stack

- **Backend:** Python, FastAPI, Uvicorn, Pydantic, HTTPX, python-dotenv
- **AI providers:** Z.ai / GLM primary provider, GLM vision model, Groq fallback
- **Frontend:** React 18 UMD, ReactDOM UMD, Babel Standalone, plain CSS
- **Storage:** JSON files in `data/`
- **Testing / quality:** pytest, Ruff, pip-audit, detect-secrets, GitHub Actions
- **API tooling:** Postman collections

## My Role / Contribution

This was built as a UMHackathon 2026 project. The exact individual contribution split is not visible from the code alone, so this section stays conservative:

- [TODO: clarify your exact ownership across backend, frontend, AI workflow, docs, pitch, and deployment]
- Visible project work includes FastAPI routes, agent orchestration, LLM provider/fallback logic, JSON-backed storage, frontend dashboard integration, tests, CI, and hackathon documentation.

## Project Structure

```text
Komplain.AI/
|-- app.py
|-- README.md
|-- README_BACKEND.md
|-- requirements.txt
|-- requirements-dev.txt
|-- postman_collection.json
|-- postman_qatd_collection.json
|-- backend/
|   |-- main.py
|   |-- agents.py
|   |-- llm.py
|   |-- models.py
|   `-- storage.py
|-- frontend/
|   |-- index.html
|   |-- app.jsx
|   |-- styles.css
|   `-- components/
|-- data/
|   |-- orders.json
|   |-- complaints.json
|   `-- agent_events.json
|-- docs/
`-- tests/
```

## Getting Started

### Prerequisites

- Python 3.13+
- A modern browser
- Optional Z.ai and/or Groq API keys for live LLM calls

### Installation

```bash
git clone https://github.com/Ph0enix19/Komplain.AI.git
cd Komplain.AI
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt -r requirements-dev.txt
```

macOS/Linux:

```bash
source .venv/bin/activate
python -m pip install -r requirements.txt -r requirements-dev.txt
```

### Environment Variables

Create `.env` from `.env.example`:

```env
LLM_PROVIDER=zai
ZAI_API_KEY=your_zai_api_key_here
ZAI_BASE_URL=https://api.z.ai/api/coding/paas/v4
ZAI_MODEL=glm-5.1
ZAI_VISION_MODEL=glm-4.5v
VISION_ENABLED=true

GROQ_API_KEY=your_groq_api_key_here
GROQ_MODEL=llama-3.3-70b-versatile
```

For deterministic local fallback behavior without real LLM calls:

```env
USE_LLM_AGENTS=false
VISION_ENABLED=false
```

### Run Locally

Start the backend:

```bash
python -m uvicorn backend.main:app --host 127.0.0.1 --port 8000
```

Start the frontend:

```bash
python -m http.server 3000 --directory frontend --bind 127.0.0.1
```

Open `http://127.0.0.1:3000`.

Run tests:

```bash
python -m pytest -q
ruff check backend/ tests/
ruff format --check backend/ tests/
```

## Screenshots / Demo

- Current README previously listed a frontend demo: `https://komplain-test-xi2r.vercel.app/`
- Current README previously listed backend health: `https://komplaintest.onrender.com/api/health`
- [TODO: confirm both deployed links are still live before publishing]
- [TODO: add screenshots/demo GIF]

## Current Status

Hackathon MVP. The backend and dashboard are functional, tested, and documented, but this is not production-grade yet. Storage is JSON-based, there is no user authentication, and operator approval is handled in the frontend rather than persisted as a full workflow.

## Future Improvements

- Move JSON storage to PostgreSQL or another managed database.
- Add operator authentication, tenant isolation, and role-based review flows.
- Persist approval/rejection actions through backend endpoints.
- Add rate limiting and stronger deployment observability.
- Add frontend end-to-end tests.
- Verify and refresh screenshots, demo links, and architecture diagrams.

## What I Learned

- How to design an AI workflow that keeps humans in control of support decisions.
- How to combine structured extraction, order context, optional visual evidence, and fallback logic.
- How to expose AI agent behavior through trace events instead of hiding it behind one response.
- How token usage, latency, and estimated cost can be made visible even in a hackathon MVP.
