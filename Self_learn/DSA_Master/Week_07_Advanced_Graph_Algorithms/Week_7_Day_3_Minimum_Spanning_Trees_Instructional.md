# Week 7, Day 3: Minimum Spanning Trees (Kruskal's & Prim's)

## 🗓 Metadata
**Week:** 7 | **Day:** 3 of 5 | **Topic:** Minimum Spanning Trees  
**Category:** Advanced Graph Algorithms | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-7 Days 1-2, Union-Find (Week 6 Day 5)  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Connect all vertices with minimum total edge weight (spanning tree). No cycles, all connected. Real-world: build roads/networks with minimum cable cost. Two greedy algorithms: Kruskal's (edge-based), Prim's (vertex-based).

**Design Problems Solved:**
- Network design (minimum infrastructure cost)
- Power grid optimization (minimum lines)
- Telecommunication backbone design
- Cluster analysis (grouping items)
- Game map generation (minimum connections)
- Image processing (region connectivity)
- Social network backbone (core relationships)

**Real System Usage:**
- **Telecom Networks:** Design networks with minimum cables
- **Power Distribution:** Build grids with minimum lines
- **Machine Learning:** MST for clustering algorithms
- **Road Networks:** Minimum road construction cost
- **Airline Networks:** Minimum connection routes
- **Network Topology:** Design backup paths
- **Game Design:** Minimum spawn point connectivity

**Why MST Matters:**
Greedy algorithms guarantee optimal solution. O(m log m) Kruskal's or O((n+m) log n) Prim's. Critical for infrastructure planning where cost minimization is essential.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think MST like **building minimal road network** connecting all towns. Can't skip towns, can't have cycles (wasteful). Find minimum total road length connecting all towns.

```
Example Graph (undirected, weighted):
    1 --5-- 2
    |       |
    3       4
    |       |
    4 --1-- 3

MST candidates:
Option 1: edges (3,4), (2,3), (1,2) = weight 5+4+5 = 14? No
Option 2: edges (3,4), (1,3), (2,3) = weight 1+4+4 = 9

Need exactly n-1 edges, connect all n vertices, minimum total weight.
```

**Key Invariants:**
1. **Spanning Tree:** n vertices, n-1 edges, all connected, no cycles
2. **Minimum:** Total weight minimized
3. **Uniqueness:** May not be unique if weights equal
4. **Greedy Safety:** Both Kruskal's and Prim's use greedy, guaranteed optimal

**Visual Representation:**

```
Graph (5 vertices):
    A --4-- B
    |       |
    2       3
    |       |
    C --1-- D --5-- E

Kruskal (edge-based):
Sorted edges: (C,D,1), (A,C,2), (B,D,3), (A,B,4), (D,E,5)
Pick (C,D,1): add, components {C,D}, {A}, {B}, {E}
Pick (A,C,2): add, components {A,C,D}, {B}, {E}
Pick (B,D,3): add, components {A,B,C,D}, {E}
Pick (A,B,4): skip, both in same component
Pick (D,E,5): add, components {A,B,C,D,E}

MST: edges (C,D,1), (A,C,2), (B,D,3), (D,E,5)
Total weight: 1+2+3+5 = 11
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `edges`: list of all edges
- `union_find`: tracks components
- `mst_weight`: total weight of MST

**Operation 1: Kruskal's Algorithm (Edge-Based)**
```
1. Sort edges by weight: O(m log m)
2. mst_weight = 0, mst_edges = []
3. For each edge (u,v,w) in sorted order:
     if find(u) != find(v):  // different components
       union(u,v)
       mst_weight += w
       mst_edges.append((u,v,w))
4. If |mst_edges| == n-1: MST found
5. Return mst_weight, mst_edges

Time: O(m log m) for sorting + O(m α(n)) for union-find
     = O(m log m) sorting dominates
Space: O(n) for union-find + O(m) for edges
```

**Operation 2: Prim's Algorithm (Vertex-Based)**
```
1. Start at arbitrary vertex s
2. visited = {s}, mst_weight = 0
3. pq = [(weight, u, v) for all edges from s]
4. While |visited| < n:
     (w, from_v, to_u) = pq.extract_min()
     if to_u in visited: continue  // already have this vertex
     visited.add(to_u)
     mst_weight += w
     For each edge (to_u, neighbor, w):
       if neighbor not in visited:
         pq.push((w, to_u, neighbor))
5. Return mst_weight

