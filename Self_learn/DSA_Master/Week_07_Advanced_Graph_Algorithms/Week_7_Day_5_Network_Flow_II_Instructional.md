# Week 7, Day 5: Network Flow II (Min-Cut, Bipartite Matching, Advanced Applications)

## 🗓 Metadata
**Week:** 7 | **Day:** 5 of 5 | **Topic:** Network Flow II - Advanced  
**Category:** Advanced Graph Algorithms | **Difficulty:** 🔴 Hard  
**Prerequisites:** Week 1-7 Days 1-4  
**Time:** 120-150 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Maximum flow equals minimum cut (duality). Use network flow to solve bipartite matching, min-cut image segmentation, circulation with demands, project selection. Advanced applications of fundamental max-flow algorithm.

**Design Problems Solved:**
- Bipartite matching (optimal pairing)
- Minimum cut for image segmentation
- Circulation with supply/demand balancing
- Project selection with resources
- Baseball elimination (sports analytics)
- Optimal task assignment
- Supply chain optimization

**Real System Usage:**
- **Job Scheduling:** Match jobs to workers optimally
- **Image Processing:** Foreground/background segmentation
- **Logistics:** Balance supply and demand
- **Project Management:** Select projects respecting resources
- **Sports:** Determine playoff possibilities
- **Dating Apps:** Optimal matching of preferences
- **Hospital:** Assign doctors to shifts optimally

**Why Advanced Flow Matters:**
Max-flow min-cut duality fundamental. Bipartite matching solved elegantly via flow. Min-cut image segmentation powerful computer vision tool. Advanced flow algorithms handle complex real-world scenarios.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Concepts:**

**Max-Flow Min-Cut Theorem:**
Maximum flow from S to T = minimum capacity of any S-T cut.
Cut: partition vertices into S-side and T-side. Min-cut: cut with minimum capacity.

**Bipartite Matching:**
Two disjoint sets of vertices. Edges only between sets. Goal: maximum matching (each vertex matched at most once). Convert to max-flow problem.

**Min-Cut Applications:**
Image segmentation: partition pixels into foreground/background minimizing cut cost.

**Circulation:**
Flow with supply/demand at every vertex. Find circulation satisfying all demands.

```
Bipartite Matching as Flow:
Left set (jobs): J1, J2, J3
Right set (workers): W1, W2, W3
Source connects to all jobs (capacity 1)
Jobs connect to compatible workers (capacity ∞)
Workers connect to sink (capacity 1)
Max flow = maximum matching
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Operation 1: Bipartite Matching via Network Flow**
```
1. Build flow network:
   - Add source S, sink T
   - For each left vertex u: add edge S→u capacity 1
   - For each edge (u,v) in bipartition: add edge u→v capacity ∞
   - For each right vertex v: add edge v→T capacity 1
2. Compute maximum flow
3. Each unit of flow = one matching
4. Extract matching from flow

Time: O(n × m²) using Edmonds-Karp
```

**Operation 2: Min-Cut Finding**
```
1. Compute maximum flow
2. Build residual graph from flow
3. Find all reachable vertices from S in residual
4. Cut = all edges from reachable to unreachable
5. Cut capacity = max flow value

Time: O(n + m) for cut finding
```

**Operation 3: Circulation with Demands**
```
1. For each vertex v with demand d[v]:
   - If d[v] > 0: add super-source with edge capacity d[v]
   - If d[v] < 0: add super-sink with edge capacity -d[v]
2. Compute maximum flow
3. If flow = total demand, circulation exists

Time: O(n × m²) for flow computation
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Bipartite Matching**

```
Problem: Match jobs to workers
Jobs: J1, J2, J3
Workers: W1, W2, W3
Compatibility:
  J1 can go to W1, W2
  J2 can go to W2, W3
  J3 can go to W1, W3

Flow Network:
         J1 --∞--> W1
        /    |       \
       /     |        \1
      S--1--+  --∞--> W2 --> T
       \     |        /
        \ --J2--∞--  /1
         \   |     /
          \  |    /
           J3--∞--> W3

Max flow = 3:
Path 1: S→J1→W1→T (flow 1)
Path 2: S→J2→W2→T (flow 1)
Path 3: S→J3→W3→T (flow 1)

Matching: (J1,W1), (J2,W2), (J3,W3)
```

**Example 2: Min-Cut Image Segmentation**

