# 🏗️ Technology Stack

Devil Revenant Studio utilizes a **modern, scalable, and production-ready** tech stack across three major projects.

---

## 📦 Core Tech Stack Overview

```
┌─────────────────────────────────────────────────┐
│         DEVIL REVENANT TECH ECOSYSTEM            │
├─────────────────────────────────────────────────┤
│                                                 │
│  CLIENT TIER                                    │
│  ├─ Unity 2021.3.45f2 LTS (Game Engine)       │
│  ├─ React 18 + Vite (Web Frontend)             │
│  ├─ Tailwind CSS (Styling)                     │
│  └─ WebGL (Cross-platform Rendering)           │
│                                                 │
│  SERVER TIER                                    │
│  ├─ Node.js v22.20.0 (Runtime)                 │
│  ├─ Express 4.22.1 (HTTP Framework)            │
│  ├─ Socket.IO 4.8.3 (Real-time)                │
│  └─ Docker (Containerization)                  │
│                                                 │
│  DATA TIER                                      │
│  ├─ MongoDB Atlas (Document DB)                │
│  ├─ Redis Cloud (Cache Layer)                  │
│  └─ PostgreSQL (Future: Structured Data)       │
│                                                 │
│  AI TIER                                        │
│  ├─ Python 3.13.8 (AI Runtime)                 │
│  ├─ FastAPI (API Framework)                    │
│  ├─ OpenAI GPT-4 (NPC Dialogue - fallback)      │
│  ├─ Vertex AI Gemini 2.5 (Primary NPC AI)       │
│  ├─ Meshy AI (3D Asset Generation)               │
│  ├─ NVIDIA Build (GPU Inference)                 │
│  └─ Stable Diffusion (Texture Generation)       │
│                                                 │
│  BLOCKCHAIN TIER                                │
│  ├─ Solidity 0.8.20 (Smart Contracts)          │
│  ├─ Hardhat (Development Framework)            │
│  ├─ Polkadot DOT (Primary Token)               │
│  └─ Alchemy RPC (Node Provider)                │
│                                                 │
│  CLOUD & DEPLOYMENT                             │
│  ├─ Google Cloud Platform (GCP)                │
│  ├─ Amazon Web Services (AWS)                  │
│  ├─ Microsoft Azure                            │
│  ├─ Railway.app (Production Hosting)           │
│  ├─ GitHub Actions (CI/CD)                     │
│  ├─ Docker Hub (Container Registry)            │
│  └─ Vercel (Static Frontend)                   │
│                                                 │
└─────────────────────────────────────────────────┘
```

---

## 🎮 Client Technologies

### Unity (Game Engine)

| Component | Version | Purpose |
|-----------|---------|---------|
| Unity Engine | 2021.3.45f2 LTS | Core game runtime |
| TextMeshPro | 3.0.6 | Rich text rendering |
| Newtonsoft.Json | 3.0.2 | JSON serialization |
| Socket.IO Client | Latest | Real-time multiplayer |

**Platforms:**
- ✅ Windows PC
- ✅ WebGL (browser)
- 🔄 iOS (Q3 2026)
- 🔄 Android (Q3 2026)
- 🔄 Mac (Q4 2026)

**Performance Targets:**
- 60 FPS @ 1080p (PC)
- 30 FPS @ WebGL (browser)
- <50ms network latency
- <100MB memory footprint

### React + Vite (Web App)

| Component | Version | Purpose |
|-----------|---------|---------|
| React | 18.x | UI framework |
| Vite | 5.x | Build tool |
| Tailwind CSS | 3.x | Styling |
| Redux Toolkit | 2.x | State management |
| Stripe.js | Latest | Payment processing |
| Socket.IO Client | 4.x | Real-time sync |

**Features:**
- ✅ Hot module reloading
- ✅ Tree-shaking optimization
- ✅ Mobile responsive
- ✅ PWA capable

---

## 🖥️ Backend Infrastructure

### Node.js Server

```javascript
Runtime:        Node.js v22.20.0
Framework:      Express 4.22.1
Real-time:      Socket.IO 4.8.3
JSON Parsing:   Newtonsoft.Json 3.0.2
Testing:        Jest (100% workflow coverage)
Environment:    Cross-platform (Windows/Linux/Mac)
```

### Core Modules

| Module | Purpose | Status |
|--------|---------|--------|
| **WorldManager** | 4-world switching, room management | ✅ Production |
| **CombatManager** | Server-authoritative PvE/PvP | ✅ Production |
| **NPCManager** | AI character spawn & dialogue | ✅ Production |
| **CrossWorldEventManager** | Event propagation across realms | ✅ Production |
| **QuestManager** | Dynamic quest generation | 🔄 In Dev |
| **StripeService** | AI subscription payments | ✅ Production |
| **BlockchainProxy** | Smart contract interaction | ✅ Testing |

### Middleware Stack

