

# Project Directory Structure
supa/
│
├── 📁 supa-backend/                    # EXISTING Node.js app
│   ├── src/
│   │   ├── routes/
│   │   │   └── ai.routes.js           # NEW: AI proxy endpoints
│   │   └── (existing structure...)
│   ├── package.json
│   └── .env                           # Add AI_SERVICE_URL
│
├── 📁 supa-ai-service/              # NEW: Python AI Microservice
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py                    # FastAPI app initialization
│   │   ├── api/
│   │   │   ├── __init__.py
│   │   │   ├── v1/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── endpoints.py       # /ask, /health, /feedback
│   │   │   │   └── dependencies.py    # Auth, rate limiting
│   │   │   └── websockets.py          # (Optional) For real-time
│   │   │
│   │   ├── core/
│   │   │   ├── __init__.py
│   │   │   ├── config.py              # App configuration
│   │   │   ├── security.py            # API key validation
│   │   │   └── logging_config.py
│   │   │
│   │   ├── services/
│   │   │   ├── __init__.py
│   │   │   ├── document_service.py    # Document processing
│   │   │   ├── embedding_service.py   # Text → vectors
│   │   │   ├── search_service.py      # Vector similarity search
│   │   │   ├── llm_service.py         # Answer generation
│   │   │   ├── simple_matcher.py      # Phase 1: Keyword matching
│   │   │   └── cache_service.py       # Redis/Memory caching
│   │   │
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── schemas.py             # Pydantic models
│   │   │   ├── database.py            # MongoDB models
│   │   │   └── ai_models.py           # AI response models
│   │   │
│   │   ├── utils/
│   │   │   ├── __init__.py
│   │   │   ├── document_parser.py     # PDF/DOCX/Excel parsers
│   │   │   ├── text_chunker.py        # Split text for embedding
│   │   │   ├── helpers.py             # Utility functions
│   │   │   └── constants.py           # SUPA-specific constants
│   │   │
│   │   └── workers/                   # Background tasks
│   │       ├── __init__.py
│   │       └── embedding_worker.py    # Async document processing
│   │
│   ├── data/
│   │   ├── raw_documents/             # Your SUPA documents here
│   │   │   ├── programme_overview.pdf
│   │   │   ├── curriculum/
│   │   │   ├── policies/
│   │   │   └── faqs/
│   │   │
│   │   ├── processed/                 # Processed text files
│   │   ├── embeddings/                # Vector embeddings cache
│   │   └── vector_store/              # Chroma/Qdrant data
│   │
│   ├── tests/
│   │   ├── __init__.py
│   │   ├── test_api.py
│   │   ├── test_services.py
│   │   └── test_documents/
│   │
│   ├── scripts/
│   │   ├── process_documents.py       # Initial document ingestion
│   │   ├── build_index.py             # Build vector index
│   │   └── evaluate_responses.py      # Test accuracy
│   │
│   ├── dockerfile
│   ├── requirements.txt
│   ├── pyproject.toml
│   ├── .env.example
│   └── README.md
│
├── 📁 supa-frontend/                  # EXISTING Vite app
│   ├── src/
│   │   ├── components/
│   │   │   ├── ai-chat/               # NEW: Chat components
│   │   │   │   ├── ChatInterface.vue (or .jsx)
│   │   │   │   ├── MessageBubble.vue
│   │   │   │   ├── SuggestedQuestions.vue
│   │   │   │   └── index.js
│   │   │   │
│   │   │   └── (existing components...)
│   │   │
│   │   ├── services/
│   │   │   └── ai.service.js          # NEW: API calls to Node backend
│   │   │
│   │   ├── assets/
│   │   ├── App.vue (or .jsx)
│   │   └── main.js
│   │
│   ├── package.json
│   └── vite.config.js
│
├── 📁 shared/                         # Shared between services
│   ├── types/                         # TypeScript/JSON schemas
│   │   ├── ai.types.ts
│   │   └── supaprogram.types.ts
│   │
│   └── scripts/
│       ├── setup.sh                   # One-time setup
│       └── deploy_local.sh
│
├── 📁 infrastructure/
│   ├── docker-compose.yml
│   ├── nginx/
│   │   └── nginx.conf                 # Reverse proxy config
│   ├── mongodb/
│   │   └── init-mongo.js              # DB initialization
│   └── monitoring/
│       └── prometheus.yml             # Metrics collection
│
├── 📁 docs/
│   ├── api/
│   │   ├── node-api.md
│   │   └── python-ai-api.md
│   ├── ai-capabilities.md
│   ├── deployment-guide.md
│   └── user-guide.md
│
├── .gitignore
├── Makefile                          # Common commands
├── docker-compose.yml                # Root compose file
└── README.md