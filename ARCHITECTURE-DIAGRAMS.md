# 🏗️ Architecture & System Diagrams

Complete visual representation of Devil Revenant Studio's technical infrastructure.

---

## 1. High-Level System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    DEVIL REVENANT ECOSYSTEM                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  CLIENT LAYER (Presentation)                                  │
│  ┌─────────────────┬──────────────┬─────────────┐              │
│  │  Unity WebGL    │  React App   │  Mobile App │              │
│  │  (Browser)      │  (Dashboard) │  (iOS/Andr) │              │
│  └────────┬────────┴──────┬───────┴────────┬────┘              │
│           │                │                │                   │
│           └────────────────┼────────────────┘                   │
│                            │                                    │
│  API GATEWAY LAYER                                             │
│  ┌─────────────────────────▼──────────────────────┐            │
│  │         HTTPS/WebSocket (TLS 1.3)             │            │
│  │      Route to appropriate service             │            │
│  └─────┬──────────────┬──────────────┬──────────┘             │
│        │              │              │                        │
│  APPLICATION LAYER (Business Logic)                           │
│  ┌──────▼────┐  ┌───▼────┐  ┌────▼─────┐  ┌─────▼───┐      │
│  │ API Server│  │ Socket │  │   AI     │  │Blockchain
│  │(REST API) │  │ Server │  │ Worker   │  │Proxy    │      │
│  │(Express)  │  │(Socket)│  │(Python)  │  │(Web3.js)│      │
│  └──────┬────┘  └───┬────┘  └────┬─────┘  └─────┬───┘      │
│         │           │            │              │           │
│  DATA LAYER (Persistence)                                    │
│  ┌──────▼─────┐  ┌─────▼──┐  ┌──▼──────┐  ┌──▼─────────┐   │
│  │  MongoDB   │  │ Redis  │  │ Solidity│  │  External  │   │
│  │   Atlas    │  │ Cloud  │  │Contracts│  │   APIs     │   │
│  └────────────┘  └────────┘  └─────────┘  └────────────┘   │
│                                                              │
│  EXTERNAL SERVICES                                           │
│  ┌──────────────┬──────────────┬──────────────┐             │
│  │   Vertex AI  │    Stripe    │   Alchemy    │             │
│  │  Gemini 2.5  │  Payments    │  RPC Node    │             │
│  └──────────────┴──────────────┴──────────────┘             │
│  ┌──────────────┬──────────────┬──────────────┐             │
│  │  Meshy AI    │ NVIDIA Build │   OpenAI     │             │
│  │  3D Assets   │ GPU Inference│  GPT-4 (FB)  │             │
│  └──────────────┴──────────────┴──────────────┘             │
│                                                              │
│  CLOUD INFRASTRUCTURE (Multi-Cloud Ready)                    │
│  ┌──────────────┬──────────────┬──────────────┐             │
│  │ Google Cloud │     AWS      │   Azure      │             │
│  │ Vertex AI    │  EC2/EKS/S3  │  AKS/App Svc │             │
│  │ Cloud Run    │  Lambda/CDN  │  Cosmos DB   │             │
│  │ GKE          │  CloudFront  │  Azure AI    │             │
│  └──────────────┴──────────────┴──────────────┘             │
│                                                              │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. Server Architecture (Node.js)

```
┌─────────────────────────────────────────────────────────┐
│             NODE.JS MULTIPLAYER SERVER                  │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  EXPRESS MIDDLEWARE STACK                             │
│  ┌─────────────────────────────────────────┐          │
│  │ 1. CORS (cross-origin requests)        │          │
│  │ 2. JWT Authentication (Bearer tokens)  │          │
│  │ 3. Request Validation (Joi schemas)    │          │
│  │ 4. Rate Limiting (Redis-backed)        │          │
│  │ 5. Error Handling (centralized)        │          │
│  └─────────────────────────────────────────┘          │
│                    ↓                                    │
│  REST ROUTES                                           │
│  ├─ GET /health              → Server status          │
│  ├─ POST /login              → Authentication         │
│  ├─ GET /api/profile         → Player data            │
│  ├─ POST /api/world/switch   → World transition       │
│  ├─ POST /api/combat/attack  → Combat action          │
│  └─ POST /api/subscription/* → Payment endpoints      │
│                    ↓                                    │
│  SOCKET.IO REAL-TIME EVENTS                           │
│  ├─ player:move             → Position update        │
│  ├─ player:joined           → Player enters world    │
│  ├─ player:left             → Player leaves          │
│  ├─ ai:dialogue:request     → NPC dialogue query    │
│  ├─ combat:attack           → Combat action          │
│  ├─ world:switch            → World transition       │
│  └─ cross-world:event       → Multi-realm broadcast  │
│                    ↓                                    │
│  MANAGER CLASSES (Business Logic)                     │
│  ┌─────────────┬─────────┬──────────────┬──────────┐  │
│  │ WorldManager│ Combat  │ NPCManager   │ Quest    │  │
│  │             │Manager  │              │Manager   │  │
│  │ · Switch    │         │ · Spawn NPC  │          │  │
│  │ · Zones     │ · Damage│ · Dialogue   │ · Gen    │  │
│  │ · Events    │ · Validation
          │ · AI State │ · Track │  │
│  └─────────────┴─────────┴──────────────┴──────────┘  │
│                    ↓                                    │
│  DATA LAYER (Mongoose ODM)                            │
│  └─────────────────────────────────────────┘          │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 3. Database Schema (MongoDB)

```
┌─ PLAYERS Collection
│  ├─ userId (PK)
│  ├─ username
│  ├─ email
│  ├─ currentWorld (Angel|Demon|Hybrid|Human)
│  ├─ currentZone (zone_id)
│  ├─ stats {health, mana, strength, ...}
│  ├─ inventory [{itemId, quantity, ...}]
│  ├─ subscriptionTier (free|basic|premium|vip)
│  ├─ subscriptionExpiry (ISO datetime)
│  ├─ faction (Angel|Demon|Human)
│  └─ createdAt