```
Graph: Pixels connected by edge weights
High weight = should be in same region
Low weight = should be in different regions

Foreground pixels (high prob): weights high to source
Background pixels (high prob): weights high to sink
Edges between similar pixels: high weights
Edges between different pixels: low weights

Min-cut = partition minimizing "cost"
Foreground/background achieved naturally
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Problem | Algorithm | Time | Space |
|---------|-----------|------|-------|
| **Bipartite Matching** | Max-Flow | O(n×m²) | O(n²) |
| **Min-Cut** | Max-Flow + DFS | O(n×m²) | O(n²) |
| **Circulation** | Max-Flow | O(n×m²) | O(n²) |
| **Min-Cost Flow** | Successive shortest | O(n³) | O(n²) |

**Key Insight:** Flow-based algorithms elegant but not always fastest. Specialized algorithms may be better for specific problems.

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Job-to-Worker Assignment:**
- Workers have skill sets
- Jobs require specific skills
- Find maximum number of assignments
- Model as bipartite matching
- Solve via max-flow

**Image Segmentation:**
- Partition image into regions
- Minimize "cut" between regions
- Uses min-cut algorithm
- Fast and effective segmentation
- Practical computer vision

**Supply Chain Balancing:**
- Suppliers have supply levels
- Customers have demands
- Routes have capacities
- Balance supply/demand
- Circulation with demands

**Project Selection:**
- Projects generate profit
- Projects require resources
- Resources have limits
- Select projects maximizing profit
- Min-cut formulation

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Network Flow I (Week 7 Day 4)
- Ford-Fulkerson, Edmonds-Karp
- BFS/DFS, graph traversal

**Built Upon By:**
- **Multicommodity Flow:** Multiple sources/sinks
- **Minimum Cost Flow:** Cost per unit flow
- **Dynamic Flow:** Time-dependent capacities
- **Submodular Optimization:** Generalization

**Used In Algorithms:**
- Bipartite matching (Hungarian algorithm alternative)
- Image segmentation (computer vision)
- Logistics optimization
- Project planning

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Max-Flow Min-Cut Theorem (Formal):**
For any flow network, maximum flow from S to T equals minimum capacity of S-T cut.

**Proof Sketch:**
- Upper bound: any flow ≤ capacity of any S-T cut
- Achievability: max-flow algorithm finds flow achieving min-cut

**Bipartite Matching via Flow (Hall's Theorem):**
Maximum matching equals minimum vertex cover via max-flow duality.

**Integrality of Min-Cut:**
If all capacities integer, min-cut has integer value (immediate from max-flow integrality).

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Bipartite Matching:**

✅ **Use when:**
- Two disjoint sets needing pairing
- One-to-one matching required
- Compatibility constraints
- Optimization of assignments

✅ **Examples:**
- Job assignment
- Student-to-advisor matching
- Preference matching (dating apps)

**When to Use Min-Cut:**

✅ **Use when:**
- Need partition minimizing cost
- Image segmentation problem
- Project selection problem
- Clustering with cost

**When to Use Circulation:**

✅ **Use when:**
- Supply/demand balancing
- Flow at every vertex has constraint
- Commodity distribution
- Logistics networks

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** What does Max-Flow Min-Cut Theorem state?

**Q2:** How convert bipartite matching to max-flow problem?

**Q3:** Why is min-cut useful for image segmentation?

**Q4:** How detect if circulation exists?

**Q5:** When use flow-based vs specialized algorithms?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Network Flow II: Max-flow = min-cut (duality). Bipartite matching, min-cut segmentation, circulation. Flow solves diverse problems elegantly.**

**Mnemonic:** "M.F.M." → Max-Flow Min-Cut, Matching, Many applications

**Cognitive Lenses:**

| **Computational** | Bipartite O(nm²), Min-Cut O(nm²), Circulation O(nm²). All flow-based. |
| **Psychological** | Intuitive: max-flow = min-cut (beautiful duality). Matching natural formulation. |
| **Design Trade-off** | Unified framework vs specialized algorithms. Flow elegant but sometimes slower. |
| **AI/ML Analogy** | Similar to: convex optimization (duality, multiple formulations). |
| **Historical Context** | Max-Flow Min-Cut (1956), widespread applications since. Fundamental theorem. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Maximum Bipartite Matching
2. Image Largest Island (segmentation)
3. Minimum Cut to Make Network Connected
4. Project Selection with Constraints
5. Optimal Account Balancing
6. Baseball Elimination
7. Minimum Path Cost with Obstacles
8. Warehouse Location Optimization

**Interview Q&A Highlights:**
- Max-Flow Min-Cut Theorem meaning?
- How model bipartite matching as flow?
- Min-cut for image segmentation?
- Circulation existence check?
- Flow-based vs direct algorithms?

**Common Misconceptions:**
- ❌ "Flow only for transportation" → ✅ Solves matching, segmentation, etc.
- ❌ "Min-cut hard to compute" → ✅ Follows from max-flow
- ❌ "Bipartite matching complex" → ✅ Simple via flow formulation
- ❌ "Flow algorithms slow" → ✅ O(nm²) acceptable for most graphs
- ❌ "Theory only, no practice" → ✅ Critical for real applications

---

## 🎓 Week 7 Completion

**Five Advanced Graph Algorithms Mastered:**
- Day 1: Dijkstra's (greedy shortest path)
- Day 2: Bellman-Ford & Floyd-Warshall (negative weights, all-pairs)
- Day 3: MST (Kruskal's, Prim's)
- Day 4: Network Flow I (Ford-Fulkerson, Edmonds-Karp)
- Day 5: Network Flow II (Min-cut, bipartite, applications)

**Coverage:** 90-95% interview problems  
**Learning Time:** 12-14 hours  
**Practice Problems:** 40+  
**Interview Q&A:** 40+

**Ready for Week 8 (Advanced Topics)?** YES

