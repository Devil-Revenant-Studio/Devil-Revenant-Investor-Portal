# 📋 Devil Revenant MMO - Project Manifest

**Version:** 1.1.2 – Hybrid World Demo  
**Release Date:** May 16, 2026  
**Status:** Active Development → Alpha (June 30, 2026)  
**Organization:** Devil-Revenant-Studio

---

## 🎯 Project Vision

**Devil Revenant MMO** is a quad-world blockchain-integrated massively multiplayer role-playing game combining traditional gameplay with Web3 economics, AI-driven NPC systems, and cross-platform support.

### Canonical Worlds
1. **Angel Realm** – Sacred territories, holy magic, celestial NPCs
2. **Demon Realm** – Infernal domains, dark magic, demonic NPCs
3. **Human Realm** – Mortal plane, balanced gameplay, human NPCs
4. **Hybrid Realm** – Cross-faction liminal space, mixed entities

---

## 🏗️ Technical Stack

### Frontend
- **Unity 2021.3.45f LTS** – 3D game engine (C#)
- **React 18 + Vite** – Web/companion app (`Devil-Revenant-App`)
- **Tailwind CSS** – UI styling

### Backend
- **Node.js v22.20.0** – MMO server (Socket.IO, Express)
- **Python 3.13.8** – AI engine (NPC behavior, GPT-4/Gemini)
- **MongoDB Atlas** – Player/NPC persistence
- **Redis Cloud** – Position caching, cross-world events

### Blockchain
- **Solidity 0.8.20** – Smart contracts (DOT/SHIB marketplace)
- **Polkadot** – Primary blockchain integration
- **Hardhat** – Development & testing

### Cloud & AI
- **Railway** – Production hosting (lessdevilrevenantmmorpg-production.up.railway.app)
- **Google Vertex AI Gemini 2.5** – NPC dialogue generation
- **OpenAI GPT-4** – Backup NPC dialogue
- **Meshy AI** – 3D asset generation
- **NVIDIA Build** – GPU inference

---

## 📦 Repository Structure

```
Devil-Revenant-MMO-RPG/
├── Server/                    # Node.js MMO backend
│   ├── managers/             # WorldManager, CombatManager, CrossWorldEventManager
│   ├── middleware/           # JWT + Ory authentication
│   ├── models/               # Mongoose schemas (Player, NPC, Subscription)
│   ├── services/             # stripeService, aiService, blockchainProxy
│   ├── utils/                # aiSchema validation, worldBridge
│   ├── combat/               # serverCombat.js (authoritative damage)
│   ├── database/             # CharacterDatabase.json (30 NPCs)
│   ├── server.js             # Entry point
│   └── .env.production       # Railway secrets
│
├── UnityProject/             # C# game client
│   ├── Assets/Scripts/
│   │   ├── AI/               # NPCDialogueController, HybridNPC
│   │   ├── WorldSystem/      # MultiWorldManager, WorldType enum
│   │   ├── Networking/       # SocketIOManager, WebSocketManager
│   │   └── Blockchain/       # BlockchainProxy
│   ├── Scenes/               # Angel, Demon, Human, Hybrid worlds
│   └── ProjectSettings/
│
├── blockchain/               # Solidity smart contracts
│   ├── contracts/
│   │   ├── DOTMarketplace.sol
│   │   ├── RevenantNFT.sol
│   │   └── PlayerRewards.sol
│   ├── DEPLOYMENT_GUIDE_SEPOLIA.md
│   └── hardhat.config.js
│
├── python-servers/           # AI engine
│   ├── ai-core/
│   │   ├── npc-behavior.py   # NPCBehaviorEngine (28 characters)
│   │   └── dialogue.py       # Gemini 2.5 integration
│   ├── mcp-orchestrator/     # MCP server orchestration
│   └── requirements.txt
│
└── website/                  # Marketing website
    ├── index.html
    ├── characters.html       # Character gallery
    └── download.html
```

---

## 🔐 Authentication Architecture (Dual Layer)

### JWT Authentication (Game Client)
- **Used by:** Unity game client
- **Middleware:** `middleware/auth.js` → `requireAuth`
- **Token:** Bearer token in Authorization header
- **Flow:** `/api/auth/[provider]/callback` → JWT token issued

### Ory Authentication (Web Client)
- **Used by:** React web app, OAuth login
- **Middleware:** `middleware/ory-auth.js` → `requireOrySession`
- **Token:** Ory session cookie/token
- **Flow:** Ory portal `/login` → redirect to `/callback` → session established
- **Ory Project Slug:** `affectionate-elbakyan-cxn3civgm7`

### OAuth Providers (All Platforms)
| Provider | Callback | Status |
|----------|----------|--------|
| Discord | `/api/auth/discord/callback` | ✅ HTTP 302 (May 16) |
| Google | `/api/auth/google/callback` | ✅ HTTP 302 (May 16) |
| GitHub | `/api/auth/github/callback` | ✅ HTTP 302 (May 16) |

---

## 💰 Subscription & Payments

### Stripe AI Quota System
Controls **NPC dialogue limits** (not in-game items):

| Tier | Price | Daily | Monthly |
|------|-------|-------|---------|
| Free | $0 | 10 | 300 |
| Basic | $4.99 | 50 | 1,500 |
| Premium | $14.99 | 200 | 6,000 |
| VIP | $29.99 | ∞ | ∞ |

**Routes:**
- `POST /api/subscription/create-payment-intent` → Stripe.js form
- `POST /api/subscription/upgrade` → Payment confirmation
- `POST /api/subscription/webhook` → Stripe events (raw body!)
- `GET /api/subscription/usage` → Remaining dialogues

**Blockchain payments:** (TODO – DOT/SHIB secondary method)

---

## 🌐 Cross-World Event System

### CrossWorldEventManager
- **File:** `Server/managers/CrossWorldEventManager.js`
- **Purpose:** Broadcast events across all 4 worlds
- **Event History:** Max 50 per world

**Event Propagation Rules:**
```
Source: Angel    → Broadcasts to: Demon, Hybrid
Source: Demon    → Broadcasts to: Angel, Hybrid
Source: Hybrid   → Broadcasts to: Angel, Demon
Source: Human    → Broadcasts to: Angel, Demon, Hybrid
```

**Example Event Types:**
- `boss_killed` – All 4 worlds notified
- `faction_war` – Cross-world conflict
- `world_event` – Special occurrences

**NPC AI Integration:**
```python
# Python AI engine requests cross-world context
context = crossWorldManager.getCrossWorldKnowledge("angel", "demon")
# Returns: { recentEvents: [...], playerCount, summary }
```

---

## ⚔️ Server-Authoritative Combat

**Rule:** All damage calculated server-side in `Server/combat/serverCombat.js`

```javascript
// ✅ CORRECT
const result = combatManager.processAttack(attacker, { targetId }, callback);
// Server validates: same world+zone, range ≤ 4m, faction bonuses

// ❌ WRONG
client.emit("damage", { damage: 999 }); // Client never sends damage values
```

**Constants:** `WEAPON_DAMAGE`, `ARMOR_REDUCTION` defined in `serverCombat.js` only

---

## 🤖 NPC AI System (28 Characters)

### Architecture
- **Python Engine:** `ai-core/npc-behavior.py` loads `CharacterDatabase.json`
- **C# Client:** `DevilRevenant.AI` handles rendering + UI
- **Integration:** SocketIOManager emits `ai:dialogue:request` events

### Validation Pipeline
1. Client sends `ai:dialogue:request` via Socket.IO
2. `aiSchema.js` validates event type (must start `ai:`)
3. `validateBridgePayload()` checks cross-world constraints
4. Python AI engine processes with Gemini 2.5
5. Response emitted back to client

---

## 🚀 Production Deployment (Railway)

### Current Status (May 16, 2026)
- **Domain:** `lessdevilrevenantmmorpg-production.up.railway.app`
- **Health:** `/health` endpoint responding ✅
- **Database:** MongoDB Atlas connected ✅
- **Cache:** Redis Cloud connected ✅
- **OAuth:** Discord/Google/GitHub configured ✅

### Environment Variables
```
DISCORD_CALLBACK_URL=https://lessdevilrevenantmmorpg-production.up.railway.app/api/auth/discord/callback
GOOGLE_CALLBACK_URL=https://lessdevilrevenantmmorpg-production.up.railway.app/api/auth/google/callback
GITHUB_CALLBACK_URL=https://lessdevilrevenantmmorpg-production.up.railway.app/api/auth/github/callback
ORY_SDK_URL=https://affectionate-elbakyan-cxn3civgm7.projects.oryapis.com
STRIPE_SECRET_KEY=sk_test_...
MONGODB_URI=mongodb+srv://...
REDIS_URL=redis://...
```

---

## 📅 Development Timeline

| Phase | Target | Status |
|-------|--------|--------|
| **Demo** | End May 2026 | 🟡 In Progress |
| **Alpha 1.1.2** | June 30, 2026 | 🟡 In Progress (Unity ~17% complete) |
| **Public Beta** | Q3 2026 | 🔴 Planned |
| **Full Launch** | Q4 2026 | 🔴 Planned |

---

## 📊 Project Statistics

- **Quad Worlds:** 4 realms
- **NPCs:** 28 AI characters
- **Deployment:** Railway + multi-cloud (AWS, Azure, GCP)
- **Smart Contracts:** 3 main (DOT Marketplace, NFT, Rewards)
- **Development Teams:** Studio + external partners
- **API Endpoints:** 50+ REST + Socket.IO namespaces

---

## ✅ Recent Milestones (May 2026)

✅ **OAuth Endpoint Configuration** (May 16)
- Discord, Google, GitHub callbacks now returning HTTP 302
- Railway domain corrected to `lessdevilrevenantmmorpg-production.up.railway.app`
- Redeploy completed, all auth providers functional

✅ **Dual Authentication Layer** (May 2026)
- JWT for game clients (Unity)
- Ory sessions for web clients (React)
- Both running in production

✅ **Stripe Subscription System** (May 2026)
- Payment intents for custom Stripe forms
- Checkout sessions for redirect flow
- Webhook handling active

---

## 🔗 Related Repositories

| Repo | Purpose |
|------|---------|
| `Devil-Revenant-App` | React/Vite frontend (THIS PROJECT SEPARATE) |
| `Devil-Revenant-Investor-Portal` | Investor-facing documentation |
| `devil-revenant-orchestrator` | Multi-service deployment orchestration |
| `Devil-Revenant-Rise-of-the-Hero` | Anime series (SEPARATE PROJECT) |
| `devil-revenant-shared` | Shared types & utilities |
| `devil-revenant-infra` | IaC (Terraform/Bicep) |
| `devil-revenant-docs` | Technical documentation |

---

**Last Updated:** May 16, 2026  
**Maintainers:** Devil Revenant Studio Dev Team
