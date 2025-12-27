# Week 7, Day 1: Dijkstra's Algorithm

## 🗓 Metadata
**Week:** 7 | **Day:** 1 of 5 | **Topic:** Dijkstra's Algorithm  
**Category:** Advanced Graph Algorithms | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-6 (Graph fundamentals, BFS, priority queues)  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Find shortest path in weighted graph (distances, costs, latencies). BFS only works for unweighted. Need efficient algorithm for weighted graphs. Dijkstra's greedy approach: always expand closest unexplored node.

**Design Problems Solved:**
- GPS navigation (shortest route by distance/time)
- Network routing (shortest path by latency/hops)
- Robot pathfinding (cost-weighted terrain)
- Social networks (influence minimization)
- Game AI (pathfinding with terrain costs)
- Airline routing (cheapest flight path)
- Telecommunication networks (minimum latency)

**Real System Usage:**
- **Google Maps/GPS:** Dijkstra's for route calculation
- **BGP Routing:** Network routing protocol uses similar concept
- **Telecommunications:** Find minimum-latency paths
- **Game Engines:** Pathfinding with varied terrain costs
- **Robotics:** Motion planning with cost functions
- **Social Networks:** Find influence paths
- **Database Query Optimization:** Cost-based optimization

**Why Dijkstra's Matters:**
Greedy algorithm guaranteeing optimal shortest path with non-negative weights. O((n+m) log n) with priority queue. Fundamental for routing systems handling millions of queries daily.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think of Dijkstra's like **expanding ripples, but at different speeds**. Close nodes expand fast, far nodes expand slow. Always expand the closest node first. Guaranteed shortest path because closer nodes can't improve further.

```
Weighted Graph:
    A --1-- B --2-- D
    |       |
    3       5
    |       |
    C --1-- E

Dijkstra from A:
Round 1: Expand A (distance 0)
  B at distance 1
  C at distance 3

Round 2: Expand B (distance 1, closest)
  D at distance 1+2=3
  E at distance 1+5=6

Round 3: Expand C (distance 3)
  E at min(6, 3+1) = 4
  
Round 4: Expand E (distance 4)
  D still at 3

Round 5: Expand D (distance 3)
  Done

Shortest paths from A: A(0), B(1), C(3), D(3), E(4)
```

**Key Invariants:**
1. **Greedy selection:** Always process closest unprocessed node
2. **Distance finalization:** Once processed, distance never decreases
3. **Non-negative weights:** Algorithm assumes weights ≥ 0
4. **Priority queue:** Efficient extraction of minimum distance

**Visual Representation:**

```
Dijkstra Exploration (distance, parent):
Start: A(0)
Frontier: {B(1,A), C(3,A)}

Process B(1):
Frontier: {D(3,B), C(3,A), E(6,B)}

Process C(3):
Frontier: {D(3,B), E(4,C)}

Process D(3):
Frontier: {E(4,C)}

Process E(4):
Done

Final: A→0, B→1, C→3, D→3, E→4
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `distance[v]`: shortest known distance from source to v
- `processed`: set of processed vertices
- `pq`: priority queue of (distance, vertex) pairs

**Operation 1: Dijkstra's Algorithm**
```
1. distance[source] = 0, all others = ∞
2. pq.push((0, source))
3. While pq not empty:
     dist, u = pq.pop()
     if u in processed: continue
     processed.add(u)
     For each neighbor v of u with edge weight w:
       if distance[u] + w < distance[v]:
         distance[v] = distance[u] + w
         parent[v] = u
         pq.push((distance[v], v))
4. Return distance, parent

Time: O((n+m) log n) with binary heap
Space: O(n) for distance and processed
```

**Operation 2: Path Reconstruction**
```
1. path = []
2. current = target
3. While current != source:
     path.prepend(current)
     current = parent[current]
4. path.prepend(source)
5. Return path

Time: O(path length)
```

**Memory Behavior:**
- Priority queue: O(n) at worst, typical O(log n) height
- Distance array: O(n) space
- Each edge processed once: O(m) total
- Priority queue operations: O(log n) per operation

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Dijkstra from A in weighted graph**

```
Graph:
  A --1-- B --2-- D
  |       |
  3       5
  |       |
  C --1-- E

Dijkstra from A:

Initialization:
distance = {A:0, B:∞, C:∞, D:∞, E:∞}
processed = {}
pq = [(0, A)]

Step 1: Pop (0, A), process A
processed = {A}
Neighbors: B(1), C(3)
  distance[B] = 0+1=1 < ∞, update
  distance[C] = 0+3=3 < ∞, update
pq = [(1, B), (3, C)]

Step 2: Pop (1, B), process B
processed = {A, B}
Neighbors: A(already), D(2), E(5)
  distance[D] = 1+2=3 < ∞, update
  distance[E] = 1+5=6 < ∞, update
pq = [(3, C), (3, D), (6, E)]

Step 3: Pop (3, C), process C
processed = {A, B, C}
Neighbors: A(already), E(1)
  distance[E] = 3+1=4 < 6, update!
pq = [(3, D), (4, E)]

Step 4: Pop (3, D), process D
processed = {A, B, C, D}
Neighbors: B(already), E(already)
pq = [(4, E)]

Step 5: Pop (4, E), process E
processed = {A, B, C, D, E}
Done

