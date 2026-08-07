# VU — AI-Powered Virtual Interview Platform

<p align="center">
  <strong>Real-time AI interviews with BARS-anchored scoring, multi-modal cheat detection, and automated performance reports.</strong>
</p>

---

## What is VU?

VU is a graduation project that conducts fully automated AI-driven job interviews. A candidate speaks to an AI interviewer in real time — the system transcribes their speech, evaluates their answers using BARS (Behaviorally Anchored Rating Scales), analyzes their voice for confidence, tracks their face and gaze via webcam, and detects cheating through 5 independent signals. At the end, the recruiter receives a complete performance report with sub-scores, per-question feedback, an overall summary, and an integrity label.

### Key Capabilities

- **Real-time voice interviews** — dual WebSocket (STT + interview control) with edge-tts AI voice
- **BARS-anchored scoring** — 5 LLM-scored dimensions (1-5 scale with behavioral anchors)
- **Multi-modal assessment** — transcript analysis + audio confidence + video face/gaze tracking
- **Cheat detection** — 5 signals: tab switches, no face, multiple faces, gaze away, second speaker (diarization)
- **CV analysis** — 4 BARS dimensions scored from PDF/DOCX, skills extracted for question tailoring
- **Adaptive questioning** — difficulty-aware question count, topic diversity, LLM-driven follow-ups
- **Pluggable LLM** — switch between Gemini and Groq with one environment variable

## Architecture

```
Frontend (React)  ←→  AI Service (FastAPI)  ←→  Backend (NestJS)  ←→  PostgreSQL
                         ├─ STT (AssemblyAI)
                         ├─ LLM (Gemini / Groq)
                         ├─ TTS (edge-tts)
                         ├─ Video (OpenCV + YuNet)
                         └─ Scoring (BARS + cheat detection)
```

## Repositories

| Repo | Description |
|------|-------------|
| [vu-app](https://github.com/vu-app-dev/vu-app) | **Start here** — full-stack deployment with Docker Compose, nginx, docs |
| [vu-ai](https://github.com/vu-app-dev/vu-ai) | AI service (FastAPI, Python) — scoring, STT, TTS, cheat detection |
| [vu-backend](https://github.com/vu-app-dev/vu-backend) | Backend API (NestJS, TypeORM, PostgreSQL) |
| [vu-frontend](https://github.com/vu-app-dev/vu-frontend) | Frontend (React 19, Vite 7, Tailwind) |

## Quick Start

```bash
git clone --recursive https://github.com/vu-app-dev/vu-app.git
cd vu-app
cp .env.example .env   # fill in API keys
docker compose -f compose.yml -f compose.dev.yml up --build
```

 → Frontend at `http://localhost:5173`, Backend at `:3000`, AI at `:8000`

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, Vite 7, Tailwind CSS 4, Recharts |
| Backend | NestJS 11, TypeORM, PostgreSQL 16, JWT |
| AI Service | FastAPI, Gemini/Groq, AssemblyAI, edge-tts, OpenCV+YuNet |
| Deployment | Docker Compose, nginx, Let's Encrypt |

## Documentation

- [Architecture](https://github.com/vu-app-dev/vu-app/blob/main/docs/architecture.md) — system design, request flow, data model
- [AI Scoring](https://github.com/vu-app-dev/vu-app/blob/main/docs/ai-scoring.md) — BARS dimensions, cheat detection, LLM config
- [Deployment](https://github.com/vu-app-dev/vu-app/blob/main/docs/deployment.md) — VPS setup, DNS, SSL, backups

## License

MIT