```
Request → CORS → Auth (JWT/Ory) → Validation → Route Handler → Response
```

**Authentication Options:**
- JWT (Bearer token) - Native game clients
- Ory Session - Web clients & OAuth
- API Key - Service-to-service

---

## 💾 Data Storage

### MongoDB Atlas

**Databases:**
- `players` - User accounts, progress
- `characters` - NPC definitions, stats
- `inventory` - Item storage, crafting
- `events` - Cross-world event history
- `quests` - Quest instances & progress
- `subscriptions` - AI quota tracking

**Schema Validation:** Strict (prevents data corruption)  
**Backup:** Daily automated snapshots  
**Replication:** 3-node replica set (high availability)

### Redis Cloud

**Purpose:** Real-time game state caching

| Key | TTL | Purpose |
|-----|-----|---------|
| `position:<playerId>` | 5s | Player location |
| `room:<worldId>` | Live | World member list |
| `event:<worldId>` | 1h | Cross-world events |
| `cache:<questId>` | 30m | AI-generated quests |

**Cluster Mode:** Enabled (horizontal scaling)  
**Persistence:** RDB snapshots every 1h

---

## 🤖 AI Engine (Python)

### Tech Stack

```
Runtime:        Python 3.13.8
Framework:      FastAPI
API Async:      Uvicorn + asyncio
AI Models:      OpenAI GPT-4, Vertex AI
Rate Limiting:  Redis-backed
Logging:        Structured JSON
Monitoring:     OpenTelemetry (future)
```

### NPC Behavior Engine

**Architecture:**
```
Player → Socket.IO → aiWorker.js → FastAPI Endpoint
                                      ↓
                           NPCBehaviorEngine (Python)
                                      ↓
                           CharacterDatabase.json (30 NPCs)
                                      ↓
                           OpenAI GPT-4 API
                                      ↓
                           Response → Socket.IO → Player
```

**Features:**
- ✅ 30 AI-driven NPCs
- ✅ Dynamic dialogue generation
- ✅ Cross-world awareness
- ✅ Personality consistency
- ✅ Rate limiting (subscription tiers)

### LLM Integration

| LLM | Purpose | Cost | Status |
|-----|---------|------|--------|
| Vertex AI Gemini 2.5 | Primary NPC dialogue (99% cheaper) | $0.000075 per 1K tokens | ✅ Primary |
| OpenAI GPT-4 | Fallback NPC dialogue | $0.03 per 1K tokens | ✅ Fallback |
| Meshy AI | 3D model/asset generation | Pay-per-model | ✅ Active |
| NVIDIA Build | GPU inference, model serving | Pay-per-use | ✅ Active |
| Ollama (local) | Development testing | Free | 🔄 In Dev |

---

## ⛓️ Blockchain Layer

### Smart Contracts (Solidity)

**Version:** 0.8.20  
**Chain:** Polkadot (primary), Ethereum (secondary)

#### DOT Marketplace Contract

```solidity
Contract: DOTMarketplace.sol
├── buyItem(itemId, paymentTokens) → Item transferred
├── sellItem(itemId, askPrice) → Listed on marketplace
├── stakeDOT(amount) → Staking rewards
└── withdrawRewards() → Claim earned tokens
```

**Features:**
- ✅ ERC-20 DOT integration
- ✅ Secure escrow system
- ✅ Fee collection (5%)
- ✅ Admin controls (pause, withdraw)

#### NFT Skin Contract (Future)

```solidity
Contract: DevilRevenantNFT.sol (ERC-721)
├── mintSkin(characterClass, rarity)
├── transferSkin(toAddress)
└── burn(tokenId)
```

### Network Configuration

| Network | Purpose | Status |
|---------|---------|--------|
| **Sepolia Testnet** | Development & testing | ✅ Active |
| **Ethereum Mainnet** | Production (future) | 📋 Pending launch |
| **Polkadot** | Primary token (DOT) | ✅ Active |

**RPC Providers:**
- Primary: Alchemy (Ethereum)
- Fallback: Infura
- Backup: Public RPC (rate-limited)

### Security

- ✅ Solidity 0.8.20 (latest features)
- ✅ OpenZeppelin libraries (audited)
- ✅ Hardhat testing suite
- 🔄 Third-party audit (pending)
- ✅ Slither static analysis (CI/CD)

---

## 🚀 Deployment & DevOps

### Production Hosting

