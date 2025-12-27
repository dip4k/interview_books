# Week 7, Day 2: Bellman-Ford & Floyd-Warshall

## 🗓 Metadata
**Week:** 7 | **Day:** 2 of 5 | **Topic:** Bellman-Ford & Floyd-Warshall  
**Category:** Advanced Graph Algorithms | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-7 Day 1 (Dijkstra's, graph basics)  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Dijkstra's fails with negative weights. Need algorithms handling negative edges. Bellman-Ford: single-source, detects negative cycles. Floyd-Warshall: all-pairs distances. Trade-offs: time vs weight constraints.

**Design Problems Solved:**
- Currency arbitrage (negative cycles)
- Deadlock detection (negative weights = dependencies)
- Robot pathfinding with cost functions (negative rewards)
- Network routing with cost adjustments
- All-pairs shortest paths
- Social network influence (negative relationships)
- Financial market analysis (negative returns)

**Real System Usage:**
- **Financial Systems:** Arbitrage detection via negative cycles
- **Network Routing:** Handles cost adjustments
- **Game AI:** Pathfinding with variable costs
- **Database:** Query optimization with negative factors
- **Robotics:** Path planning with reward functions
- **Social Analysis:** Influence with negative connections
- **Network Testing:** Negative cycle detection

**Why Matters:**
Bellman-Ford handles negative weights (Dijkstra can't). Floyd-Warshall simple all-pairs solution. Essential for problems with negative relationships or costs.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Bellman-Ford like **relaxing muscles repeatedly** until no improvement. Floyd-Warshall like **learning through intermediaries**: "can I reach J better via K?" Test all combinations.

**Key Invariants:**
1. **Bellman-Ford:** Relax all edges n-1 times, detect cycles on nth pass
2. **Floyd-Warshall:** Test all intermediate nodes as shortcuts
3. **Negative cycles:** Bellman-Ford detects; Floyd-Warshall may not converge

**Bellman-Ford:**
```
For i from 1 to n-1:
  For each edge (u,v,w):
    distance[v] = min(distance[v], distance[u] + w)

Check negative cycle:
  For each edge (u,v,w):
    if distance[u] + w < distance[v]:
      NEGATIVE CYCLE EXISTS
```

**Floyd-Warshall:**
```
For k from 0 to n-1:  // intermediate vertex
  For i from 0 to n-1:  // source
    For j from 0 to n-1:  // destination
      distance[i][j] = min(distance[i][j], 
                           distance[i][k] + distance[k][j])
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Bellman-Ford Algorithm:**
```
1. Initialize: distance[source] = 0, others = ∞
2. For i from 1 to n-1:
     For each edge (u,v,w):
       if distance[u] + w < distance[v]:
         distance[v] = distance[u] + w
         parent[v] = u
3. For each edge (u,v,w):
     if distance[u] + w < distance[v]:
       NEGATIVE CYCLE
4. Return distance, parent

Time: O(n×m)
Space: O(n)
```

**Floyd-Warshall Algorithm:**
```
1. Initialize: dist[i][i] = 0, dist[i][j] = weight(i,j) or ∞
2. For k from 0 to n-1:
     For i from 0 to n-1:
       For j from 0 to n-1:
         dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
3. Return dist (all-pairs matrix)

Time: O(n³)
Space: O(n²)
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Bellman-Ford Example with negative edge:**

```
Graph: A --1--> B --(-3)--> C
       (A→C cost 4)

Distance[A]=0, [B]=∞, [C]=∞

Pass 1:
Edge (A,B,1): distance[B] = min(∞, 0+1) = 1
Edge (B,C,-3): distance[C] = min(∞, 1-3) = -2
Edge (A,C,4): distance[C] = min(-2, 0+4) = -2

Pass 2:
Edge (A,B,1): 0+1=1, no change
Edge (B,C,-3): 1-3=-2, no change
Edge (A,C,4): 0+4=4, no change

Check cycle: All edges satisfied, no negative cycle

Result: A(0), B(1), C(-2)
```

**Floyd-Warshall Example (small graph):**

```
      1
A --1--> B
|        ^
|        |2
3        |
v        |
C ----1--

Distance matrix after all passes:
  A  B  C
A 0  1  3
B ∞  0  2
C 1  3  0

(Testing via C as intermediate: A→C(3)→B(3+2)=5 not better)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Algorithm | Time | Space | Negative | All-Pairs |
|-----------|------|-------|----------|-----------|
| **Dijkstra's** | O((n+m) log n) | O(n) | ✗ | × |
| **Bellman-Ford** | O(n×m) | O(n) | ✓ | × |
| **Floyd-Warshall** | O(n³) | O(n²) | ✓ | ✓ |

**Key Insight:** Choose based on requirements. Dijkstra's fastest, but no negative. Bellman-Ford handles negative, single-source. Floyd-Warshall all-pairs.

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Financial Arbitrage Detection:**
- Currency exchange rates as weights
- Negative cycle = profit opportunity
- Bellman-Ford detects arbitrage

**Network Routing with Costs:**
- Link costs may be negative (incentives)
- Bellman-Ford handles adjustments
- Periodic updates for cost changes

**All-Pairs Network Analysis:**
- Floyd-Warshall for complete routing table
- Precompute all distances
- Used in small networks (n < 500)

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Dijkstra's (Week 7 Day 1)
- Relaxation concept
- Graph algorithms

**Built Upon By:**
- **Johnson's Algorithm:** Dijkstra's + Bellman-Ford for all-pairs
- **Linear Programming:** Similar relaxation concepts
- **Dynamic Programming:** Similar bottom-up approach

**Used In Algorithms:**
- Arbitrage detection
- Network optimization
- All-pairs shortest paths
- Graph negative cycle detection

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Bellman-Ford Correctness:**
After k iterations, correct distances to nodes at distance ≤ k edges.
Induction: after n-1 iterations, all reachable nodes have correct distance (no path > n-1 edges in shortest path).

**Floyd-Warshall Correctness:**
After k iterations, dist[i][j] = shortest path using only vertices {0..k} as intermediates.
Induction: extending intermediate set increases possible paths.

**Negative Cycle Detection:**
If nth iteration improves any distance, negative cycle exists (path can still improve = cycle possible).

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When Use Bellman-Ford:**
✅ Single-source shortest path with negative weights
✅ Need to detect negative cycles
✅ Sparse graphs (m << n²)

**When Use Floyd-Warshall:**
✅ All-pairs shortest paths
✅ Small graphs (n < 500)
✅ Need simple implementation

**When Use Dijkstra's:**
✅ Non-negative weights
✅ Faster than Bellman-Ford
✅ Single-source sufficient

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why does Bellman-Ford need n-1 iterations?

**Q2:** How does Bellman-Ford detect negative cycles?

**Q3:** Why is Floyd-Warshall O(n³) but simpler than Dijkstra's?

**Q4:** When would you use Floyd-Warshall over Bellman-Ford?

**Q5:** Can negative weights help find better paths?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Bellman-Ford: O(n×m) shortest path, handles negatives, detects cycles. Floyd-Warshall: O(n³) all-pairs, simple DP approach. Trade speed for flexibility.**

**Mnemonic:** "B.F." → Bellman-Ford, Flexible (negative), For single-source

**Cognitive Lenses:**

| **Computational** | Bellman-Ford O(n×m), Floyd-Warshall O(n³). Choose based on graph size and all-pairs need. |
| **Psychological** | Bellman-Ford: relax iteratively. Floyd-Warshall: try all shortcuts. Both intuitive. |
| **Design Trade-off** | Dijkstra's fastest but restricted. Bellman-Ford slower, more flexible. Floyd-Warshall simplest all-pairs. |
| **AI/ML Analogy** | Similar to: iterative refinement (relax constraints until convergence). |
| **Historical Context** | Bellman (1958), Ford (1962), Floyd-Warshall (1962). Still optimal for respective use cases. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Bellman-Ford Shortest Path
2. Network Delay (Bellman variant)
3. Arbitrage Detection
4. Floyd-Warshall All-Pairs
5. Cheapest Flights with k Stops
6. Negative Cycle Detection
7. Reachability with Constraints
8. Minimum Cost Path

**Interview Q&A Highlights:**
- Bellman-Ford vs Dijkstra's?
- Negative cycle detection?
- Floyd-Warshall all-pairs?
- Time complexity trade-offs?
- Real-world applications?

**Common Misconceptions:**
- ❌ "Bellman-Ford always slower" → ✅ Only if m >> n
- ❌ "Floyd-Warshall impractical" → ✅ Fine for n < 500
- ❌ "Negative weights impossible" → ✅ Bellman-Ford handles
- ❌ "No use for negative cycles" → ✅ Arbitrage detection critical
- ❌ "All algorithms equivalent" → ✅ Different trade-offs, choose wisely

