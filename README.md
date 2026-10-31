# 🚀 FinAlpha — AI-Powered Financial Intelligence & Investment Management System

> An advanced, interview-ready personal finance intelligence platform that combines rich AI-driven visual analytics with a conversational AI assistant — helping users *understand* their money without ever giving buy/sell advice.

![License](https://img.shields.io/badge/license-MIT-green.svg)
![Node](https://img.shields.io/badge/Node.js-20%20LTS-339933?logo=node.js)
![React](https://img.shields.io/badge/React-18.3-61DAFB?logo=react)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?logo=python)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [API Documentation](#-api-documentation)
- [AI Philosophy & Guardrails](#-ai-philosophy--guardrails)
- [Contributing](#-contributing)
- [License](#-license)

---

##  Overview

FinAlpha is a **proactive wealth management system** (not just a data tracker) that:

1. **Tracks** all your investments — Stocks, Mutual Funds, FDs, Gold, Real Estate, EPF/PPF, Crypto, NPS
2. **Analyzes** your portfolio with quantitative models (Monte Carlo, momentum, sentiment)
3. **Alerts** you with AI-generated insights (rebalancing, tax-loss harvesting, SIP optimization)
4. **Visualizes** your wealth with rich D3.js charts (Sankey, heatmaps, treemaps)
5. **Converses** via a RAG-powered chatbot that answers questions about YOUR portfolio
6. **Respects** regulatory boundaries — never gives buy/sell advice (SEBI RIA compliance)

### What Makes It Different

| Feature | Traditional Trackers | FinAlpha |
|---|---|---|
| Portfolio Tracking | ✅ Basic | ✅ Multi-asset, multi-portfolio, family view |
| AI Insights | ❌ | ✅ Auto-narrated, anomaly-highlighted |
| Tax Optimization | ❌ | ✅ Tax-loss harvesting engine |
| Portfolio Rebalancing | ❌ | ✅ Algorithmic drift detection |
| SIP Optimization | ❌ | ✅ "Buy the Dip" market correction alerts |
| Monte Carlo Simulation | ❌ | ✅ 10,000 scenario stress testing |
| AI Chatbot (RAG) | ❌ | ✅ Portfolio-aware, guardrailed |
| D3 Visualizations | ❌ | ✅ Sankey, heatmap, treemap |
| CAS Import | ⚠️ Limited | ✅ NSDL/CAMS PDF auto-parse |

---

## ✨ Key Features

### Proactive Wealth Dashboard
- Total net worth with XIRR calculation
- Asset allocation (Equity / Debt / Gold / Real Estate / Crypto)
- Live P&L with gain/loss coloring
- Family View for household wealth aggregation
- AI "Insight of the Day" narration

### Advanced Visualizations
- **Sankey Diagram:** Income → Investments → Goals cash flow
- **Correlation Heatmap:** Cross-holding correlation analysis
- **Allocation Treemap:** Hierarchical asset breakdown
- **"Explain This" Button:** Every chart connects to the AI chatbot

### AI/Quant Engine
- **Monte Carlo Simulation:** 10,000 scenarios for stress testing
- **Momentum Analysis:** Linear regression + DMA crossover signals
- **Market Sentiment:** VADER NLP on financial news headlines
- **Anomaly Detection:** Z-score flagging of unusual patterns

### 🔔 Smart Alert System
- **Rebalancing Alerts:** Auto-detect allocation drift
- **Tax-Loss Harvesting:** Identify tax-saving opportunities
- **SIP Optimizer:** Market dip detection for step-up SIPs

###  AI Chatbot (RAG)
- Natural language Q&A about YOUR portfolio
- Grounded in real portfolio data via ChromaDB
- Two-layer guardrails (prompt + classifier)
- Transparent sourcing ("Based on: your equity holdings...")
- Runs 100% free via Ollama (local) or Groq (cloud)

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     React.js Frontend                        │
│  (Tailwind CSS, Recharts, D3.js, Socket.io-client)          │
└────────────────────────┬────────────────────────────────────┘
                         │ HTTP / WebSocket
┌────────────────────────▼────────────────────────────────────┐
│                  Node.js Express Backend                     │
│  (REST API, JWT Auth, Socket.io, Sequelize ORM)             │
└──────┬─────────────────┬────────────────────────────────────┘
       │                 │ HTTP (proxy)
       │    ┌────────────▼─────────────────────────────────┐
       │    │       Python FastAPI AI Microservice           │
       │    │  (Quant Engine, RAG Pipeline, NLP)            │
       │    │  ┌─────────────────────────────────────┐      │
       │    │  │  ChromaDB     │  Ollama (LLM)       │      │
       │    │  │  (Vectors)    │  (Local Inference)   │      │
       │    │  └─────────────────────────────────────┘      │
       │    └──────────────────────────────────────────────┘
       │
┌──────▼──────────────┐
│   MySQL 8.0         │
│   (12 tables,       │
│    views, indexes)  │
└─────────────────────┘
```

---

## 🛠 Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend** | React 18, Tailwind CSS, Recharts, D3.js | UI, charts, visualizations |
| **Backend** | Node.js 20, Express 4, Sequelize 6 | REST API, auth, business logic |
| **Database** | MySQL 8.0 | Normalized financial data storage |
| **AI Service** | Python 3.11, FastAPI | Quant models, RAG pipeline |
| **LLM** | Ollama (Llama 3.2 / Mistral) | Local AI inference (free) |
| **Embeddings** | sentence-transformers (MiniLM) | Text embeddings for RAG |
| **Vector Store** | ChromaDB | RAG context retrieval |
| **Real-time** | Socket.io | Chat streaming |
| **Market Data** | yfinance | Historical price data |

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** 20 LTS or later
- **Python** 3.11 or later
- **MySQL** 8.0 or later
- **Ollama** (optional, for local AI chatbot)
- **Java** 8+ (only if using tabula-py for PDF parsing)

### 1. Clone & Setup Database

```bash
# Clone the repository
git clone <your-repo-url>
cd FinAlpha

# Create the database and tables
mysql -u root -p < database/schema.sql

# (Optional) Load demo data
mysql -u root -p < database/seed.sql
```

### 2. Setup Backend (Node.js)

```bash
cd server
cp .env.example .env
# Edit .env with your MySQL credentials and JWT secret

npm install
npm run dev  # Starts on http://localhost:5000
```

### 3. Setup AI Microservice (Python)

```bash
cd ai-service
cp .env.example .env
# Edit .env if needed

python -m venv venv
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

pip install -r requirements.txt

# Download NLTK data (one-time)
python -c "import nltk; nltk.download('vader_lexicon')"

uvicorn main:app --reload --port 8000  # Starts on http://localhost:8000
```

### 4. Setup Ollama (Optional — for AI Chatbot)

```bash
# Install Ollama from https://ollama.com
ollama pull llama3.2    # or: ollama pull mistral
ollama serve            # Starts on http://localhost:11434
```

### 5. Setup Frontend (React)

```bash
cd client
npm install
npm start  # Starts on http://localhost:3000
```

### 6. Demo Login

If you loaded the seed data:
- **Email:** `madhav1@demo.com`
- **Password:** `Demo@1234`

---

##  Project Structure

```
FinAlpha/
├── database/           # MySQL schema + seed data
│   ├── schema.sql      # 12 tables, views, indexes, trigger
│   └── seed.sql        # Demo portfolio data
│
├── server/             # Node.js Express Backend
│   └── src/
│       ├── config/     # DB + environment
│       ├── middleware/  # Auth, errors, rate limiting
│       ├── models/     # 12 Sequelize models
│       ├── controllers/# 9 controllers
│       ├── routes/     # 9 route files
│       ├── services/   # Business logic layer
│       └── utils/      # XIRR, trade calc, validators
│
├── ai-service/         # Python FastAPI AI Microservice
│   ├── routers/        # API endpoints
│   ├── services/       # Quant engines (Monte Carlo, etc.)
│   ├── rag/            # RAG pipeline (embedder, retriever, LLM, guardrails)
│   └── utils/          # Cache, helpers
│
└── client/             # React.js Frontend
    └── src/
        ├── store/      # Redux Toolkit + RTK Query
        ├── components/ # 50+ components
        ├── pages/      # 11 pages
        ├── hooks/      # Custom hooks
        └── utils/      # Formatters, constants
```

---

## 📡 API Documentation

### Backend (Node.js) — `http://localhost:5000/api`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/auth/register` | User registration |
| POST | `/auth/login` | Login (returns JWT) |
| GET | `/auth/profile` | Get user profile |
| GET/POST | `/portfolios` | List / Create portfolios |
| GET/PUT/DELETE | `/portfolios/:id` | Portfolio CRUD |
| GET/POST | `/assets` | List / Create assets |
| GET/PUT/DELETE | `/assets/:id` | Asset CRUD |
| GET/POST | `/trades` | List / Create trades |
| GET/POST | `/goals` | List / Create goals |
| GET | `/alerts` | List alerts |
| PATCH | `/alerts/:id/read` | Mark alert as read |
| POST | `/chat` | Send message to AI chatbot |
| POST | `/import/csv` | Import CSV data |
| POST | `/import/cas` | Import CAS PDF |
| GET | `/reports/portfolio` | Download PDF report |

### AI Service (Python) — `http://localhost:8000/api/ai`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/stress-test` | Monte Carlo simulation |
| GET | `/momentum/{symbol}` | Momentum analysis |
| GET | `/market-data/{symbol}` | Market data + stats |
| GET | `/sentiment/{symbol}` | News sentiment |
| POST | `/insight-of-day` | AI narration |
| POST | `/anomaly-detect` | Anomaly detection |
| POST | `/chat` | RAG chatbot |
| POST | `/parse-cas` | CAS PDF parsing |

---

## 🛡 AI Philosophy & Guardrails

### Core Principle
> Every AI component exists to **track, manage, explain, and surface insight** about the user's own portfolio data — never to give buy/sell advice.

### Two-Layer Defense-in-Depth

1. **Layer 1 — System Prompt:** Every LLM call includes explicit instructions prohibiting investment advice.

2. **Layer 2 — Keyword Classifier:** A backend classifier scans both incoming questions AND outgoing answers for investment advice patterns. Blocked responses are replaced with a safe redirect.

### Why This Matters
- **Regulatory:** Giving personalized security-level advice in India requires SEBI RIA registration
- **Technical:** An analytics-only AI layer is the more interesting design choice
- **Interview:** Strong story about defense-in-depth, responsible AI, and regulatory awareness

---

## Disclaimers

- **Educational Project:** This system is built for educational/portfolio purposes. It is NOT a registered investment advisor.
- **Market Data:** Uses yfinance (unofficial Yahoo wrapper) and free APIs. Data may be delayed or unavailable.
- **No Financial Advice:** The AI chatbot and all insights are analytical only. Always consult a SEBI-registered advisor for investment decisions.
- **Indian Market Focus:** Designed for Indian investors (INR, NSE/BSE, Indian tax rules).

---

## License

This project is licensed under the MIT License.

---

##  Acknowledgments

- [yfinance](https://github.com/ranaroussi/yfinance) — Yahoo Finance market data
- [Ollama](https://ollama.com) — Local LLM inference
- [ChromaDB](https://www.trychroma.com) — Vector database
- [sentence-transformers](https://www.sbert.net) — Text embeddings
- [Recharts](https://recharts.org) — React charting
- [D3.js](https://d3js.org) — Advanced visualizations
- [Tailwind CSS](https://tailwindcss.com) — Utility-first CSS

---

**Built for the Indian investor community**
