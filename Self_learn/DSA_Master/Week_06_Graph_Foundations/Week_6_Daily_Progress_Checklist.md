# Week 6: Daily Progress Checklist & Interview Q&A

## ✅ DAY 1: Graph Representations

### Morning Objectives
- [ ] Understand adjacency matrix (O(n²) space, O(1) lookup)
- [ ] Understand adjacency list (O(n+m) space, O(degree) lookup)
- [ ] Know trade-offs: density vs operation type
- [ ] Identify representation from problem constraints

### Core Learning
- [ ] Read: Week_6_Day_1_Graph_Representations_Instructional.md
- [ ] Trace: Build matrix and list from same edges
- [ ] Trace: Convert matrix ↔ list
- [ ] Understand: When choose each representation

### Practice Problems
- [ ] Build adjacency list from edges
- [ ] Build adjacency matrix
- [ ] Convert matrix to list
- [ ] Count edges/vertices

**Confidence Rating**: ___ / 5

---

## ✅ DAY 2: Breadth-First Search (BFS)

### Morning Objectives
- [ ] Understand level-by-level exploration
- [ ] Know BFS guarantees shortest path (unweighted only)
- [ ] Understand queue (FIFO) requirement
- [ ] Know O(n+m) time, O(n) space

### Core Learning
- [ ] Read: Week_6_Day_2_Breadth_First_Search_Instructional.md
- [ ] Trace: BFS from source, mark distances
- [ ] Trace: Path reconstruction via parent
- [ ] Understand: Why FIFO queue essential

### Practice Problems
- [ ] Shortest path unweighted
- [ ] Nodes at distance k
- [ ] Bipartite checking
- [ ] Connected components

**Confidence Rating**: ___ / 5

---

## ✅ DAY 3: Depth-First Search (DFS)

### Morning Objectives
- [ ] Understand deep exploration
- [ ] Know pre-order and post-order
- [ ] Understand DFS for cycles and topological foundation
- [ ] Understand recursive vs iterative

### Core Learning
- [ ] Read: Week_6_Day_3_Depth_First_Search_Instructional.md
- [ ] Trace: DFS pre/post-order
- [ ] Trace: Cycle detection via back edges
- [ ] Understand: Post-order for topological

### Practice Problems
- [ ] DFS traversal
- [ ] Cycle detection
- [ ] Connected components
- [ ] All paths from source to target

**Confidence Rating**: ___ / 5

---

## ✅ DAY 4: Topological Sort

### Morning Objectives
- [ ] Understand DAG requirement (no cycles)
- [ ] Know DFS post-order method
- [ ] Know Kahn's algorithm (in-degree approach)
- [ ] Understand cycle detection via topological

### Core Learning
- [ ] Read: Week_6_Day_4_Topological_Sort_Instructional.md
- [ ] Trace: DFS-based topological sort
- [ ] Trace: Kahn's algorithm
- [ ] Understand: Why must verify DAG

