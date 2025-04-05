# prompt-engine-kit
```
┌──────────────────────────────┐
│        FastAPI App           │
│  - Routing Layer             │
│  - Controllers               │
│  - Auth Middleware           │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│     Agent Manager Layer      │  ← Factory + Registry
│  - Resolves agent by name    │
│  - Loads correct agent logic │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│     Prompt Controller Layer  │  ← Strategy + Jinja2
│  - Per-agent prompt builder  │
│  - Image & text handling     │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│     LLM Connector Layer      │  ← Adapter Pattern
│  - API calls to LLMs         │
│  - Handles model-specific    │
│    auth, retries, parsing    │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│      LLM Provider API        │
│    (e.g. GPT-4 Vision, etc)  │
└──────────────────────────────┘
```

# Folder Structure: prompt-engine-kit/

```
prompt-engine-kit/
├── app/
│   ├── main.py                  # FastAPI app instance
│   ├── api/
│   │   ├── routes/
│   │   │   └── agent_router.py  # Route definitions (Phase 2)
│   │   └── controllers/
│   │       └── agent_controller.py # Logic for /agent endpoints (Phase 2)
│   ├── auth/
│   │   └── auth.py              # API Key verification logic (Phase 2)
│   ├── agents/
│   │   ├── base.py              # BaseAgent interface (Phase 3)
│   │   ├── registry.py          # Agent registry/factory (Phase 3)
│   │   ├── calorie_estimator.py # Agent 1 (Phase 4)
│   │   └── rural_chatbot.py     # Agent 2 (Phase 4)
│   ├── core/
│   │   ├── prompt_base.py       # Base Prompt Strategy (Phase 4)
│   │   ├── prompt_calorie.py    # Prompt logic for Calorie Estimator
│   │   └── prompt_rural.py      # Prompt logic for Rural ChatBot
│   ├── llm_connectors/
│   │   ├── base.py              # LLMConnector interface (Phase 5)
│   │   └── openai.py            # OpenAI implementation (Phase 5)
│   └── config/
│       └── settings.py          # Loads .env vars securely
├── .env                         # Local secrets (never commit)
├── requirements.txt             # Python dependencies
├── Dockerfile                   # Container setup
└── .dockerignore                # Ignore files from Docker build
```