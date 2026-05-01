# 🎬 DEMO VIDEO SCRIPT
## Advanced AI Algorithms in Unity Game Development
### Romit Nahar | BCA Final Year Project | Chandigarh University

---

## 📋 PRE-RECORDING CHECKLIST

Before hitting record:
- [ ] Unity scene: **MixedUrban** (most visually impressive)
- [ ] Resolution: 1920×1080, 60 FPS
- [ ] F1 Debug Overlay: **ON** (shows FSM states, detection radii)
- [ ] NPC Color Coding: Green=Patrol, Yellow=Alert, Red=Chase/Attack, Blue=Flee
- [ ] Audio: Background music low, game sounds audible
- [ ] Recording tool: OBS Studio (free) recommended
- [ ] Target video length: **5–8 minutes**

---

## 🎙️ VIDEO STRUCTURE

---

### [0:00 – 0:30] INTRO SLIDE / TITLE CARD

**Show:** A clean title screen with project name, your name, university logo

**Say:**
> *"Hi everyone! I'm Romit Nahar, a BCA student from Chandigarh University.  
> This is my final year project: Advanced AI Algorithms in Unity Game Development.  
> In this demo, I'll show you five AI systems I built from scratch in C# inside Unity 2022 —  
> Finite State Machines, Behavior Trees, A-Star Pathfinding, NavMesh Navigation, and  
> a Fuzzy Logic adaptive difficulty engine.  
> Let's dive in."*

---

### [0:30 – 1:30] SCENE OVERVIEW + DEBUG OVERLAY

**Show:** Fly the camera over the Mixed Urban map. Then press F1 to activate debug overlay.

**Say:**
> *"This is the Mixed Urban test environment — city blocks, alleys, buildings, and open plazas.  
> I've designed three such environments for this project. Let me press F1 to enable the AI debug overlay.  
> You can now see colored spheres above each NPC — green means Patrol, yellow is Alert,  
> red is Chase or Attack, and blue means the NPC is Fleeing.  
> The circles around them show their detection radius. Everything you see is real-time AI data."*

---

### [1:30 – 2:30] FSM DEMONSTRATION — PATROL → ALERT → CHASE → ATTACK

**Show:** Walk the player character toward a patrolling guard NPC. Let the detection trigger.  
Watch the NPC sphere change: Green → Yellow → Red.

**Say:**
> *"Here's my Finite State Machine in action. This Guard NPC is in Patrol state — following waypoints.  
> Watch what happens when I walk into its vision cone...  
> [pause as detection triggers]  
> It's now in Alert — investigating my last known position.  
> If I stay visible for 2.5 seconds... it transitions to Chase.  
> And when I'm within 2.5 meters — Attack.  
> Each transition has guard conditions, and each state has its own OnEnter, OnUpdate, and OnExit logic.  
> The FSM processes in under 0.05 milliseconds per NPC — extremely lightweight."*

---

### [2:30 – 3:15] FLEE STATE + DEATH

**Show:** Let the NPC take damage (or trigger it via a config). Watch it flee and then die.

**Say:**
> *"If an NPC's health drops below 15%, the FSM triggers the Flee state — watch the sphere go blue.  
> The NPC now actively navigates away from the player and seeks cover.  
> [let it play out]  
> And when health reaches zero — the Death transition fires cleanly, mid-movement if needed.  
> All six of these state transitions are covered by 12 automated unit tests, all passing."*

---

### [3:15 – 4:00] BEHAVIOR TREE — SQUAD FLANKING

**Show:** Trigger a multi-NPC encounter. One NPC approaches from the front, another flanks the side.

**Say:**
> *"Now let's look at the Behavior Tree. I built this from scratch — no plugins.  
> It uses Sequence nodes (logical AND), Selector nodes (logical OR), Condition nodes, and Action nodes.  
> Watch this encounter — I have two Guards and a Scout coming at me.  
> [let the encounter play]  
> Notice how one guard approached from the front while another came from my left?  
> That flanking behavior was never explicitly programmed. It emerged from each NPC  
> independently pathfinding to my position from different locations.  
> That's emergent behavior from the BT priority system and steering forces working together."*

---

### [4:00 – 4:45] FUZZY LOGIC ADAPTIVE DIFFICULTY

**Show:** Let player health drop low. NPCs should visibly speed up and attack faster.

**Say:**
> *"This is my favorite part — the Fuzzy Logic adaptive difficulty system.  
> Classical difficulty settings give you Easy, Normal, Hard — three discrete levels.  
> Mine is continuous. It takes two inputs every frame:  
> how far the player is, and what percentage health they have.  
> Watch what happens as my health drops...  
> [let health drop to around 30%]  
> The NPCs are attacking faster. More aggressively. The difficulty scaled up automatically.  
> Now watch — if I back off and create distance...  
> [retreat]  
> The pressure eases. That's the tension-release rhythm that good game designers spend months tuning.  
> Here it emerges from a 20-line fuzzy inference engine.  
> In my user study, non-gamer participants saw a 61.9% improvement in satisfaction  
> specifically because of this system."*

