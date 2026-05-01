# 🎮 Advanced AI Algorithms in Unity Game Development

<div align="center">

![Unity](https://img.shields.io/badge/Unity-2022.3%20LTS-black?style=for-the-badge&logo=unity)
![C#](https://img.shields.io/badge/C%23-.NET%206.0-purple?style=for-the-badge&logo=csharp)
![Tests](https://img.shields.io/badge/Tests-47%20Passing-brightgreen?style=for-the-badge&logo=github-actions)
![Coverage](https://img.shields.io/badge/Coverage-~90%25-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-Academic-blue?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS-lightgrey?style=for-the-badge)

**BCA Final Year Project — Chandigarh University**  
*Submitted by Romit Nahar | Roll No: O23BCA110283*  
*Mentor: Dr. Vandana Sivaraj (Senior Mentor)*

---

### 🏆 +27.6% Player Satisfaction · 📈 +68% Session Length · ⚡ <3ms AI Budget (20 NPCs)

</div>

---

## 📺 Demo Video

> 🎬 **[▶ Watch Full Demo on YouTube](#)** ← *(add your link here)*

<!-- DEMO GIF PLACEHOLDER -->
> 📸 Add a screen-recording GIF here using tools like ScreenToGif or OBS → Ezgif
>
> Suggested GIF clips:
> - NPC FSM state transitions (Patrol → Alert → Chase → Attack → Flee)
> - A* Pathfinding in the dungeon corridor
> - Fuzzy Logic adaptive difficulty (aggression scaling as player HP drops)
> - Squad flanking behavior (emergent from BT + Steering)

---

## 📖 Project Overview

This project implements and empirically evaluates **five advanced AI algorithms** inside Unity 2022 LTS, measuring their combined impact on player engagement through a structured 30-participant user study.

> **Central Finding:** A multi-paradigm AI architecture (combining FSM + BT + A* + NavMesh + Fuzzy Logic) produces measurably superior player experience compared to single-algorithm approaches common in indie/student games.

### Key Results

| Metric | Alpha Phase | Beta Phase | Improvement |
|--------|------------|-----------|-------------|
| Overall AI Quality (/ 10) | 5.8 | 7.4 | **+27.6%** |
| Avg Session Length (mins) | 12.3 | 20.7 | **+68.3%** |
| Early Abandonment (< 5 min) | 33.3% | 6.7% | **−80.0%** |
| Non-Gamer Satisfaction (/ 5) | 2.1 | 3.4 | **+61.9%** |
| Players Requesting 2nd Round | 20.0% | 60.0% | **+200.0%** |

> All improvements statistically significant at **p < 0.01** with **Cohen's d > 0.8** (large effect size)

---

## 🧠 AI Systems Implemented

### 1. 🔄 Finite State Machine (FSM)
- **6 states**: Idle → Patrol → Alert → Chase → Attack → Flee → Death
- Generic C# implementation using dictionary-based O(1) state lookup
- CPU cost: **< 0.05ms per NPC** per frame

### 2. 🌳 Behavior Tree (BT)
- Built from scratch: Sequence, Selector, Inverter, Condition, Action, Wait nodes
- Priority-ordered combat decision logic (Flee > Attack > Chase > Investigate > Patrol)
- CPU cost: **0.1–0.4ms per NPC** for 20-node tree

### 3. 🗺️ A* Pathfinding
- Binary min-heap priority queue (O(log n) insertion)
- Hash set Closed Set (O(1) lookup)
- Benchmarks: 50×50 grid in **< 0.3ms**, 100×100 in **< 1.2ms**

### 4. 🧭 NavMesh Navigation
- 3 agent profiles: Guard, Scout, Brute
- Off-mesh link traversal, dynamic obstacle carving
- **5× faster** than custom A* for 3D environments

### 5. 🌫️ Fuzzy Logic Adaptive Difficulty
- Mamdani inference engine with trapezoidal membership functions
- Inputs: player distance + player health → Output: real-time aggression multiplier
- Produces natural tension-release rhythm without manual difficulty tuning

### 6. 🚶 Steering Behaviors
- Seek, Flee, Wander, Separation, Alignment, Cohesion, Avoidance
- Emergent squad flanking observed (not explicitly programmed!)

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│              AI AGENT (AIAgent.cs)           │
├─────────────┬───────────────┬───────────────┤
│  PERCEPTION │   REASONING   │    ACTION     │
│             │               │               │
│ SensorComp  │ AIStateMachine│ NavMeshAgent  │
│ VisionCone  │ BehaviorTree  │ UnityAnimator │
│ HearingZone │ FuzzyEngine   │ CombatSystem  │
│ Blackboard  │               │               │
└─────────────┴───────────────┴───────────────┘
         ↕ Shared via Blackboard Pattern ↕
```

All modules communicate via **C# events** and **ScriptableObject** data — zero tight coupling.

---

## ⚡ Performance Benchmarks

| Scenario | NPCs | Avg FPS | AI Cost (avg) | AI Cost (p99) | Memory |
|----------|------|---------|---------------|---------------|--------|
| Open Terrain | 10 | 96 FPS | 0.41 ms | 0.91 ms | 62 MB |
| Open Terrain | 20 | 78 FPS | 0.82 ms | 1.62 ms | 87 MB |
| Dungeon Corridors | 20 | 61 FPS | 1.11 ms | 2.41 ms | 94 MB |
| Mixed Urban | 20 | 67 FPS | 0.93 ms | 1.82 ms | 89 MB |
| Mixed Urban | 30 | 43 FPS | 1.83 ms | 3.12 ms | 112 MB |

**Target budget: ≤ 3ms/frame with 20 NPCs** ✅ Achieved (0.8ms avg)

---

## 🗂️ Project Structure

```
Assets/
├── Scripts/
│   ├── AI/
│   │   ├── Core/           → AIAgent, AIStateMachine, Blackboard
│   │   ├── States/         → Idle, Patrol, Alert, Chase, Attack, Flee, Death
│   │   ├── BehaviorTree/   → Node, Sequence, Selector, Conditions, Actions
│   │   ├── Pathfinding/    → AStarPathfinder, GridMap, MinHeap
│   │   ├── FuzzyLogic/     → FuzzyInferenceEngine, TrapezoidalMF, FuzzyProfile
│   │   ├── Perception/     → SensorComponent, HearingZone, CoverSystem
│   │   └── Steering/       → SeekBehavior, FleeBehavior, WanderBehavior, Flocking
│   ├── Player/             → PlayerController, PlayerHealth
│   └── Managers/           → GameManager, SpawnManager, LogManager
├── ScriptableObjects/      → NPCConfig, FuzzyProfile, LevelData
├── Scenes/                 → OpenTerrain, DungeonCorridors, MixedUrban
└── Tests/
    ├── EditMode/           → AIStateMachineTests, AStarTests, FuzzyTests, BTTests
    └── PlayMode/           → IntegrationTests, PerformanceTests
```

---

## 🧪 Test Suite

```
Test Suite                  Tests    Coverage    Status
─────────────────────────────────────────────────────
AIStateMachineTests.cs        12       94%       ✅ All Pass
AStarPathfinderTests.cs        8       88%       ✅ All Pass
FuzzyEngineTests.cs            9       91%       ✅ All Pass
BehaviorTreeTests.cs          11       86%       ✅ All Pass
IntegrationTests.cs            5       N/A       ✅ All Pass
PerformanceTests.cs            2       N/A       ✅ All Pass
─────────────────────────────────────────────────────
TOTAL                         47      ~90%       ✅ All Pass
```

CI runs automatically on every pull request via **GitHub Actions**.

---

## 🚀 Getting Started

### Prerequisites
- Unity 2022.3.15f1 LTS
- Visual Studio 2022 (Community or higher)
- Git 2.42+

### Setup

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/unity-ai-bca-project.git

# 2. Open in Unity Hub → Add project from disk
# Select the cloned folder

# 3. Open any scene
# File → Open Scene → Assets/Scenes/MixedUrban.unity

# 4. Press Play!
```

### Controls

| Key | Action |
|-----|--------|
| `WASD` | Move player |
| `Mouse` | Look around |
| `F1` | Toggle AI debug overlay |
| `Space` | Jump |
| `Left Click` | Attack |

---

## 🧩 NPC Types

| NPC | Speed | Vision | Health | Role |
|-----|-------|--------|--------|------|
| Guard | 3.5 m/s | 12m / 90° | 100 | Balanced patrol + combat |
| Scout | 5.5 m/s | 15m / 120° | 60 | Fast flanker, wide vision |
| Brute | 2.0 m/s | 8m / 60° | 300 | Slow, high damage tank |

---

## 🔮 Future Scope

- [ ] **Unity ML-Agents** — PPO reinforcement learning for patrol optimization
- [ ] **Hierarchical Task Networks (HTN)** — Multi-phase boss AI
- [ ] **Visual BT Editor** — Drag-and-drop behavior tree authoring
- [ ] **Jump Point Search (JPS)** — 3× faster open-grid pathfinding
- [ ] **LLM-Driven Dialogue** — Contextually aware NPC conversation
- [ ] **Open-Source Package** — Unity Package Manager release

---

## 📚 References

| # | Source | Contribution |
|---|--------|-------------|
| 1 | Millington & Funge (2009) — *AI for Games* | FSM, Steering, A* foundations |
| 2 | Buckland (2004) — *Programming Game AI by Example* | C# FSM/A* patterns |
| 3 | Isla, GDC 2005 — *Halo 2 AI* | Behavior Tree architecture |
| 4 | Russell & Norvig (2020) — *AI: A Modern Approach* | Search theory, A* proof |
| 5 | Yannakakis & Togelius (2018) — *AI and Games* | Player modeling |

---

## 👤 Author

**Romit Nahar**  
Roll No: O23BCA110283  
Bachelor of Computer Application (BCA)  
Department of Computer Science & Engineering  
Chandigarh University  
📧 Contact: 9001582969

**Mentor:** Dr. Vandana Sivaraj (Senior Mentor)  
**Submitted:** 20-01-2026 | **Platform:** Qollabb

---

<div align="center">

*"The best game AI is the kind the player never notices — they only feel its effects."*

⭐ **Star this repo if it helped you!** ⭐

</div>
