<div align="center">

# 🧠 EPI Brain

**An AI-powered conversational platform with 9 distinct personality modes, a cross-conversation hybrid memory system, voice-first interaction, and a full-stack architecture built for scale.**

[![Frontend](https://img.shields.io/badge/Frontend-Next.js%2016-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![Backend](https://img.shields.io/badge/Backend-FastAPI-009688?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-99.4%25-3178C6?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org/)
[![Python](https://img.shields.io/badge/Python-99.2%25-3776AB?style=for-the-badge&logo=python)](https://python.org/)
[![Status](https://img.shields.io/badge/Status-In%20Development-yellow?style=for-the-badge)](https://github.com/twinwicksllc)

</div>

---

## 📖 What Is It?

EPI Brain is a full-stack, production-deployed AI chat platform where users converse with an AI that adapts its personality, tone, and expertise based on the selected mode. Whether someone needs a personal friend to talk to, a weight loss coach, a business mentor, or a student tutor — EPI Brain switches its entire persona to match.

The platform goes beyond simple mode-switching: it features a **sophisticated hybrid memory system** that remembers users across conversations, a **Discovery Mode onboarding flow** with LLM-first contextual validation, **voice-first interaction** with push-to-talk and live transcription, a **"Vault" for saved notes**, and a **secure Admin Dashboard** for usage tracking and cost monitoring.

**Frontend:** Next.js 16 + TypeScript · **Backend:** FastAPI + Python · **AI:** Groq/Llama 3.1, Anthropic Claude, OpenAI Whisper · **Voice:** ElevenLabs TTS

---

## ✨ Platform Features

### 🎭 9 Personality Modes

Each mode has a completely distinct persona, system prompt, tone, and color identity. The AI's entire behavior, language style, and depth of knowledge shifts based on the active mode:

| Mode | Color | Focus |
|---|---|---|
| **Personal Friend** | 🔵 Blue `#3B82F6` | Casual, empathetic personal conversation |
| **Sales Agent** | 🟡 Amber `#F59E0B` | Objection handling, sales training |
| **Student Tutor** | 🟢 Emerald `#10B981` | Academic support and explanations |
| **Kids Learning** | 🩷 Pink `#EC4899` | Age-appropriate educational content |
| **Christian Companion** | 🟣 Violet `#8B5CF6` | Faith-based conversation and support |
| **Customer Service** | 🔷 Indigo `#6366F1` | Professional support interactions |
| **Psychology Expert** | 🩵 Teal `#14B8A6` | Mental wellness and emotional guidance |
| **Business Mentor** | 🩶 Slate `#64748B` | Strategy, growth, and entrepreneurship |
| **Weight Loss Coach** | 🔴 Red `#EF4444` | Fitness, nutrition, and accountability |

> **Note:** Manual mode switching has been replaced by an intelligent mode assignment system — the AI routes users from **Discovery Mode** into the most appropriate default persona based on their onboarding responses.

---

### 🔍 Discovery Mode — LLM-First Onboarding

When a user first arrives, they enter **Discovery Mode** — a structured, conversational onboarding flow designed to understand who they are and what they need before routing them to the right personality.

Discovery Mode v3.0 uses **LLM-first contextual validation** rather than simple regex:

- **Contextual Name Validation** — The AI uses an LLM to determine if a response is a genuine name, a playful joke, or spam — not just a length check
- **Correction Handling** — Users can correct a misheard name and the AI gracefully updates its understanding
- **Dynamic Greetings** — No more templated "Nice to meet you, [Name]!" — every greeting is generated in context
- **Verification Step** — After capturing a name, the AI confirms before proceeding
- **Dual Strike Counter** — 5 chances for genuine engagement, 3 for obvious non-engagement, with weighted scoring (1–3 points) based on behavior type
- **Intelligent Engagement Assessment** — The system classifies responses as `playful`, `dismissive`, or `spam` and responds appropriately

```
User: "Skinna marinka dinka dink"
AI: "That's a catchy tune! But I'd love to know what to actually call you.
    What's your name?"
```

---

### 🧠 Hybrid Memory System

EPI Brain remembers users across conversations — not just within a session. The memory system is built across three tiers:

#### **Core Variables** (Actively Collected)
The AI naturally weaves these questions into early conversation:
- User's name, preferred name, location, timezone, language preference
- Communication preferences: tone (formal/casual), style (detailed/concise), response length

#### **Active Memory** (Automatically Extracted)
Every 5 messages, the AI analyzes the last 10 messages and extracts:
- Interests, hobbies, and life events
- Goals, targets, and objectives
- Personality-specific context per mode (e.g., for Weight Loss Coach: fitness goals, exercise preferences, dietary restrictions; for Business Mentor: revenue goals, company stage, challenges)

```json
{
  "personality_contexts": {
    "weight_loss_coach": {
      "fitness_goals": ["lose 20 pounds by summer"],
      "exercise_preferences": ["hiking"],
      "exercise_dislikes": ["gym"],
      "dietary_restrictions": ["peanut_allergy"]
    }
  }
}
```

#### **Privacy Variables** (Consent-Gated)
Sensitive information (financial details, health metrics) is never stored without explicit user consent. The AI detects this content and generates a natural consent request:

```
User: "My current revenue is $50K/month and I want to reach $200K."
AI: "That's an ambitious goal! Would you like me to remember your
    revenue numbers so I can track your progress in future conversations?
    I won't share this with anyone."
```

#### Memory API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/v1/chat/memory/completion-status` | Core variable completion % |
| GET | `/api/v1/chat/memory/next-priority-variable` | Next variable to collect |
| POST | `/api/v1/chat/memory/extract` | Trigger manual memory extraction |
| POST | `/api/v1/chat/memory/privacy-consent` | Handle user consent |
| GET/PUT | `/api/v1/chat/memory/privacy-settings` | Manage privacy preferences |

---

### 🎙️ Voice-First Interaction

EPI Brain is designed as a **Pocket Assistant** — mobile-first with voice at the center:

**Push-to-Talk (PTT)**
- **Desktop:** Hold `Spacebar` to record, release to send (doesn't trigger while typing)
- **Mobile:** 64×64px tap-to-toggle microphone button (fixed bottom-right)
- Powered by the **Web Speech API** with continuous listening, interim results, and auto-reconnect

**Live Transcript Bubble**
- Glassmorphic bubble displays above the input as the user speaks
- Shows real-time "EPI is hearing..." transcription with animated cursor
- Auto-hides when not recording

**ElevenLabs TTS**
- AI responses can be played back with natural voice synthesis
- Voice preference stored per user in memory

---

### 🔐 The Vault

A **mobile-optimized notes sidebar** accessible from the dashboard header:

- **4 note types:** Note 📝, Draft ✍️, Reflection 🤔, Quick ⚡
- Filter tabs to view by type
- Click to expand full note view
- Tap-to-delete with confirmation
- Created via the **Floating Action Button (FAB)** on mobile or programmatically
- Stored server-side via `POST /api/v1/assistant-tools/notes`

---

### 📱 Mobile "Pocket Assistant" Experience

The dashboard is fully optimized for mobile-first use:

**Floating Action Button (FAB)** — Mobile only, fixed bottom-right:
1. **📝 New Note** — Instantly create a quick vault note
2. **💼 Sales Mode** — One-tap switch to sales mode
3. **✉️ Message Admin** — Sends a support request directly to the platform admin

**Slim Rail Sidebar** — The conversation sidebar collapses to a 70px icon rail via a smooth 300ms CSS transition (GPU-accelerated, no JS animation). The main content area expands to fill ~95% width in collapsed mode.

---

### 📊 Admin Dashboard

A protected route at `/admin` (requires `is_admin` flag in JWT) with:

**System Metrics Overview:**
- Total tokens consumed (formatted as M for millions)
- Total messages and conversation count
- Estimated cost (tokens × $0.00001)
- Total users and daily active users

**Detailed Analytics at `/admin/analytics`:**
- Per-user usage table with plan tier badges (Free / Basic / Pro / Enterprise)
- Sortable columns: email, tokens, voice minutes, conversations, last active
- Filter by plan tier
- Responsive grid layout

**Security:**
- JWT token validation + `is_admin` check on every load
- Non-admin users silently redirected to `/dashboard`
- No sensitive data in error messages
- Fallback metrics aggregation if primary endpoint is unavailable

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                    EPI Brain Frontend                        │
│           Next.js 16 · TypeScript · Tailwind CSS            │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │ Slim Rail ←→ Dashboard ←→ Chat Interface            │   │
│  │  Sidebar      State Mgmt    Messages + Input        │   │
│  │  (70-256px)   (React)       + Live Transcript       │   │
│  └────────────────────────┬─────────────────────────────┘   │
│                           │ Axios + WebSocket               │
└───────────────────────────┼─────────────────────────────────┘
                            ↓
┌─────────────────────────────────��────────────────────────────┐
│                    EPI Brain Backend                         │
│              FastAPI · Python 3.11 · Uvicorn                │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ API Layer (/api/v1/*)                               │    │
│  │  auth · chat · voice · modes · users · admin       │    │
│  └────────────────────┬────────────────────────────────┘    │
│                       │                                      │
│  ┌──────────┬──────────┴──────┬─────────────────────────┐   │
│  │ Memory   │ Discovery Mode  │ Personality Router       │   │
│  │ System   │ (LLM-First)     │ (9 modes + prompts)     │   │
│  └──────────┴─────────────────┴─────────────────────────┘   │
│                                                              │
│  ┌──────────┬──────────────┬──────────────────────────��───┐ │
│  │PostgreSQL│ Redis Cache  │ Vector Embeddings (pgvector) │ │
│  └──────────┴──────────────┴──────────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
                            │
       ┌────────────────────┼──────────────────────┐
       ↓                    ↓                       ↓
┌──────────────┐   ┌─────────────────┐   ┌──────────────────┐
│  AI Models   │   │  Voice Services │   │  External APIs   │
│  Groq/Llama  │   │  ElevenLabs TTS │   │  Stripe Billing  │
│  Anthropic   │   │  OpenAI Whisper │   │  Twilio SMS      │
│  Claude      │   │  Web Speech API │   │  SendGrid Email  │
└──────────────┘   └─────────────────┘   └──────────────────┘
```

---

## 🛠️ Tech Stack

### Frontend
| Layer | Technology |
|---|---|
| **Framework** | Next.js 16 (App Router, Turbopack) |
| **Language** | TypeScript 5.7 (99.4% of codebase) |
| **Styling** | Tailwind CSS 3.4 |
| **HTTP Client** | Axios |
| **Real-time** | PartySocket (WebSocket) |
| **Voice** | Web Speech API |
| **Icons** | Lucide React |
| **Date Utils** | date-fns |
| **Deployment** | Vercel (auto-deploy on push to `main`) |

### Backend
| Layer | Technology |
|---|---|
| **Framework** | FastAPI 0.115 + Uvicorn |
| **Language** | Python 3.11+ (99.2% of codebase) |
| **Database** | PostgreSQL 15 + pgvector extension |
| **ORM** | SQLAlchemy 2.0 (async) |
| **Migrations** | Alembic |
| **Cache** | Redis |
| **Auth** | JWT (python-jose) + bcrypt |
| **Validation** | Pydantic v2 |
| **AI — Chat** | Groq (Llama 3.1) · Anthropic Claude |
| **AI — STT** | OpenAI Whisper |
| **AI — TTS** | ElevenLabs |
| **AI — Embeddings** | sentence-transformers + pgvector |
| **Background Tasks** | Celery + Redis |
| **Rate Limiting** | slowapi |
| **Payments** | Stripe |
| **SMS** | Twilio |
| **Email** | SendGrid |
| **Monitoring** | Sentry (FastAPI integration) |
| **Deployment** | Render (auto-deploy from GitHub) |
| **Containerization** | Docker + docker-compose |

---

## 🗄️ Database Schema

### `users`
| Column | Type | Description |
|---|---|---|
| `id` | UUID PK | Auto-generated |
| `email` | VARCHAR UNIQUE | User email |
| `hashed_password` | VARCHAR | bcrypt hash |
| `tier` | VARCHAR | `free` / `basic` / `pro` / `enterprise` |
| `voice_preference` | VARCHAR | TTS voice ID |
| `global_memory` | JSON | Cross-conversation memory store |
| `is_admin` | BOOLEAN | Admin access flag |
| `created_at` / `updated_at` | TIMESTAMP | — |

### `conversations`
| Column | Type | Description |
|---|---|---|
| `id` | UUID PK | — |
| `user_id` | UUID FK | Owner |
| `mode` | VARCHAR | Active personality mode |
| `title` | VARCHAR | Auto-generated title |
| `session_memory` | JSON | Per-conversation memory |
| `created_at` / `updated_at` | TIMESTAMP | — |

### `messages`
| Column | Type | Description |
|---|---|---|
| `id` | UUID PK | — |
| `conversation_id` | UUID FK | Parent conversation |
| `role` | VARCHAR | `user` or `assistant` |
| `content` | TEXT | Message body |
| `embedding` | VECTOR(384) | For semantic memory search |
| `created_at` | TIMESTAMP | — |

### `learning_patterns`
| Column | Type | Description |
|---|---|---|
| `id` | UUID PK | — |
| `user_id` | UUID FK | — |
| `mode` | VARCHAR | Mode context |
| `pattern_type` | VARCHAR | Category |
| `success_score` | FLOAT | Engagement quality |
| `metadata` | JSONB | Flexible payload |

---

## 📡 API Endpoints

### Authentication
```
POST /api/v1/auth/register
POST /api/v1/auth/login
POST /api/v1/auth/refresh
POST /api/v1/auth/logout
```

### Chat
```
POST   /api/v1/chat/message               Send message + get AI response
GET    /api/v1/chat/conversations          List user conversations
GET    /api/v1/chat/conversations/{id}     Get specific conversation
POST   /api/v1/chat/conversations          Create new conversation
DELETE /api/v1/chat/conversations/{id}     Delete conversation
```

### Memory
```
GET    /api/v1/chat/memory/completion-status
GET    /api/v1/chat/memory/next-priority-variable
POST   /api/v1/chat/memory/extract
POST   /api/v1/chat/memory/privacy-consent
GET    /api/v1/chat/memory/privacy-settings
PUT    /api/v1/chat/memory/privacy-settings
```

### Voice
```
POST /api/v1/voice/synthesize    Text-to-speech (ElevenLabs)
POST /api/v1/voice/transcribe    Speech-to-text (Whisper)
```

### Users
```
GET /api/v1/users/me             Current user profile
PUT /api/v1/users/me             Update profile
GET /api/v1/users/me/usage       Usage statistics
```

### Assistant Tools
```
POST   /api/v1/assistant-tools/notes          Create vault note
GET    /api/v1/assistant-tools/notes          List notes
GET    /api/v1/assistant-tools/notes/{id}     Get note
DELETE /api/v1/assistant-tools/notes/{id}     Delete note
POST   /api/v1/assistant-tools/internal-message  Message admin
```

### Admin
```
GET /api/v1/admin/usage              Per-user usage stats
GET /api/v1/admin/usage/{user_id}    Single user stats
GET /api/v1/admin/usage/report       Aggregated system report
```

---

## 🎨 Design System

EPI Brain uses a **glassmorphic purple-neon** visual language throughout:

```
Backgrounds:  #1a0a2e → #2d1b4e  (deep purple gradient)
Primary:      #7B3FF2             (violet)
Secondary:    #A78BFA             (light violet)
Hover:        #6B46C1             (dark violet)
Accent:       #E9D5FF             (lavender)
Border:       #7B3FF2/20-30%      (transparent violet)

Effects:
  backdrop-blur-md / xl
  shadow-lg shadow-purple-500/30
  pulse animations on active states
  300ms ease-in-out transitions (GPU-accelerated CSS)
```

---

## 🚀 Getting Started

### Prerequisites
- **Frontend:** Node.js 20+, pnpm
- **Backend:** Python 3.11+, PostgreSQL 15+, Redis

### Frontend Setup

```bash
git clone https://github.com/twinwicksllc/epi-brain-frontend.git
cd epi-brain-frontend
pnpm install
cp .env.example .env.local
pnpm dev
# → http://localhost:3000
```

```env
# .env.local
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_API_VERSION=v1
NEXT_PUBLIC_ENABLE_VOICE=true
NEXT_PUBLIC_ENVIRONMENT=development
```

### Backend Setup

```bash
git clone https://github.com/twinwicksllc/epi-brain-backend.git
cd epi-brain-backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
docker-compose up -d postgres redis
alembic upgrade head
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
# → API: http://localhost:8000
# → Docs: http://localhost:8000/docs
```

```env
# .env
DATABASE_URL=postgresql://user:password@localhost:5432/epi_brain_dev
REDIS_URL=redis://localhost:6379
JWT_SECRET_KEY=your-secret-key
GROQ_API_KEY=gsk_...       # Free at console.groq.com
CLAUDE_API_KEY=sk-ant-...  # Optional (Anthropic)
OPENAI_API_KEY=sk-...      # Whisper STT
ELEVENLABS_API_KEY=...     # TTS
STRIPE_SECRET_KEY=sk_test_...
MEMORY_ENABLED=true
ENVIRONMENT=development
```

---

## 📈 Build Phases Completed

| Phase | Description | Status |
|---|---|---|
| Phase 1 | Foundation, auth, basic chat | ✅ Complete |
| Phase 2 | Hybrid Memory System (core vars + active extraction + privacy) | ✅ Complete |
| Phase 2A | Semantic Memory Integration (pgvector embeddings) | ✅ Complete |
| Phase 2B | Goal Management Integration | ✅ Complete |
| Phase 3 | Personality Router (Discovery Mode → mode assignment) | ✅ Complete |
| Phase 3 v2 | Discovery Mode LLM-First Validation | ✅ Complete |
| Phase 3 v3 | Dual Strike Counter + Weighted Engagement Scoring | ✅ Complete |
| Phase 4 | CBT/Accountability framework | 🔄 In Progress |
| Voice Phase 1 | PTT + Live Transcript + ElevenLabs TTS | ✅ Complete |
| Pocket Assistant | Mobile FAB + The Vault + Admin Analytics | ✅ Complete |
| Slim Rail | Collapsible sidebar with 300ms CSS transitions | ✅ Complete |
| Admin Dashboard | JWT-gated metrics dashboard + usage report | ✅ Complete |

---

## 🔜 Roadmap

### Near-term
- Phase 4: Full CBT/accountability flow with goal setting, check-ins, and progress tracking
- Vault enhancements: search, sort, export to markdown/PDF, rich text editing
- Voice commands (e.g., "new note", "sales mode") via voice activity detection
- Frontend memory management UI (completion status, privacy settings)

### Medium-term
- Real-time admin metrics via WebSocket
- Voice activity detection (VAD) for hands-free experience
- Customizable FAB quick actions
- Per-mode learning pattern refinement using pgvector similarity

### Long-term
- Multi-language voice support
- Mobile app (React Native)
- White-label licensing
- Enterprise SSO integration

---

## 📄 License

Proprietary software — © TwinWicks LLC. All rights reserved.

Built with ❤️ by [TwinWicks LLC](https://twinwicksllc.com)