### Practice Problems
- [ ] Topological sort (DFS)
- [ ] Topological sort (Kahn's)
- [ ] Course schedule
- [ ] Alien dictionary

**Confidence Rating**: ___ / 5

---

## ✅ DAY 5: Union-Find

### Morning Objectives
- [ ] Understand parent pointers
- [ ] Know path compression optimization
- [ ] Know union by rank optimization
- [ ] Understand O(α(n)) amortized ≈ O(1)

### Core Learning
- [ ] Read: Week_6_Day_5_Union_Find_Instructional.md
- [ ] Trace: Union-Find operations
- [ ] Trace: Path compression
- [ ] Understand: Why path compression speeds up

### Practice Problems
- [ ] Implement Union-Find
- [ ] Cycle detection
- [ ] Connected components dynamic
- [ ] Kruskal's MST

**Confidence Rating**: ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (25+ Pairs)

### Graph Representations (5 pairs)

**Q1: When use adjacency matrix vs list?**
A: Matrix: O(n²) space, O(1) lookup. List: O(n+m) space, O(degree) lookup. Choose based on density and operations.

**Q2: Why does matrix use O(n²) space even for sparse graphs?**
A: Allocates full n×n even if few edges. For sparse (m << n²), list better.

**Q3: Can convert between matrix and list?**
A: Yes. Matrix→List: scan rows. List→Matrix: allocate, fill from lists.

**Q4: What if undirected? Directed?**
A: Undirected: symmetric (both matrix[u][v] and matrix[v][u]). Directed: only matrix[u][v].

**Q5: For weighted graphs?**
A: Matrix stores weight. List stores (neighbor, weight) pairs.

---

### BFS (5 pairs)

**Q1: Why queue (FIFO) not stack (LIFO)?**
A: Queue processes level-by-level. Stack would go deep (DFS). FIFO essential for level-order.

**Q2: Does BFS find shortest path in weighted graph?**
A: NO, only unweighted. Use Dijkstra's for weighted.

**Q3: Why mark visited before adding to queue?**
A: Prevents revisiting and adding multiple times (quadratic time). Mark immediately after discovery.

**Q4: How reconstruct path from BFS?**
A: Track parent[v] = u when discovering v. Backtrack from target to source.

**Q5: Complexity: why O(n+m) not O(n×m)?**
A: Each vertex enqueued once, dequeued once. Each edge examined once. Total linear.

---

### DFS (5 pairs)

**Q1: Recursive vs iterative DFS?**
A: Recursive: cleaner code, stack overflow risk on deep graphs. Iterative: explicit stack, safe.

**Q2: How detect cycles in DFS?**
A: Directed: back edge (edge to ancestor) indicates cycle. Undirected: back edge to parent.

**Q3: Pre-order vs post-order?**
A: Pre-order: when entering node. Post-order: when leaving node. Use post-order for topological.

**Q4: Space complexity O(height) or O(width)?**
A: O(height) for recursion stack, O(width) for iterative stack. Usually better than BFS.

**Q5: When use DFS over BFS?**
A: Topological sort, cycle detection, connected components, memory constraint (height < width).

---

### Topological Sort (5 pairs)

**Q1: Why topological sort only for DAGs?**
A: Cycles make ordering impossible. Dependencies undefined. Must have acyclic structure.

**Q2: How verify graph is DAG before topological?**
A: Run DFS, detect back edges. Or run Kahn's, check |output| == n.

**Q3: DFS post-order vs Kahn's?**
A: DFS: recursive, clean. Kahn's: iterative, explicit in-degree tracking. Both O(n+m).

**Q4: Multiple valid topological orderings?**
A: YES. Any ordering respecting dependencies is valid. Problem may have many solutions.

**Q5: Real-world: npm dependencies?**
A: Dependency graph is DAG. Topological sort gives install order respecting dependencies.

---

### Union-Find (5+ pairs)

**Q1: How does path compression speed up find?**
A: Redirect nodes directly to root during find. Subsequent finds short-circuit to root.

**Q2: Why union by rank?**
A: Attaches smaller tree under larger, keeping height O(log n) max. Ensures find is O(log n) amortized.

**Q3: Together (compression + rank): O(α(n))?**
A: YES. Inverse Ackermann: α(n) ≈ 4 for all practical n. Nearly O(1).

**Q4: How detect cycle in undirected graph?**
A: For each edge (u,v): if find(u) == find(v), cycle exists. Else union(u,v).

**Q5: Kruskal's MST with Union-Find?**
A: Sort edges by weight. For each edge, union endpoints if different sets (no cycle). Select n-1 edges.

**Q6: Why Union-Find better than DFS for cycle detection?**
A: Union-Find O(α(n)) incremental, DFS O(n+m) from scratch. For dynamic graphs, Union-Find wins.

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Implementation | Confidence |
|-----|-------|---|---|---|
| **1** | Graph Representations | ___ | ___ | ___ / 5 |
| **2** | BFS | ___ | ___ | ___ / 5 |
| **3** | DFS | ___ | ___ | ___ / 5 |
| **4** | Topological Sort | ___ | ___ | ___ / 5 |
| **5** | Union-Find | ___ | ___ | ___ / 5 |

**Target:** 4/5+ on all before Week 7

---

## ✅ WEEK 6 COMPLETION CHECKLIST

### Knowledge Check
- [ ] Can explain all 5 algorithms and when to use
- [ ] Understand representation trade-offs
- [ ] Know complexity for each algorithm
- [ ] Can recognize patterns in problems

### Skills Check
- [ ] Can implement BFS from scratch
- [ ] Can implement DFS from scratch
- [ ] Can implement topological sort (both methods)
- [ ] Can implement Union-Find with optimizations
- [ ] Can choose algorithm for problem
- [ ] Can solve algorithm variants

---

## 📈 Week 6 Summary

**Time:** ~12-14 hours  
**Topics:** 5 graph fundamentals  
**Problems:** 40+  
**Coverage:** +8-10% (cumulative 88-98%)

**Ready for Week 7 (Advanced Graphs)?** YES / NO