Final distances: A(0), B(1), C(3), D(3), E(4)
Shortest paths: A→A(0), A→B(1), A→C(3), A→D(1→2), A→E(3→1)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Implementation | Insert | Extract-Min | Total Time |
|----------------|--------|-------------|-----------|
| **Array** | O(1) | O(n) | O(n²) |
| **Binary Heap** | O(log n) | O(log n) | O((n+m) log n) |
| **Fibonacci Heap** | O(1) amort | O(log n) amort | O(n log n + m) |

**Key Insight:** Priority queue choice matters. Fibonacci heap theoretical best, binary heap practical standard.

**Real Memory Behavior:**
- Binary heap: Array-based, good cache locality
- Each vertex processed once: O(n) node extractions
- Each edge relaxation: O(m) updates
- Priority queue operations: logarithmic per edge

**Edge Cases & Failure Modes:**
- **Negative weights:** Algorithm fails (gives wrong results)
- **Negative cycles:** Not applicable with Dijkstra's
- **Disconnected nodes:** Remain at distance ∞
- **Self-loops:** Ignored (distances don't improve)
- **Multiple edges:** Keep minimum weight

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Google Maps/GPS Navigation:**
- Weighted graph: roads with distance/time weights
- Dijkstra's for single-source shortest path
- Precomputed with A* variants for speed
- Real-time updates for traffic

**Network Routing (BGP/OSPF):**
- Link-state routing: Dijkstra's algorithm
- Weights = link costs (latency, bandwidth)
- Each router computes shortest paths
- Periodic updates for topology changes

**Telecommunications:**
- Find minimum-latency paths
- Weights = network latency
- Critical for real-time communication
- Used in 5G network routing

**Game Engines (Pathfinding):**
- Terrain costs: mountains costly, plains cheap
- Dijkstra's for optimal routes
- Often use A* (Dijkstra + heuristic)
- Combat pathfinding with dynamic obstacles

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Graph representations (Week 6 Day 1)
- BFS (Week 6 Day 2)
- Priority queues (Week 5 Day 4)
- Greedy algorithms

**Built Upon By:**
- **A* Algorithm:** Dijkstra's + heuristic
- **Bidirectional Search:** Run from both ends
- **Graph Contraction:** Preprocessing for speed
- **ALT Algorithm:** Landmarks for speedup

**Used In Algorithms:**
- Single-source shortest path
- All-pairs via repeated Dijkstra's
- Minimum spanning tree (variant)
- Network routing protocols

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Correctness Proof (by induction):**
Maintain invariant: processed vertices have correct shortest distances.
- Base: source distance 0 is correct
- Inductive: when processing next vertex u, its distance is minimal (can't improve via unprocessed)

**Greedy Choice Property:**
After sorting unprocessed by distance, expanding minimum is safe. No edge weight can reduce distance to closer node from farther node.

**Time Complexity:**
T(n,m) = O((n+m) log n) with binary heap because:
- Extract-min: O(log n) × n = O(n log n)
- Decrease-key: O(log n) × m = O(m log n)
- Total: O((n+m) log n)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Dijkstra's:**

✅ **Use when:**
- Need shortest path with non-negative weights
- Single-source distances sufficient
- Graphs sparse to moderate density
- Real-time queries (preprocessing possible)

✅ **Examples:**
- GPS navigation
- Network routing
- Game pathfinding
- Airline pricing

❌ **Don't use when:**
- Negative weights (use Bellman-Ford)
- Dense graphs (Floyd-Warshall may be better)
- Need all-pairs (repeated Dijkstra's suboptimal)
- Only need single path (BFS for unweighted faster)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why does Dijkstra's require non-negative weights?

**Q2:** Why is greedy choice safe (always expand closest node)?

**Q3:** How does priority queue improve naive O(n²) to O((n+m) log n)?

**Q4:** Can Dijkstra's handle multiple edges between same vertices?

**Q5:** What happens if graph is disconnected?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Dijkstra's: Greedy shortest path for non-negative weights. Always expand closest unprocessed node. O((n+m) log n) with priority queue. Essential for routing.**

**Mnemonic:** "D.I.J." → Distance tracking, Incremental expansion, Jump to nearest

**Cognitive Lenses:**

| **Computational** | O((n+m) log n) optimal for weighted. Priority queue essential. Binary heap standard. |
| **Psychological** | Intuitive: expand closer nodes first. Safe because closer can't worsen far nodes. |
| **Design Trade-off** | Dijkstra's vs Bellman-Ford: speed vs negative weights. Trade accuracy for efficiency. |
| **AI/ML Analogy** | Similar to: greedy best-first search (always pick best option so far). |
| **Historical Context** | Dijkstra 1956. Still optimal for non-negative weights. A* variant with heuristic. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Shortest Path (Dijkstra's)
2. Network Delay Time
3. Path with Maximum Probability
4. Reachable Nodes with Restrictions
5. Minimum Cost to Reach Destination
6. Swim in Rising Water
7. Minimum Effort Path
8. Path with Maximum Minimum Value

**Interview Q&A Highlights:**
- Why non-negative weights requirement?
- How priority queue improves complexity?
- Greedy proof: why safe?
- Time/space complexity trade-offs?
- When use vs Bellman-Ford?

**Common Misconceptions:**
- ❌ "Works with negative weights" → ✅ Only non-negative
- ❌ "Always finds shortest path" → ✅ Only if non-negative
- ❌ "Faster than BFS" → ✅ BFS faster for unweighted
- ❌ "Complex to implement" → ✅ Simple with priority queue
- ❌ "Only academic" → ✅ GPS, routing use daily