Time: O((n+m) log n) with binary heap
Space: O(n) for visited + O(n) for pq (can have O(m) edges)
```

**Memory Behavior:**
- Kruskal's: Sort dominates, O(m log m). Union-Find efficient O(α(n)).
- Prim's: Priority queue operations O(log n) × m = O(m log n). Total O((n+m) log n).

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Kruskal's MST (step-by-step)**

```
Graph:
  A --4-- B --3-- D
  |               |
  2               5
  |               |
  C --1-----------E

Edges sorted by weight:
(C,E,1), (A,C,2), (B,D,3), (A,B,4), (D,E,5)

Union-Find initialization:
parent = {A:A, B:B, C:C, D:D, E:E}

Step 1: Edge (C,E,1)
  find(C)=C, find(E)=E, different
  union(C,E), add to MST
  weight = 1
  parent = {A:A, B:B, C:C, D:D, E:C}

Step 2: Edge (A,C,2)
  find(A)=A, find(C)=C, different
  union(A,C), add to MST
  weight = 1+2=3
  parent = {A:C, B:B, C:C, D:D, E:C}

Step 3: Edge (B,D,3)
  find(B)=B, find(D)=D, different
  union(B,D), add to MST
  weight = 3+3=6
  parent = {A:C, B:D, C:C, D:D, E:C}

Step 4: Edge (A,B,4)
  find(A)=C, find(B)=D, different
  union(C,D), add to MST
  weight = 6+4=10
  parent = {A:C, B:D, C:D, D:D, E:D}

Step 5: Edge (D,E,5)
  find(D)=D, find(E)=D, SAME component
  skip this edge

MST complete: 4 edges (n-1), total weight 10
```

**Example 2: Prim's MST (step-by-step from A)**

```
Same graph as above

Start at A:
visited = {A}, weight = 0
pq = [(2, A, C), (4, A, B)]

Pop (2, A, C):
  C not visited, add C
  visited = {A, C}, weight = 2
  Add edges from C: (1, C, E)
  pq = [(1, C, E), (4, A, B)]

Pop (1, C, E):
  E not visited, add E
  visited = {A, C, E}, weight = 3
  No new edges from E (all visited or already in)
  pq = [(4, A, B)]

Pop (4, A, B):
  B not visited, add B
  visited = {A, B, C, E}, weight = 7
  Add edges from B: (3, B, D)
  pq = [(3, B, D)]

Pop (3, B, D):
  D not visited, add D
  visited = {A, B, C, D, E}, weight = 10
  Done (all visited)

MST: weight 10, same as Kruskal's
Edges: (A,C,2), (C,E,1), (A,B,4), (B,D,3)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Algorithm | Time | Space | Implementation | When |
|-----------|------|-------|-----------------|------|
| **Kruskal's** | O(m log m) | O(n+m) | Sorting + Union-Find | Sparse graphs |
| **Prim's** | O((n+m) log n) | O(n+m) | Priority queue | Dense graphs |
| **Prim's (array)** | O(n²) | O(n²) | Simple, no PQ | Dense, small n |

**Key Insight:** Choice depends on graph density. Kruskal's better for sparse (m << n²), Prim's for dense (m ≈ n²).

**Real Memory Behavior:**
- Kruskal's: Sorting dominates, must store all edges
- Prim's: Priority queue grows with edges added, typically O(n) in practice
- Both optimal for their respective use cases

**Edge Cases & Failure Modes:**
- **Disconnected graph:** MST doesn't exist (n-1 edges insufficient)
- **Single vertex:** MST is trivial (no edges)
- **Multiple edges:** Keep minimum weight, remove duplicates
- **Self-loops:** Ignore (no value in MST)
- **Negative weights:** Works fine (tree property unchanged)

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Telecommunication Networks:**
- Design backbone network with minimum fiber
- MST finds optimal core infrastructure
- Redundancy added afterward (but core is MST)

**Power Distribution Systems:**
- Connect power stations with minimum lines
- MST minimizes copper/infrastructure cost
- Real grids add redundancy beyond MST

**Machine Learning Clustering:**
- Build MST of data points
- Edges = similarity between points
- Remove long edges to create clusters
- MST-based clustering algorithm

**Game Engine Map Design:**
- Connect spawn points with minimum paths
- MST ensures all reachable with minimal connections
- Add shortcuts (edges beyond MST) for gameplay