├─ CHARACTERS Collection (30 NPCs)
│  ├─ npcId (PK)
│  ├─ name
│  ├─ world (Angel|Demon|Hybrid|Human)
│  ├─ zone
│  ├─ personality {traits, likes, dislikes}
│  ├─ dialogue {greeting, quest_offer, ...}
│  ├─ stats {level, hp, mana, ...}
│  └─ aiPersona (structured prompt for GPT-4)

├─ INVENTORY Collection
│  ├─ playerId (FK → PLAYERS)
│  ├─ items [{itemId, name, rarity, ...}]
│  ├─ equipment {head, chest, legs, feet, ...}
│  └─ lastUpdated

├─ EVENTS Collection (Cross-world history)
│  ├─ eventId (PK)
│  ├─ sourceWorld
│  ├─ type (boss_killed, item_found, ...)
│  ├─ data {details}
│  ├─ timestamp
│  └─ ttl: 86400 (auto-expire after 24h)

└─ SUBSCRIPTIONS Collection
   ├─ subscriptionId (PK)
   ├─ playerId (FK → PLAYERS)
   ├─ tier (free|basic|premium|vip)
   ├─ dialoguesUsedToday
   ├─ dialoguesUsedThisMonth
   ├─ stripeCustomerId
   ├─ renewalDate
   └─ createdAt
```

---

## 4. AI NPC Pipeline

```
┌──────────────────────────────────────────────────────┐
│        PLAYER → NPC DIALOGUE FLOW                    │
├──────────────────────────────────────────────────────┤
│                                                      │
│  1. PLAYER SENDS QUERY (WebGL Client)              │
│  ┌─────────────────────────────────────┐           │
│  │ Message: "What do you know?"        │           │
│  │ NPC ID: kaelin_001                  │           │
│  │ Player ID: player_123               │           │
│  └────────────────┬────────────────────┘           │
│                   │                                 │
│  2. SOCKET.IO EVENT (Node.js Server)               │
│  ┌──────────────────────────────────┐              │
│  │ socket.on("ai:dialogue:request") │              │
│  │ → Validate with aiSchema.js      │              │
│  │ → Check subscription quota       │              │
│  │ → Emit to Python worker          │              │
│  └──────────────────┬───────────────┘              │
│                     │                              │
│  3. PYTHON AI ENGINE (FastAPI)                    │
│  ┌──────────────────────────────────┐              │
│  │ Endpoint: /npc/dialogue          │              │
│  │ Input: {npcId, playerMessage}    │              │
│  │ Load: CharacterDatabase.json     │              │
│  │ Build: Context-aware prompt      │              │
│  │ Call: OpenAI GPT-4 API           │              │
│  └──────────────────┬───────────────┘              │
│                     │                              │
│  4. OPENAI GPT-4 (External API)                   │
│  ┌──────────────────────────────────┐              │
│  │ System Prompt: Kaelin's persona  │              │
│  │ Context: World state, NPC memory │              │
│  │ User Query: Player's message     │              │
│  │ Response: Generated dialogue     │              │
│  └──────────────────┬───────────────┘              │
│                     │                              │
│  5. PYTHON RESPONSE (Cache result)                │
│  ┌──────────────────────────────────┐              │
│  │ Send response back to Node.js    │              │
│  │ Cache in Redis (30 min TTL)      │              │
│  │ Decrement subscription quota     │              │
│  └──────────────────┬───────────────┘              │
│                     │                              │
│  6. SOCKET.IO EMIT (Node.js → Client)             │
│  ┌──────────────────────────────────┐              │
│  │ Event: "ai:dialogue:response"    │              │
│  │ Content: NPC's reply             │              │
│  │ Broadcast: To all players in zone
          │              │
