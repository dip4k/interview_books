# Week 7: Summary & Key Concepts

## 📖 Week 7 Overview

Advanced Graph Algorithms teaches **5 powerful algorithms** for weighted graphs and network flow. Builds on Week 6 fundamentals. Covers shortest paths, spanning trees, and flow networks.

---

## 📊 Algorithm Comparison Table

| Algorithm | Problem | Time | Space | When |
|-----------|---------|------|-------|------|
| **Dijkstra's** | Shortest path (non-negative) | O((n+m) log n) | O(n) | Greedy, single-source |
| **Bellman-Ford** | Shortest path (negative weights) | O(n×m) | O(n) | Negative detection |
| **Floyd-Warshall** | All-pairs shortest path | O(n³) | O(n²) | Small dense graphs |
| **Kruskal's MST** | Minimum spanning tree | O(m log m) | O(n+m) | Sparse graphs |
| **Prim's MST** | Minimum spanning tree | O((n+m) log n) | O(n) | Dense graphs |
| **Ford-Fulkerson** | Maximum network flow | O(flow × m) | O(n²) | Simple, integer flows |
| **Edmonds-Karp** | Maximum network flow | O(n × m²) | O(n²) | Polynomial guaranteed |

---

## 🧠 Key Insights

### Insight 1: Weight Changes Everything
Unweighted (Week 6) vs weighted (Week 7) completely different algorithms. Dijkstra's greedy, BFS level-by-level.

### Insight 2: Trade-offs Matter
Dijkstra's fast but non-negative only. Bellman-Ford slower but handles negatives. Floyd-Warshall simplest all-pairs, O(n³).

### Insight 3: Greedy Guaranteed for Graphs
Both Kruskal's and Prim's greedy but guaranteed optimal MST. Graph structure allows greedy.

### Insight 4: Flow Unifies Problems
Max-flow solves matching, min-cut, circulation. Single framework for diverse problems.

### Insight 5: Complexity Matters at Scale
Dijkstra O((n+m) log n) vs Bellman-Ford O(n×m) huge difference for large graphs. Choose wisely.

---

## ❌ Common Misconceptions Fixed

### ❌ "Dijkstra's always faster"
✅ **Reality:** Faster for non-negative. Bellman-Ford needed for negatives.

### ❌ "Floyd-Warshall best for all-pairs"
✅ **Reality:** O(n³) only practical for small n. Repeated Dijkstra's better for sparse.

### ❌ "Kruskal's always simpler"
✅ **Reality:** Simpler code, but Prim's better for dense graphs.

### ❌ "Ford-Fulkerson always efficient"
✅ **Reality:** O(flow × m) can be slow. Edmonds-Karp polynomial.

### ❌ "Flow only for transportation"
✅ **Reality:** Solves matching, segmentation, optimization, and more.

---

## 📈 Mastery Progression

### Level 1: Recognition (Day 1-2)
- Identify shortest path problems
- Know algorithm names and complexities
- Understand when each applies

### Level 2: Understanding (Days 2-4)
- Explain WHY algorithm works
- Understand greedy/DP approaches
- Know preconditions and constraints

### Level 3: Application (Days 4-5)
- Implement from scratch
- Solve problem variants
- Combine with other techniques
- Recognize patterns

### Level 4: Mastery (Week 8+)
- Teach others
- Optimize for real constraints
- Choose algorithm for trade-offs
- Apply to novel problems

---

## 🔗 Week 7 → Week 8+ Connections

**Week 8:** Advanced topics, combining multiple weeks  
**Competitive Programming:** Shortest paths, flows, MST foundation  
**System Design:** Routing algorithms, network optimization  
**Machine Learning:** MST clustering, min-cut segmentation

---

## ✨ Week 7 Key Takeaway

> **Master 5 advanced algorithms: Dijkstra's (weighted shortest) → Bellman-Ford/Floyd-Warshall (negatives/all-pairs) → MST (Kruskal's/Prim's) → Network Flow (Ford-Fulkerson/Edmonds-Karp) → Applications (matching, min-cut, circulation). Together: handle 90-95% of graph interview problems.**

---

**Cumulative (Weeks 1-7):** 90-95% interview coverage

