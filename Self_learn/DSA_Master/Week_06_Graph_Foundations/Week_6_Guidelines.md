# Week 6 (Graph Foundations): Guidelines

## 📅 Daily Breakdown & Time Allocation

**Total Week:** 12-14 hours (2.4-2.8 hours per day)

| Day | Topic | Time | Focus | Coverage |
|-----|-------|------|-------|----------|
| **1** | Graph Representations | 2.5h | Matrix vs List, density trade-offs | — |
| **2** | Breadth-First Search (BFS) | 2.5h | Level-order, shortest path unweighted | 5-8% |
| **3** | Depth-First Search (DFS) | 2.5h | Deep exploration, topological foundation | 5-8% |
| **4** | Topological Sort | 2.5h | DAG ordering, dependency resolution | 3-5% |
| **5** | Union-Find | 2.5h | Disjoint sets, O(α(n)) amortized | 3-5% |
| **Weekend** | Integration & Review | 2-3h | Pattern combinations, MST | — |

**Total:** 12-14 hours, 5 fundamental graph algorithms

---

## 🎯 Learning Objectives

### By End of Week 6
- [ ] Understand graph representations and choose wisely
- [ ] Master BFS for shortest paths (unweighted)
- [ ] Master DFS for exploration and topological sort
- [ ] Implement topological sort (DFS and Kahn's)
- [ ] Implement Union-Find with path compression and rank
- [ ] Recognize which algorithm fits each graph problem
- [ ] Understand real-world applications (npm, Gradle, etc.)
- [ ] Solve 88-98% of interview problems (cumulative)

---

## 📚 Core Concepts

**Concept 1: Representation Matters**  
Adjacency matrix O(n²) vs list O(n+m). Density determines choice.

**Concept 2: Traversal Algorithms**  
BFS level-by-level, DFS deep exploration. Different properties, both O(n+m).

**Concept 3: Dependency Ordering**  
Topological sort for DAGs. DFS post-order or Kahn's algorithm.

**Concept 4: Dynamic Connectivity**  
Union-Find maintains connected components with near-O(1) operations.

---

## 🔄 Recommended Learning Path

**Each Day (2.5 hours):**
- Morning (75 min): Read instructional, trace examples, understand mechanics
- Afternoon (45 min): Solve 3-4 problems, implement from scratch
- Evening (30 min): Review checklist, rate confidence, compare algorithms

**Weekend (2-3 hours):**
- Review all 5 algorithms
- Solve mixed problems requiring algorithm selection
- Answer all 25+ interview Q&A pairs
- Complete integration checklist

---

## ⚠️ Common Mistakes to Avoid

**Mistake 1: "Use BFS for everything"**  
Reality: BFS for shortest path unweighted. DFS for topological sort, cycles.

**Mistake 2: "Adjacency matrix always slow"**  
Reality: O(n²) acceptable for dense graphs or small n.

**Mistake 3: "Topological sort only for DAGs"**  
Reality: True. Cycles make it undefined. Must verify no cycles first.

**Mistake 4: "Union-Find is slow"**  
Reality: O(α(n)) ≈ O(1) amortized with path compression + rank. Near-optimal.

**Mistake 5: "DFS not useful, BFS better"**  
Reality: Different properties. DFS for dependencies, BFS for distance.

---

## 🎓 Practice Problems Guide

### Graph Representations (4+ problems)
1. Build adjacency list from edges
2. Build adjacency matrix
3. Convert between representations
4. Count edges/vertices

### BFS (8+ problems)
1. Shortest path unweighted
2. Nodes at distance k
3. Connected components (BFS variant)
4. Bipartite graph checking
5. Word ladder (shortest path variant)
6. Maze solving
7. Level-order traversal
8. All shortest paths

### DFS (8+ problems)
1. DFS traversal
2. Cycle detection
3. Connected components
4. Number of islands (DFS)
5. Path exists (DFS)
6. All paths from source to target
7. Course schedule (topological sort variant)
8. Backtracking problems

### Topological Sort (5+ problems)
1. Topological sort (DFS-based)
2. Topological sort (Kahn's)
3. Course schedule validity
4. Build order dependencies
5. Alien dictionary

### Union-Find (6+ problems)
1. Implement Union-Find
2. Cycle detection (undirected)
3. Kruskal's MST
4. Connected components dynamic
5. Percolation threshold
6. Image connected components

---

## 💼 Interview Preparation

**Week 6 Coverage:** 8-10% of interview problems (cumulative 88-98%)

**Interview Strategy:**
1. Identify graph problem type (shortest path? dependencies? connectivity?)
2. Check if directed/undirected, weighted/unweighted
3. Choose algorithm (BFS? DFS? Topological? Union-Find?)
4. Implement cleanly with proper graph representation
5. Explain time/space complexity and real-world use

**When Week 6 Matters Most:**
- Graph problems (15-20% of interviews)
- Hard problems combining algorithms
- System design (network topology, dependency graphs)
- Real-world systems (npm, Gradle, databases)

---

## 🔗 Connection to Other Weeks

**Week 5:** Trees are special graphs (connected, acyclic)  
**Week 5.5:** Optimization patterns apply to graphs  
**Week 6:** Graph fundamentals, traversal, sorting  
**Week 7+:** Advanced (MST, shortest path, flows)

---

## ❓ Frequently Asked Questions

**Q: Why both BFS and DFS if both O(n+m)?**
A: Different properties. BFS guarantees shortest unweighted, DFS natural for recursion and topological sort.

**Q: When use topological sort vs BFS/DFS?**
A: Topological sort for dependencies (DAGs only). BFS/DFS for general traversal.

**Q: Is Union-Find really O(1)?**
A: O(α(n)) amortized, which ≈ O(1) for practical sizes (α(2^65536) ≈ 4).

**Q: How know if graph has cycle?**
A: DFS (back edge), or Union-Find (Find(u) == Find(v) before union).

**Q: Can use BFS for weighted graphs?**
A: BFS only guarantees shortest for unweighted. Dijkstra's for weighted.

**Q: Is Kruskal's better than Prim's?**
A: Different trade-offs. Kruskal's O(m log m) with sorting/union-find. Prim's O(n²) or O((n+m) log n).

---

## ✅ Before Proceeding to Week 7

- [ ] Rate 4/5+ on all 5 graph algorithms
- [ ] Can implement BFS and DFS from memory
- [ ] Can do topological sort (DFS and Kahn's)
- [ ] Can implement Union-Find with optimizations
- [ ] Understand when to use each algorithm
- [ ] Recognize real-world applications

