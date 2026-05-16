# 🔥 Devil Revenant Studio — Investor Portfolio

**Status:** Alpha 1.1.2 — Active Development  
**Demo Target:** End of May 2026 | **Alpha Target:** June 30, 2026  
**License:** MIT | **Organization:** [Devil-Revenant-Studio](https://github.com/Devil-Revenant-Studio)

---

## 📊 Studio Overview

**Devil Revenant Studio** develops **advanced blockchain MMO RPG ecosystems** with AI-driven NPCs, cross-platform deployment, and cryptocurrency integration.

### 🎯 Current Portfolio (5 Platforms)

| Platform | Status | Progress | Tech Stack | Live |
| -------- | ------ | -------- | --------- | ---- |
| **Devil Revenant MMO — Server** | 🟢 Production | **92%** | Node.js v22 + Express + Socket.IO + MongoDB Atlas + Redis | [Railway](https://lessdevilrevenantmmorpg-production.up.railway.app) |
| **Devil Revenant MMO — Unity Client** | 🔴 Alpha 1.1.2 | **~35%** | Unity 2021.3.45f2 LTS · 52 C# scripts · WebGL | In Development |
| **Hybrid World Demo** | 🟢 Playable | **~85%** | Unity WebGL Build | [WebGL Demo](#-hybrid-world-demo) |
| **Devil Revenant App** (Web Frontend) | 🟡 Beta | **75%** | React 18 + Vite + Tailwind + Base44 + Polkadot | [Netlify](https://devil-revenant-app.netlify.app) |
| **Python AI Engine** | 🟢 Production | **90%** | FastAPI + Vertex AI Gemini 2.5 + NVIDIA NIM | [Railway](https://python-ai-production-e0cd.up.railway.app) |
| **Blockchain (DOT/NFT)** | 🟢 Deployed | **85%** | Solidity 0.8.20 · 5 contracts · Sepolia testnet | [Etherscan](#%EF%B8%8F-blockchain--85-complete-sepolia-deployed) |
| **Website** | 🟢 Live | **95%** | HTML/CSS/JS · 23 pages · Multi-language | [Netlify](https://devilrevenant.netlify.app) |
| **Revenant Vault** | 🟡 Beta | **40%** | React + Base44 Identity/Wallet | In Development |
| **Rise of the Hero** (Anime) | 🟡 Pre-Production | **5%** | Unreal Engine + 3D Animation | Q3 2026 |

---

## 🎮 Hybrid World Demo

> **Playable WebGL demo** of the Hybrid realm — browser-accessible, no install required.

- ✅ Hybrid World environment fully generated
- ✅ AI NPC dialogue system (30 characters with cross-world awareness)
- ✅ Server-authoritative combat with real-time sync
- ✅ UI: Health/Mana/Stamina bars, Quest Tracker, Dialogue Window, Skill Bar
- ✅ WebGL build ready for browser play

---

## 🌍 Quad-World Blockchain MMO RPG

A **massively multiplayer online RPG** combining 4 interconnected realms with AI-driven NPCs, real-time combat, and Polkadot (DOT) cryptocurrency integration.

### Core Features

- 🌍 **4 Interconnected Worlds**: Angel, Demon, Human, Hybrid
- 🤖 **30 AI-Driven NPC Characters** with dynamic dialogue & cross-world awareness
- 🎮 **12 Playable Classes** × 4 Races = 48 unique character combinations
- ⚔️ **Real-time Combat**: PvE + PvP with server-authoritative validation
- 💱 **DOT Marketplace**: In-game trading using Polkadot DOT tokens
- 📖 **Epic Storyline**: 3 seasons, 18 episodes with branching narratives
- 🛠️ **Crafting & Trading**: Player-driven economy
- 🤝 **Guild System**: Cross-faction alliances
- 🌐 **Cross-World Events**: Server-wide boss raids

### Key NPCs (30 Total)

**Protagonists:** Kaelin (Hybrid Hero), Raphael (Angel General), Nyx Umbra (Balance Entity)  
**Antagonist:** Verschlinger (Chaos God)  
**Factions:** 8 Angels + 12 Demons + 5 Hybrids + 5 Humans

---

## 🏗️ Platform Details

### 🖥️ Node.js Server — 92% Complete

| Component | Count | Status |
| --------- | ----- | ------ |
| Manager Classes | 7 | ✅ Complete |
| API Routes | 8 | ✅ Complete |
| Data Models | 7 | ✅ Complete |
| Auth Methods | 6 | ✅ Multi-provider |

**Managers:** ChatManager · CombatManager · CrossWorldEventManager · DemoManager · PlayerManager · QuestManager · WorldManager

**Implemented Features:**

- ✅ Multi-auth: JWT, Ory, Entra ID, Discord, Google, GitHub OAuth
- ✅ Server-authoritative combat system
- ✅ AI NPC management + cross-world events
- ✅ Stripe subscription system (4 tiers)
- ✅ Blockchain DOT reward integration
- ✅ WebSocket rate limiting + Prometheus metrics
- ✅ Swagger API documentation
- ✅ MongoDB Atlas persistence + Redis Cloud caching

**Deployment:** 🟢 Railway — `https://lessdevilrevenantmmorpg-production.up.railway.app`

---

### 🎮 Unity Client — ~35% Complete (52 C# Scripts)

| System | Scripts | Status |
| ------ | ------- | ------ |
| World System | 5 | ✅ MultiWorldManager + 4 generators |
| Combat | 4 | ✅ Server-synced CombatManager |
| AI NPCs | 3 | ✅ NPCDialogueController + HybridNPC |
| UI Components | 11 | ✅ Full HUD framework |
| Blockchain | 5 | ✅ Wallet + NFT + DOT integration |
| Networking | 3 | ✅ Socket.IO + WebSocket |
| Quests | 2 | ✅ Dynamic AI-driven quests |
| Testing | 2 | ✅ DevilRevenantTestSuite |

**World Generators:** AngelicWorldGenerator · DemonicWorldGenerator · HumanWorldGenerator · HybridWorldGenerator

---

### 🤖 Python AI Engine — 90% Complete

| Component | Details | Status |
| --------- | ------- | ------ |
| NPC Characters | 30 distinct personalities | ✅ Live |
| AI Engines | 6 modules | ✅ Active |
| LLM Integrations | 3 providers | ✅ Multi-fallback |

**AI Modules:** npc-behavior.py · dialogue-engine.py · quest-generator.py · npc-personality-learning.py · ai-api.py · main.py

**LLM Stack:**

- 🥇 **Google Vertex AI Gemini 2.5** — Primary (99% cheaper than GPT-4)
- 🥈 **OpenAI GPT-4** — Fallback
- 🥉 **NVIDIA NIM** — Local personality learning inference

**Deployment:** 🟢 Railway — `https://python-ai-production-e0cd.up.railway.app`

---

### ⛓️ Blockchain — 85% Complete (Sepolia Deployed)

| Contract | Address | Status |
| -------- | ------- | ------ |
| **DOT Token** | `0x86bB91055B92901F3eed66eF405787cef3CE408c` | ✅ Deployed |
| **NFT (ERC-721)** | `0xCCA369bF6E56F6d8D4819f0FD94D088E1E11821B` | ✅ Deployed |
| **DOT Marketplace** | `0x9a97106fb27EB3933b2378F22F3047F51cD29d66` | ✅ Deployed |
| **DOT Staking** | `0x4b4263C7d5042D90F111c037a5bBdB62df4be116` | ✅ Deployed |
| **SubscriptionPayment** | Sepolia | ✅ Deployed |

**Test Coverage:** 4 test suites (DOTMarketplace · DOTStaking · DevilRevenantNFT · SubscriptionPayment)  
**Next:** Security audit → Mainnet deployment

---

### 🖥️ Devil Revenant App — 75% Complete

| Component | Count | Status |
| --------- | ----- | ------ |
| React Components | 127+ | ✅ Built |
| Pages | 23+ | ✅ Implemented |
| UI Library | 50+ Radix UI | ✅ Complete |

**Pages:** Landing · Dashboard · Characters · About · Contact · Download · Events · FAQ · Guilds · Impressum · Leaderboard · Music · Play (WebGL embed) · Press · Privacy · Roadmap · Shop · Anime · and more

**Integrations:** Base44 SDK · Azure MSAL Auth · Polkadot API · Stripe Payments

---

### 🌐 Website — 95% Complete

- 23 HTML pages · Multi-language support · SEO optimized
- OAuth integration · Docker-ready · GCP App Engine compatible
- **Deployment:** 🟢 Netlify (Live)

---

## 🏗️ Technical Architecture

### AI & ML Stack

- **Google Vertex AI Gemini 2.5** (primary NPC dialogue — 99% cheaper than GPT-4)
- **Meshy AI** (automated 3D model/asset generation)
- **NVIDIA Build** (GPU-accelerated AI inference)
- **OpenAI GPT-4** (fallback NPC dialogue)

### Blockchain

- **Polkadot DOT** (primary token)
- **Sepolia Testnet** — 5 contracts deployed (May 14, 2026)
- **Ethereum Mainnet** (post-audit)
- **Solidity 0.8.20** (auditable contracts)

### Cloud Infrastructure

- **Google Cloud Platform (GCP)** — Vertex AI, Cloud Run, GKE
- **Amazon Web Services (AWS)** — EC2, EKS, S3, Lambda, CloudFront
- **Microsoft Azure** — AKS, App Service, Cosmos DB, Azure AI
- **Railway.app** — Current production hosting (Server + AI Engine)
- **Netlify** — Website + React App hosting
- **Docker** — Cloud-agnostic containerization

---

## 💰 Business Model

### Revenue Streams

1. **AI Subscription Tiers** (Stripe)
   - Free: 10 dialogue/day, 300/month
   - Basic: $4.99/mo → 50/day, 1,500/month
   - Premium: $14.99/mo → 200/day, 6,000/month
   - VIP: $29.99/mo → Unlimited

2. **DOT Marketplace** (Blockchain)
   - In-game item trading (5% platform fee)
   - NFT skins & unique weapons
   - Staking rewards

3. **Guild Sponsorships** (Future)
   - Premium guild perks
   - Ad placements
   - Event hosting

---

## 📈 Development Timeline

| Phase | Timeline | Deliverable | Status |
| ----- | -------- | ----------- | ------ |
| **Alpha 1.1.2** | May–June 2026 | Hybrid World Demo + Combat | 🔴 Active |
| **Alpha 1.2.0** | July 2026 | All 4 Worlds + Quest System | 🟡 Planned |
| **Beta 1.0.0** | Aug–Sep 2026 | Polished gameplay + Balance | 🟡 Planned |
| **Production 1.0** | Oct 2026 | Full launch + DOT support | ⏳ Roadmap |

---

## 🚀 Live Deployments

| Service | Platform | URL | Status |
| ------- | -------- | --- | ------ |
| MMO Server | Railway | `lessdevilrevenantmmorpg-production.up.railway.app` | 🟢 Online |
| Python AI Engine | Railway | `python-ai-production-e0cd.up.railway.app` | 🟢 Online |
| Website | Netlify | `devilrevenant.netlify.app` | 🟢 Online |
| React App | Netlify | `devil-revenant-app.netlify.app` | 🟡 Beta |
| MongoDB Atlas | Cloud | Atlas Cluster | 🟢 Online |
| Redis Cloud | Cloud | Redis Instance | 🟢 Online |
| Blockchain | Sepolia | 5 contracts deployed | 🟢 Deployed |

📋 See [DEPLOYMENT-STATUS.md](DEPLOYMENT-STATUS.md) for full details.

---

## 📊 Metrics & KPIs

| Metric | Value |
| ------ | ----- |
| NPC AI Characters | 30 with dynamic dialogue |
| Unity C# Scripts | 52 |
| React Components | 127+ |
| Smart Contracts Deployed | 5 (Sepolia) |
| API Routes | 8 |
| Auth Providers | 6 (JWT, Ory, Entra, Discord, Google, GitHub) |
| Website Pages | 23 |
| Server Health | A- (88/100) |
| Production Uptime | 99.5% (Railway) |
| Combat Latency | <50ms (Socket.IO) |
| AI Cost Savings | 99% vs GPT-4 (Vertex AI Gemini 2.5) |

---

## 🔗 Quick Links

- 📖 [Full Portfolio](PORTFOLIO.md)
- 🏗️ [Architecture & Systems](ARCHITECTURE-DIAGRAMS.md)
- 🛠️ [Technology Stack](TECHNOLOGY.md)
- 📅 [Development Roadmap](ROADMAP.md)
- ✅ [Deployment Status](DEPLOYMENT-STATUS.md)
- 📦 [GitHub Organization](https://github.com/Devil-Revenant-Studio)

---

## 👥 Team

**Founder & Lead Developer:** Martin Beständig ([@Reisink2](https://github.com/Reisink2))  
**Organization:** [Devil-Revenant-Studio](https://github.com/Devil-Revenant-Studio)

---

## 📝 License

All projects are licensed under the **MIT License** — open-source with commercial support available.

---

**For investor inquiries:** Contact via [GitHub Organization](https://github.com/Devil-Revenant-Studio) or email.

---

**Last Updated:** May 15, 2026 | Alpha 1.1.2 Status