| Service | Provider | Purpose | Cost |
|---------|----------|---------|------|
| **API Server** | Railway.app | Node.js hosting | $7-25/mo |
| **Database** | MongoDB Atlas | Data persistence | $57/mo (M20) |
| **Cache** | Redis Cloud | Real-time state | $18/mo |
| **LLM APIs** | OpenAI/Vertex | AI processing | Pay-per-use |
| **3D AI** | Meshy AI | 3D asset generation | Pay-per-model |
| **GPU Inference** | NVIDIA Build | AI model serving | Pay-per-use |
| **RPC Nodes** | Alchemy | Blockchain | $20-50/mo |
| **Cloud (GCP)** | Google Cloud | Vertex AI, Cloud Run, GKE | Pay-per-use |
| **Cloud (AWS)** | Amazon Web Services | EC2, EKS, S3, Lambda | Pay-per-use |
| **Cloud (Azure)** | Microsoft Azure | AKS, App Service, Cosmos DB | Pay-per-use |

### CI/CD Pipeline

**GitHub Actions Workflows:**

```yaml
Trigger: Push to main / PR
├─ Lint (ESLint, Pylint, Solidity)
├─ Unit Tests (Jest, Pytest, Hardhat)
├─ Integration Tests
├─ Security Scan (SAST, dependency check)
├─ Build Docker image
├─ Push to Docker Hub
└─ Deploy to Railway (auto on success)
```

**Status:** ✅ 100% workflows passing

### Containerization

```dockerfile
# Base image: Node.js 22-alpine
FROM node:22-alpine

# Install dependencies
RUN npm ci --only=production

# Expose ports
EXPOSE 3000 8081

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
  CMD node healthcheck.js
```

**Docker Compose** (local development):
```yaml
services:
  server:
    image: devil-revenant-server:latest
    ports: ["3000:3000"]
    environment: !include .env.development
  
  mongodb:
    image: mongo:7
    volumes: ["mongo_data:/data/db"]
  
  redis:
    image: redis:7-alpine
    volumes: ["redis_data:/data"]
```

---

## 📊 Performance Metrics

### Server Benchmarks

| Metric | Target | Actual |
|--------|--------|--------|
| **Concurrent Players** | 1,000 | ✅ Tested to 500 |
| **Message Latency** | <50ms | ✅ ~30ms avg |
| **Database Query** | <100ms | ✅ ~45ms avg |
| **Uptime (Monthly)** | 99.5% | ✅ 99.7% |

### Client Performance

| Platform | FPS | Memory | Load Time |
|----------|-----|--------|-----------|
| **PC (1080p)** | 60 | 200MB | 3s |
| **WebGL** | 30 | 150MB | 5s |
| **Mobile (future)** | 30 | 100MB | 4s |

---

## 🔐 Security Practices

- ✅ HTTPS/TLS everywhere
- ✅ JWT token rotation
- ✅ Input validation (Joi)
- ✅ Rate limiting (Redis)
- ✅ CORS restriction
- ✅ SQL injection prevention (Mongoose schema)
- ✅ Secrets management (environment variables)
- ✅ Regular dependency updates (Dependabot)

---

## 📚 Technology Choices Rationale

| Technology | Why Chosen | Alternative Rejected |
|-----------|-----------|----------------------|
| **Unity** | Mature, cross-platform, asset store | UE5 (overkill), Godot (community) |
| **Node.js** | JavaScript full-stack, Socket.IO | Go (learning curve), Java (complex) |
| **MongoDB** | Flexible schema, Atlas hosting | PostgreSQL (rigid), Firebase (limited) |
| **Redis** | Sub-ms latency, pub/sub support | Memcached (simpler), DynamoDB (vendor lock) |
| **Python AI** | Rich ML libraries, OpenAI integration | Java (verbose), Rust (niche) |
| **Solidity** | Industry standard for EVM | Vyper (niche), Move (Aptos only) |
| **Railway** | Simple deploy, auto-scaling | Heroku (expensive) |
| **Multi-Cloud** | GCP + AWS + Azure ready; avoid vendor lock-in | Single-cloud dependency |

---

### ☁️ Multi-Cloud Strategy

The platform is designed for **cloud-agnostic deployment** across major providers:

| Provider | Services Used | Purpose |
|----------|--------------|----------|
| **Google Cloud (GCP)** | Vertex AI, Cloud Run, GKE, Cloud Storage | AI/ML inference, container orchestration |
| **Amazon Web Services (AWS)** | EC2, EKS, S3, Lambda, CloudFront | Compute, storage, CDN, serverless |
| **Microsoft Azure** | AKS, App Service, Cosmos DB, Azure AI | Kubernetes, PaaS hosting, AI services |
| **Railway** | App hosting | Current production (Node.js server) |
| **MongoDB Atlas** | Multi-cloud clusters | Database (runs on GCP/AWS/Azure) |
| **Redis Cloud** | Multi-cloud caching | Cache layer (multi-region) |

**Benefits:**
- 🔄 No vendor lock-in — containerized workloads portable across all 3 clouds
- 🌍 Multi-region availability (GCP: EU, AWS: US, Azure: Asia)
- 💰 Cost optimization — best-of-breed services from each provider
- 🛡️ Disaster recovery — cross-cloud failover capability

---

*Technology Stack Last Updated: May 10, 2026*