│  └──────────────────┬───────────────┘              │
│                     │                              │
│  7. UNITY RENDERS (WebGL Client)                  │
│  ┌──────────────────────────────────┐              │
│  │ Display NPC response in UI       │              │
│  │ Play dialogue animation          │              │
│  │ Update NPC mood/state            │              │
│  └──────────────────────────────────┘              │
│                                                      │
└──────────────────────────────────────────────────────┘
```

---

## 5. Blockchain Integration Flow

```
┌─────────────────────────────────────────────────────────┐
│        PLAYER PURCHASE ITEM (DOT MARKETPLACE)          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1. PLAYER INITIATES BUY (Unity Client)               │
│  ┌───────────────────────────────────┐                │
│  │ Button: "Buy Item for 10 DOT"    │                │
│  │ Sends: {itemId, amount, playerId}│                │
│  └─────────────────┬─────────────────┘                │
│                    │                                   │
│  2. BLOCKCHAIN PROXY (Node.js)                        │
│  ┌───────────────────────────────────┐                │
│  │ Route: POST /api/blockchain/*    │                │
│  │ Validate: Player has wallet      │                │
│  │ Check: Sufficient balance        │                │
│  │ Create: Transaction object       │                │
│  └─────────────────┬─────────────────┘                │
│                    │                                   │
│  3. SEND TO BLOCKCHAIN (Alchemy RPC)                 │
│  ┌───────────────────────────────────┐                │
│  │ Network: Sepolia Testnet         │                │
│  │ Contract: DOTMarketplace.sol     │                │
│  │ Method: buyItem(itemId, amount) │                │
│  │ Gas Estimate: ~50K gas           │                │
│  │ Send: Signed transaction         │                │
│  └─────────────────┬─────────────────┘                │
│                    │                                   │
│  4. BLOCKCHAIN PROCESSES                              │
│  ┌───────────────────────────────────┐                │
│  │ Miners/Validators confirm        │                │
│  │ Block confirmations: 3+          │                │
│  │ Execution: Transfer DOT + Item   │                │
│  │ Event: ItemBought emitted        │                │
│  └─────────────────┬─────────────────┘                │
│                    │                                   │
│  5. MONITOR TX RECEIPT (Node.js)                      │
│  ┌───────────────────────────────────┐                │
│  │ Poll: Transaction hash status    │                │
│  │ When: Receipt confirmed          │                │
│  │ Update: MongoDB (player inventory)
          │                │
│  │ Emit: Socket.IO success event    │                │
│  └─────────────────┬─────────────────┘                │
│                    │                                   │
│  6. CONFIRM TO CLIENT (Unity)                         │
│  ┌───────────────────────────────────┐                │
│  │ Event: "blockchain:purchase:success"
│  │ Show: "10 DOT transferred!"      │                │
│  │ Update: Local inventory UI       │                │
│  └───────────────────────────────────┘                │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 6. Deployment Architecture (DevOps)

```
┌────────────────────────────────────────────────────┐
│     CI/CD PIPELINE & DEPLOYMENT FLOW               │
├────────────────────────────────────────────────────┤
│                                                    │
│  DEVELOPER COMMITS CODE                           │
│  └─────────────────┬─────────────────┘            │
│                    │ git push origin main          │
│                    ↓                               │
│  GITHUB ACTIONS TRIGGERED                         │
│  ┌──────────────────────────────────┐             │
│  │ Step 1: Lint code (2 min)       │             │
│  │ - ESLint for Node.js            │             │
│  │ - Pylint for Python             │             │
│  │ - Solium for Solidity           │             │
│  │ Action: FAIL if errors > 0      │             │
│  └──────────────────┬───────────────┘             │
│                     │                             │
│  ┌──────────────────────────────────┐             │
│  │ Step 2: Unit Tests (3 min)      │             │
│  │ - Jest (250+ tests)             │             │
│  │ - Pytest (80+ tests)            │             │
│  │ - Hardhat (50+ tests)           │             │
│  │ Action: FAIL if coverage < 80%  │             │
│  └──────────────────┬───────────────┘             │
│                     │                             │
│  ┌──────────────────────────────────┐             │
│  │ Step 3: Build Docker Image      │             │
│  │ - Base: node:22-alpine          │             │
│  │ - Copy: src/, package*.json     │             │
│  │ - Run: npm ci --production      │             │
│  │ - Tag: devil-revenant-server:   │             │
│  │        {{GIT_SHA_SHORT}}        │             │
│  └──────────────────┬───────────────┘             │
│                     │                             │
│  ┌──────────────────────────────────┐             │
│  │ Step 4: Push to Docker Hub      │             │
│  │ - Authenticate: DOCKER_TOKEN    │             │
│  │ - Push: Reisink2/devil-revenant │             │
│  │ - Tag: latest, {{DATE}}         │             │
│  └──────────────────┬───────────────┘             │
│                     │                             │
│  ┌──────────────────────────────────┐             │
│  │ Step 5: Deploy to Railway       │             │
│  │ - Trigger: Railway webhook      │             │
│  │ - Pull: Latest image from Hub   │             │
│  │ - Start: New container          │             │
│  │ - Health: Check /health route   │             │
│  │ - Duration: ~2 min              │             │
│  └──────────────────┬───────────────┘             │
│                     │                             │
│  PRODUCTION LIVE                                  │
│  └──────────────────────────────────┘             │
│                                                    │
│  ROLLBACK (if needed)                             │
│  └─ Automated: Redeploy prev version             │
│  └─ Manual: GitHub Actions re-run                │
│                                                    │
└────────────────────────────────────────────────────┘
```

---

## 7. Data Flow (Cross-World Events)

```
┌──────────────────────────────────────────────────────┐
│   CROSS-WORLD EVENT PROPAGATION                      │
├──────────────────────────────────────────────────────┤
│                                                      │
│  EVENT SOURCE (Demon World)                         │
│  ┌─────────────────────────────────┐               │
│  │ Boss Killed: "Shadow Lord"      │               │
│  │ Source World: Demon             │               │
│  │ Player: player_456              │               │
│  │ Data: {loot: sword, xp: 1000}  │               │
│  └────────────────┬────────────────┘               │
│                   │                                 │
│  BROADCAST TO OTHER WORLDS                         │
│  ├─ Angel World  → room: world:Angel              │
│  ├─ Hybrid World → room: world:Hybrid              │
│  ├─ Human World  → room: world:Human               │
│  └─ NOT Demon → room: world:Demon (already knows) │
│                   │                                 │
│  EVENT HISTORY (Redis)                             │
│  ┌─────────────────────────────────┐               │
│  │ Key: event:demon                │               │
│  │ Value: [{event}, {event}, ...]  │               │
│  │ TTL: 1 hour                     │               │
│  │ Max: 50 events per world        │               │
│  └─────────────────────────────────┘               │
│                   │                                 │
│  NPC AI AWARENESS                                   │
│  ┌─────────────────────────────────┐               │
│  │ Python AI Engine queries:      │               │
│  │ "What happened in demon realm?"│               │
│  │ Returns: Summary of events     │               │
│  │ Used in: NPC dialogue context  │               │
│  └─────────────────────────────────┘               │
│                   │                                 │
│  ALL PLAYERS INFORMED                               │
│  └─ "A powerful entity was defeated in the Demon  │
│     Realm!"                                        │
│                                                      │
└──────────────────────────────────────────────────────┘
```

---

## 8. Performance Optimization Layers

```
┌────────────────────────────────────────────────────────┐
│         CACHING & OPTIMIZATION STRATEGY                │
├────────────────────────────────────────────────────────┤
│                                                        │
│  L1: CLIENT-SIDE CACHING (Unity)                      │
│  ├─ Sprite sheets (pre-loaded)                        │
│  ├─ Audio clips (cached in RAM)                       │
│  └─ Mesh data (GPU memory)                            │
│                                                        │
│  L2: REDIS CACHING (Real-time data)                   │
│  ├─ Player positions (5s TTL)                         │
│  ├─ Room member lists (live update)                   │
│  ├─ Generated quests (30m TTL)                        │
│  └─ Event history (1h TTL)                            │
│                                                        │
│  L3: DATABASE INDEXING (MongoDB)                      │
│  ├─ _id (default)                                     │
│  ├─ userId (for lookups)                              │
│  ├─ currentWorld (for zone queries)                   │
│  └─ timestamp (for event sorting)                     │
│                                                        │
│  L4: CDN CACHING (Static assets)                      │
│  ├─ JavaScript bundles                               │
│  ├─ CSS stylesheets                                  │
│  ├─ Images & sprites                                 │
│  └─ JSON data files                                  │
│                                                        │
│  L5: API RESPONSE CACHING (Node.js)                  │
│  ├─ GET requests (200 cache hits/sec)                │
│  └─ POST requests (no caching)                       │
│                                                        │
└────────────────────────────────────────────────────────┘
```

---

## Diagram Legend

| Symbol | Meaning |
|--------|---------|
| 🟢 Green | Operational / Active |
| 🟡 Yellow | In Development / Testing |
| 🔴 Red | Critical Issue |
| ✅ Check | Complete / Verified |
| 🔄 Arrows | Data flow direction |
| ├─ Tree | Sub-components |
| → Dash | Connection |

---

*Architecture Diagrams Last Updated: May 7, 2026*
