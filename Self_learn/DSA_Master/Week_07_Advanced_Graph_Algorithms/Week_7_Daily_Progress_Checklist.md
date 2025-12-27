# Week 7: Daily Progress Checklist & Interview Q&A (40+ Pairs)

## ✅ DAY 1: Dijkstra's Algorithm

### Morning Objectives
- [ ] Understand greedy selection of closest node
- [ ] Know priority queue essential for efficiency
- [ ] Understand non-negative weight requirement
- [ ] Know O((n+m) log n) complexity

### Core Learning
- [ ] Read: Week_7_Day_1_Dijkstras_Algorithm_Instructional.md
- [ ] Trace: Build distance array step-by-step
- [ ] Trace: Path reconstruction via parent pointers
- [ ] Implement: Dijkstra's from scratch

### Practice Problems
- [ ] Shortest path weighted
- [ ] Network delay time
- [ ] Path with maximum probability
- [ ] Swim in rising water

**Confidence Rating**: ___ / 5

---

## ✅ DAY 2: Bellman-Ford & Floyd-Warshall

### Morning Objectives
- [ ] Understand relaxation concept
- [ ] Know Bellman-Ford handles negatives
- [ ] Know Floyd-Warshall all-pairs O(n³)
- [ ] Understand negative cycle detection

### Core Learning
- [ ] Read: Week_7_Day_2_Bellman_Ford_Floyd_Warshall_Instructional.md
- [ ] Trace: Bellman-Ford relaxation passes
- [ ] Trace: Floyd-Warshall intermediate vertex k
- [ ] Implement: Both algorithms

### Practice Problems
- [ ] Cheapest flights with k stops
- [ ] Arbitrage detection
- [ ] All pairs shortest path
- [ ] Minimum cost path

**Confidence Rating**: ___ / 5

---

## ✅ DAY 3: Minimum Spanning Trees

### Morning Objectives
- [ ] Understand spanning tree (n-1 edges, all connected)
- [ ] Know Kruskal's edge-based O(m log m)
- [ ] Know Prim's vertex-based O((n+m) log n)
- [ ] Understand when use each

### Core Learning
- [ ] Read: Week_7_Day_3_Minimum_Spanning_Trees_Instructional.md
- [ ] Trace: Kruskal's with Union-Find
- [ ] Trace: Prim's with priority queue
- [ ] Implement: Both algorithms

