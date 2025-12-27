# Week 7 (Advanced Graph Algorithms): Guidelines

## 📅 Daily Breakdown & Time Allocation

**Total Week:** 12-14 hours (2.4-2.8 hours per day)

| Day | Topic | Time | Focus | Coverage |
|-----|-------|------|-------|----------|
| **1** | Dijkstra's Algorithm | 2.5h | Greedy shortest path, non-negative weights | 2-3% |
| **2** | Bellman-Ford & Floyd-Warshall | 2.5h | Negative weights, all-pairs, arbitrage | 2-3% |
| **3** | Minimum Spanning Trees | 2.5h | Kruskal's, Prim's, infrastructure | 2-3% |
| **4** | Network Flow I | 2.5h | Ford-Fulkerson, Edmonds-Karp, augmenting paths | 2-3% |
| **5** | Network Flow II | 2.5h | Min-cut, bipartite matching, circulation | 2-3% |
| **Weekend** | Integration & Review | 2-3h | Algorithm selection, real-world problems | — |

**Total:** 12-14 hours, 5 advanced graph algorithms

---

## 🎯 Learning Objectives

### By End of Week 7
- [ ] Master Dijkstra's for weighted shortest paths
- [ ] Understand Bellman-Ford and Floyd-Warshall trade-offs
- [ ] Implement Kruskal's and Prim's MST algorithms
- [ ] Understand network flow fundamentals (Ford-Fulkerson)
- [ ] Use max-flow for bipartite matching and min-cut
- [ ] Recognize which algorithm for each problem
- [ ] Understand real-world applications
- [ ] Solve 90-95% of interview problems (cumulative)

---

## 📚 Core Concepts

**Concept 1: Weighted Shortest Path**  
Dijkstra's greedy approach: always expand closest node. O((n+m) log n) with priority queue.

**Concept 2: Negative Weights & All-Pairs**  
Bellman-Ford for single-source with negatives. Floyd-Warshall for all-pairs. Different trade-offs.

**Concept 3: Minimum Spanning Tree**  
Connect all vertices, minimum weight, no cycles. Kruskal's (edge-based O(m log m)), Prim's (vertex-based O((n+m) log n)).

**Concept 4: Maximum Flow**  
Route maximum flow source→sink respecting capacities. Ford-Fulkerson simple, Edmonds-Karp polynomial.

**Concept 5: Flow Duality**  
Max-flow = min-cut. Use flow for matching, segmentation, circulation. Unified framework for diverse problems.

---

## 🔄 Recommended Learning Path

**Each Day (2.5 hours):**
- Morning (75 min): Read instructional, trace examples, understand mechanics
- Afternoon (45 min): Solve 3-4 problems, implement from scratch
- Evening (30 min): Review checklist, rate confidence, algorithm selection

**Weekend (2-3 hours):**
- Review all 5 algorithms
- Solve mixed problems requiring algorithm selection
- Answer all 40+ interview Q&A pairs
- Complete integration checklist

---

## ⚠️ Common Mistakes to Avoid

**Mistake 1: "Dijkstra's for negative weights"**  
Reality: Fails with negative weights. Use Bellman-Ford instead.

**Mistake 2: "Floyd-Warshall always best"**  
Reality: O(n³) too slow for large n. Use Dijkstra's for single-source unless negatives.

**Mistake 3: "Kruskal's always faster"**  
Reality: Depends on density. Sparse: Kruskal's O(m log m). Dense: Prim's O((n+m) log n).

**Mistake 4: "Ford-Fulkerson always fast"**  
Reality: O(flow × m) inefficient. Use Edmonds-Karp O(nm²) for guarantee.

**Mistake 5: "Flow only for transportation"**  
Reality: Solves matching, segmentation, circulation. Unified framework.

---

## 🎓 Practice Problems Guide

### Dijkstra's (4+ problems)
1. Shortest path weighted
2. Network delay time
3. Path with maximum probability
4. Swim in rising water

### Bellman-Ford & Floyd-Warshall (4+ problems)
1. Cheapest flights with k stops
2. Arbitrage detection
3. All pairs shortest path
4. Minimum cost path

### MST (4+ problems)
1. Minimum spanning tree (Kruskal's)
2. Minimum spanning tree (Prim's)
3. Redundant connections
4. Minimum cost to connect

### Network Flow I (4+ problems)
1. Maximum network flow
2. Maximal network rank
3. Network flow maximum path value
4. Optimal account balancing

### Network Flow II (4+ problems)
1. Bipartite matching
2. Image largest island
3. Minimum cut networks
4. Project selection

---

## 💼 Interview Preparation

**Week 7 Coverage:** 10-12% of interview problems (cumulative 90-95%)

**Interview Strategy:**
1. Identify problem type (shortest path? spanning? flow?)
2. Check constraints (negative weights? all-pairs? capacities?)
3. Match algorithm (Dijkstra? Bellman-Ford? Floyd-Warshall? MST? Flow?)
4. Implement cleanly with proper data structures
5. Explain complexity and real-world applications

**When Week 7 Matters Most:**
- Advanced graph problems (20-25% of interviews)
- System design (routing, networks, matching)
- Optimization problems
- Hard LeetCode problems

---

## 🔗 Connection to Other Weeks

**Week 6:** Graph fundamentals (BFS, DFS, topological sort)  
**Week 7:** Weighted graphs and flow (THIS WEEK)  
**Week 8:** Advanced topics (combining multiple weeks)

---

## ❓ Frequently Asked Questions

**Q: When use Dijkstra's vs Bellman-Ford?**
A: Dijkstra's faster O((n+m) log n) for non-negative. Bellman-Ford O(nm) for negative weights.

**Q: When use Kruskal's vs Prim's?**
A: Kruskal's better sparse graphs (m << n²). Prim's better dense (m ≈ n²).

**Q: Is Floyd-Warshall ever better?**
A: For small graphs (n < 500) all-pairs. O(n³) practical. Not for large n.

**Q: Why is Edmonds-Karp better than Ford-Fulkerson?**
A: Ford-Fulkerson O(flow × m) depends on flow. Edmonds-Karp O(nm²) polynomial guarantee.

**Q: Can I use flow for bipartite matching?**
A: YES! Model as flow network. Simpler than Hungarian algorithm.

**Q: What's integrality property?**
A: If capacities integer, max-flow has integer value on each edge.

---

## ✅ Before Proceeding to Week 8

- [ ] Rate 4/5+ on all 5 algorithms
- [ ] Can implement Dijkstra's and Bellman-Ford
- [ ] Can implement Kruskal's and Prim's MST
- [ ] Can implement Ford-Fulkerson/Edmonds-Karp
- [ ] Can solve bipartite matching via flow
- [ ] Can solve basic min-cut problems
- [ ] Understand when to use each algorithm
- [ ] Recognize real-world applications