---

### [4:45 – 5:30] A* PATHFINDING (DUNGEON SCENE)

**Show:** Switch to Dungeon Corridors scene. Show an NPC navigating around obstacles.  
Place a dynamic obstacle (box/door) and show the NPC reroute.

**Say:**
> *"Let me switch to the Dungeon environment to demonstrate my custom A-Star pathfinder.  
> This is not Unity's built-in NavMesh — I implemented A-Star from scratch using a binary min-heap  
> priority queue for O-log-n performance.  
> Watch the NPC navigate these tight corridors...  
> [let it navigate]  
> Now I'll place a dynamic obstacle in its path...  
> [place obstacle]  
> The NavMesh recalculates in real-time — the NPC finds an alternate route in under 0.5 seconds.  
> On a 50×50 grid, pathfinding completes in under 0.3 milliseconds."*

---

### [5:30 – 6:00] PERFORMANCE PROFILER

**Show:** Open Unity Profiler. Show AI cost markers with 20 NPCs in Mixed Urban.

**Say:**
> *"Let me show you the Unity Profiler with 20 NPCs active simultaneously.  
> I've tagged every AI subsystem with profiler markers.  
> [point to the profiler graph]  
> Total AI cost: around 0.8 to 0.9 milliseconds per frame.  
> My target was under 3 milliseconds — I'm well within budget.  
> The frame rate stays at 67 FPS in the most complex environment.  
> This was achieved through LOD AI, spatial hashing for detection, object pooling, and path caching."*

---

### [6:00 – 6:30] TEST SUITE (EDITOR VIEW)

**Show:** Open Unity Test Runner. Show all 47 tests green.

**Say:**
> *"The project follows Test-Driven Development methodology.  
> Here's the Unity Test Framework — I have 47 automated tests across 6 suites.  
> FSM transition tests, A-Star correctness tests, fuzzy engine boundary tests, BT logic tests.  
> All 47 pass. About 90% average code coverage.  
> These run automatically on every GitHub pull request via GitHub Actions CI."*

---

### [6:30 – 7:00] USER STUDY RESULTS SLIDE

**Show:** A slide or graphic showing the before/after comparison table.

**Say:**
> *"Finally — the results from my 30-participant user study across two testing phases.  
> Overall AI quality jumped from 5.8 to 7.4 out of 10 — a 27.6% improvement.  
> Average session length grew from 12 to 20 minutes — 68% longer.  
> Early abandonment dropped from 33% to just 6.7%.  
> All results are statistically significant at p less than 0.01 with large effect sizes.  
> The multi-paradigm approach works."*

---

### [7:00 – 7:20] CLOSING

**Show:** GitHub repo page

**Say:**
> *"The full source code, report, and CI configuration are on my GitHub — link in the description.  
> The project was built over 16 weeks using Unity 2022 LTS, C#, and Git with GitHub Actions.  
> Thank you for watching!  
> If you're a fellow student working on game AI — feel free to use this as a reference.  
> The README covers everything you need to get started."*

---

## 🎯 RECORDING TIPS

| Tip | Detail |
|-----|--------|
| **Resolution** | Record at 1920×1080, export at same resolution |
| **Frame Rate** | 60 FPS recording for smooth gameplay footage |
| **Microphone** | Use a quiet room; speak clearly and at a steady pace |
| **OBS Settings** | Bitrate: 6000 kbps, Encoder: x264, Audio: 192 kbps |
| **Editing** | Use DaVinci Resolve (free) for cuts, captions, and music |
| **Music** | Kevin MacLeod royalty-free tracks work great for game demos |
| **Captions** | Add text overlays when switching scenes or showing profiler |
| **YouTube** | Upload as Unlisted first to test, then Public when ready |
| **Thumbnail** | Screenshot the most visually impressive NPC encounter |

---

## 📌 DESCRIPTION TEMPLATE (for YouTube / GitHub)

```
🎮 Advanced AI Algorithms in Unity Game Development
BCA Final Year Project | Chandigarh University | Romit Nahar

🔗 GitHub Repo: https://github.com/<your-username>/unity-ai-bca-project

In this video I demonstrate 5 AI systems built from scratch in Unity 2022 (C#):
• Finite State Machine (6-state NPC behavior)
• Behavior Tree (priority-based decision making)
• A* Pathfinding (custom binary min-heap implementation)
• NavMesh Navigation (dynamic obstacle avoidance)
• Fuzzy Logic Adaptive Difficulty (real-time aggression scaling)

Results from 30-participant user study:
✅ +27.6% AI quality score
✅ +68% session length
✅ <3ms AI budget with 20 concurrent NPCs
✅ 47 automated tests, ~90% coverage

Mentor: Dr. Vandana Sivaraj | Roll No: O23BCA110283

#Unity #GameAI #BehaviorTree #AStarPathfinding #FuzzyLogic #GameDev #CSharp #Unity2022
```

---

*Script prepared for: Romit Nahar | O23BCA110283 | Chandigarh University*