### Practice Problems
- [ ] Minimum spanning tree (Kruskal's)
- [ ] Minimum spanning tree (Prim's)
- [ ] Redundant connections
- [ ] Minimum cost to connect

**Confidence Rating**: ___ / 5

---

## ✅ DAY 4: Network Flow I

### Morning Objectives
- [ ] Understand flow conservation
- [ ] Know capacity constraints
- [ ] Understand residual graph and reverse edges
- [ ] Know augmenting path concept

### Core Learning
- [ ] Read: Week_7_Day_4_Network_Flow_I_Instructional.md
- [ ] Trace: Ford-Fulkerson augmenting paths
- [ ] Trace: Residual graph updates
- [ ] Implement: Edmonds-Karp (BFS-based)

### Practice Problems
- [ ] Maximum network flow
- [ ] Maximal network rank
- [ ] Network flow maximum path
- [ ] Optimal account balancing

**Confidence Rating**: ___ / 5

---

## ✅ DAY 5: Network Flow II

### Morning Objectives
- [ ] Understand Max-Flow Min-Cut Theorem
- [ ] Know bipartite matching conversion
- [ ] Understand min-cut applications
- [ ] Know circulation with demands

### Core Learning
- [ ] Read: Week_7_Day_5_Network_Flow_II_Instructional.md
- [ ] Trace: Flow network for bipartite matching
- [ ] Trace: Min-cut after max-flow
- [ ] Implement: Min-cut finding

### Practice Problems
- [ ] Bipartite matching
- [ ] Image largest island (segmentation)
- [ ] Minimum cut networks
- [ ] Project selection

**Confidence Rating**: ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (40+ Pairs)

### Dijkstra's (5 pairs)

**Q1: Why does Dijkstra's require non-negative weights?**
A: Algorithm assumes once node processed, distance won't improve. Negative weights violate this. Shorter path via longer hop number could exist.

**Q2: Why use priority queue instead of array?**
A: Priority queue O(log n) per operation vs array O(n). Total: O((n+m) log n) vs O(n²). Critical for large graphs.

**Q3: How reconstruct actual path in Dijkstra's?**
A: Store parent[v] = u when updating distance[v]. Backtrack from target to source via parents.

**Q4: What happens if graph disconnected?**
A: Unreachable vertices remain at distance ∞. Dijkstra's only computes reachable vertices.

**Q5: Does Dijkstra's always find shortest path?**
A: YES, if all weights non-negative. Greedy choice safe. Closest unprocessed node can't improve further.

---

### Bellman-Ford & Floyd-Warshall (5 pairs)

**Q1: Why does Bellman-Ford need n-1 iterations?**
A: Longest simple path has n-1 edges. After n-1 iterations, all correct distances computed. Iteration i gives distances for paths with ≤ i edges.

**Q2: How detect negative cycle?**
A: Run nth iteration. If any distance improves, negative cycle exists (can still improve = cycle).

**Q3: Why is Floyd-Warshall O(n³)?**
A: Three nested loops: k (intermediate), i (source), j (destination). O(n) per operation.

**Q4: When use Floyd-Warshall vs Dijkstra's?**
A: Floyd-Warshall: all-pairs, simple, small graphs (n < 500). Dijkstra's: all-pairs from scratch, faster for sparse.

**Q5: Can Floyd-Warshall handle negative weights?**
A: YES. Negative cycles detected via dist[i][i] < 0.

---

### MST (5 pairs)

**Q1: Why Kruskal's better for sparse graphs?**
A: Sorting dominates: O(m log m). For sparse (m << n²), better than Prim's O((n+m) log n) in practice.

**Q2: Why Prim's better for dense graphs?**
A: Priority queue operations O((n+m) log n) constant. Sorting O(m log m) worse when m ≈ n².

**Q3: Can MST be non-unique?**
A: YES. If multiple edges with same weight, different MSTs possible. All have same total weight.

**Q4: How prove Kruskal's optimal?**
A: Cut property: minimum weight edge in any cut in some MST. Kruskal's always picks such edges.

**Q5: Why does Prim's need to track visited?**
A: Prevents processing vertex multiple times. Track minimum edge to each unvisited vertex.

---

### Network Flow I (5 pairs)

**Q1: Why do we need residual graph with reverse edges?**
A: Reverse edges represent flow cancellation. If path reroutes, must undo flow on previous edges.

**Q2: What's bottleneck in augmenting path?**
A: Minimum residual capacity on path. Limits how much flow we can send (bottleneck).

**Q3: Why is Ford-Fulkerson O(flow × m) inefficient?**
A: If max flow is large (e.g., 10^9), algorithm may take 10^9 iterations. Edmonds-Karp polynomial.

**Q4: Why does Edmonds-Karp use BFS?**
A: BFS finds shortest augmenting path. Ensures polynomial O(n × m²) complexity. Each path length increases.

**Q5: What's integrality property?**
A: If capacities integer, max-flow value and flow on each edge are integers. Guaranteed by algorithm.

---

### Network Flow II & Advanced (5+ pairs)

**Q1: What does Max-Flow Min-Cut Theorem state?**
A: Maximum flow from S to T equals minimum capacity of S-T cut. Flow and cut are dual problems.

**Q2: How model bipartite matching as flow?**
A: Source→left set (capacity 1), left↔right (capacity ∞), right→sink (capacity 1). Max flow = max matching.

**Q3: How find min-cut after computing max-flow?**
A: Run DFS/BFS in residual graph from source. Reachable = S-side, unreachable = T-side. Cut = edges between.

**Q4: Why can we solve min-cut via max-flow?**
A: Max-Flow Min-Cut Theorem. Compute max-flow, extract cut. No need for separate algorithm.

**Q5: What's circulation with demands?**
A: Every vertex has supply/demand. Find flow satisfying all demands. Circulation exists if supply = demand.

**Q6: When use flow vs direct algorithms?**
A: Flow: unified framework, simple implementation. Direct: sometimes faster, specialized. Choose based on problem.

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Implementation | Confidence |
|-----|-------|---|---|---|
| **1** | Dijkstra's | ___ | ___ | ___ / 5 |
| **2** | Bellman-Ford & Floyd-Warshall | ___ | ___ | ___ / 5 |
| **3** | MST | ___ | ___ | ___ / 5 |
| **4** | Network Flow I | ___ | ___ | ___ / 5 |
| **5** | Network Flow II | ___ | ___ | ___ / 5 |

**Target:** 4/5+ on all before Week 8

---

## ✅ WEEK 7 COMPLETION CHECKLIST

### Knowledge Check
- [ ] Can explain all 5+ algorithms and when to use
- [ ] Understand complexity trade-offs
- [ ] Know constraints and preconditions
- [ ] Can recognize problem types

### Skills Check
- [ ] Can implement Dijkstra's from scratch
- [ ] Can implement Bellman-Ford
- [ ] Can implement Kruskal's and Prim's
- [ ] Can implement Edmonds-Karp flow
- [ ] Can solve bipartite matching via flow
- [ ] Can solve basic min-cut problems
- [ ] Can choose algorithm for problem
- [ ] Can optimize for constraints

---

## 📈 Week 7 Summary

**Time:** ~12-14 hours  
**Topics:** 5+ advanced algorithms  
**Problems:** 40+  
**Coverage:** +10-12% (cumulative 90-95%)

**Ready for Week 8 (Advanced Topics)?** YES / NO