**Network Topology Design:**
- Build backbone network
- MST provides minimum connectivity
- Add redundant links for reliability
- Critical for network planning

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Graph representations (Week 6 Day 1)
- Union-Find (Week 6 Day 5)
- Greedy algorithms (Week 4.5)
- Priority queues (Week 5 Day 4)

**Built Upon By:**
- **Steiner Tree:** Minimum spanning with intermediate vertices
- **Rectilinear MST:** Non-Euclidean distances
- **Bottleneck MST:** Minimize maximum edge weight
- **Degree-constrained MST:** Limit vertex degree

**Used In Algorithms:**
- Clustering (MST-based)
- Network design
- Approximation algorithms
- Single-linkage clustering

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Cut Property (Kruskal's Proof):**
For any cut of graph, minimum weight edge crossing cut is in some MST.
Proof: If not, replace heavier edge with minimum, still spanning tree with less weight.

**Cycle Property (Prim's Proof):**
For any cycle, maximum weight edge is not in any MST.
Proof: Removing max edge from any MST's cycle still connects all vertices.

**MST Uniqueness:**
Unique if all edge weights distinct. May have multiple MSTs if weights equal.

**Time Complexity:**
- Kruskal's: O(m log m) sorting + O(m α(n)) union-find = O(m log m)
- Prim's: O(n log n) extract + O(m log n) decrease-key = O((n+m) log n)
- Dense graph: Prim's O(n²) array beats both
- Sparse graph: Kruskal's O(m log m) beats Prim's O(m log n)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Kruskal's:**

✅ **Use when:**
- Sparse graph (m << n²)
- Edges already sorted
- Union-Find available
- Conceptually simpler (greedy edges)

✅ **Examples:**
- Network backbone design
- Clustering with distance matrix
- Infrastructure planning

**When to Use Prim's:**

✅ **Use when:**
- Dense graph (m ≈ n²)
- Priority queue preferred
- Start from specific vertex
- Incremental updates possible

✅ **Examples:**
- Real-time MST updates
- Dense geometric graphs
- Implicitly-defined edge sets

**When Use O(n²) Prim's:**

✅ **Use when:**
- Small dense graph (n < 1000)
- Simplicity preferred
- No priority queue available
- Cache efficiency important

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why are Kruskal's and Prim's guaranteed to find MST?

**Q2:** When would Kruskal's be faster than Prim's?

**Q3:** Can MST exist for disconnected graph?

**Q4:** What if all edge weights are equal?

**Q5:** How does negative weight affect MST?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **MST: Connect all vertices minimum weight. Kruskal's: O(m log m) sort edges + union-find. Prim's: O((n+m) log n) grow tree. Guaranteed optimal.**

**Mnemonic:** "M.S.T." → Minimum Spanning Tree, Sort edges or grow Tree, Total weight minimized

**Cognitive Lenses:**

| **Computational** | Kruskal's O(m log m), Prim's O((n+m) log n). Choose: sparse→Kruskal's, dense→Prim's. |
| **Psychological** | Kruskal's: greedy edges (natural). Prim's: grow tree (intuitive). Both make sense. |
| **Design Trade-off** | Kruskal's needs sorting, Prim's needs PQ. Different data structure choices. |
| **AI/ML Analogy** | Similar to: hierarchical clustering (build tree minimizing distances). |
| **Historical Context** | Kruskal (1956), Prim (1957). Foundational graph algorithms. Still optimal. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Minimum Spanning Tree (Kruskal's)
2. Minimum Spanning Tree (Prim's)
3. Maximum Spanning Tree (reverse)
4. Redundant Connection Removal
5. Minimum Cost to Connect All Points
6. Min Cost to Connect All Cities
7. Connecting Cities With Minimum Cost
8. Minimum Spanning Tree Cost

**Interview Q&A Highlights:**
- Kruskal's vs Prim's trade-offs?
- Why both guaranteed optimal?
- When choose each algorithm?
- Complexity analysis differences?
- Real-world applications?

**Common Misconceptions:**
- ❌ "Kruskal's always faster" → ✅ Depends on m vs n, sparse vs dense
- ❌ "MST always unique" → ✅ Multiple MSTs if equal weights
- ❌ "Need negative weights for cycles" → ✅ MST has no cycles regardless
- ❌ "Greedy always suboptimal" → ✅ MST greedy is optimal
- ❌ "Complex to implement" → ✅ Kruskal's simple with sorting + union-find

