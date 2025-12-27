# Week 6: Interview Q&A Reference

## 🎯 Comprehensive Interview Q&A (25+ Pairs)

### Graph Representations — 5 Pairs

**Q1: When should you use adjacency matrix vs adjacency list?**
A: Use matrix for dense graphs (m ≈ n²) or when O(1) edge lookup critical. Use list for sparse graphs (m << n²) to save O(n²) space.

**Q2: Why does adjacency matrix allocate O(n²) even for sparse graphs?**
A: Fixed 2D array allocation. For 1000 vertices with 1000 edges: matrix wastes 1M cells, list uses 1000+2000 = 3000. ~300x difference!

**Q3: How do you handle undirected graphs in both representations?**
A: Matrix: both matrix[u][v] and matrix[v][u] set (symmetric). List: add v to list[u] AND u to list[v].

**Q4: Can you convert from adjacency matrix to list efficiently?**
A: YES. Scan matrix, for each non-zero entry, add to list. O(n²) time (must scan all). OR store only non-zero in list upfront.

**Q5: For weighted graphs, how store weights?**
A: Matrix: matrix[u][v] = weight. List: each element is (neighbor, weight) pair.

---

### BFS — 5 Pairs

**Q1: Why does BFS guarantee shortest path only in unweighted graphs?**
A: BFS explores level-by-level. All distance k before k+1. Weights break this: shorter weighted path at higher hop count.

**Q2: Why use queue (FIFO) instead of stack (LIFO) for BFS?**
A: Queue preserves level-order (process all distance k before k+1). Stack goes deep (DFS). FIFO essential for level-by-level property.

**Q3: When marking visited, should you mark before or after dequeuing?**
A: Mark BEFORE adding to queue. Prevents enqueueing same vertex multiple times from different neighbors. Saves time and space.

**Q4: How do you reconstruct the actual path in BFS, not just distance?**
A: Store parent[v] = u when discovering v from u. Backtrack: current = target, while current != start: path.prepend(current), current = parent[current].

**Q5: Why is BFS time complexity O(n+m) and not O(n×m)?**
A: Each vertex enqueued once, dequeued once. Each edge examined once when processing its source vertex. Total: n enqueues + n dequeues + m edge checks = O(n+m).

---

### DFS — 5 Pairs

**Q1: When should you use recursive vs iterative DFS?**
A: Recursive: cleaner code, natural recursion. Iterative: explicit stack, safer for deep graphs (avoid stack overflow). Python has ~1000 limit.

**Q2: How do you detect cycles using DFS?**
A: Directed: if DFS edge goes to ancestor (already visiting), it's back edge = cycle. Undirected: if edge to visited node (except parent), it's back edge = cycle.

**Q3: What's the difference between pre-order and post-order in DFS?**
A: Pre-order: when entering node (start processing). Post-order: when leaving node (finished processing). Post-order used for topological sort.

**Q4: Is DFS space complexity O(height) or O(width)?**
A: Recursive DFS: O(height) call stack (worst case O(n) for chain). Iterative DFS: O(width) explicit stack. May differ from BFS.

**Q5: When would you prefer DFS over BFS despite same O(n+m) complexity?**
A: Topological sort (natural with DFS post-order), cycle detection, stack constraints (height < width), memory-constrained systems.

---

### Topological Sort — 5 Pairs

**Q1: Why can't you do topological sort on graphs with cycles?**
A: Topological sort orders vertices respecting dependencies. Cycles have no valid ordering (dependency loop). Must be acyclic (DAG).

**Q2: How do you verify a directed graph is a DAG before topological sort?**
A: Run DFS, look for back edges (edges to ancestors). If found, has cycle. OR run Kahn's algorithm, check if |output| == n.

**Q3: What's the relationship between DFS post-order and topological order?**
A: Reverse of post-order IS a topological sort. Why: if edge u→v, DFS finishes v before u, so u comes after v in post-order, before in reverse.

**Q4: Can there be multiple valid topological orderings for same DAG?**
A: YES. Any ordering respecting all dependencies is valid. Kahn's may produce different result than DFS depending on queue/stack order.

**Q5: How does npm or Gradle use topological sort for dependencies?**
A: Dependency graph is DAG (no circular dependencies). Topological sort gives valid installation/build order respecting all dependencies.

---

### Union-Find — 5+ Pairs

**Q1: How does path compression optimize the find operation?**
A: During find(x), redirect parent[x] directly to root (parent[x] = find(parent[x])). Subsequent finds of x or its ancestors short-circuit to root. Amortized huge speedup.

**Q2: Why is union by rank necessary if you have path compression?**
A: Path compression alone doesn't guarantee O(log n) find (tree can be tall). Union by rank keeps tree height balanced O(log n). Together: O(α(n)) amortized.

**Q3: What's the Ackermann inverse α(n), and why is it nearly constant?**
A: Inverse of Ackermann function. Grows incredibly slowly: α(2^65536) ≈ 4. For practical n, α(n) ≤ 5. So O(α(n)) ≈ O(1).

**Q4: How do you detect cycles in an undirected graph using Union-Find?**
A: For each edge (u,v): if find(u) == find(v), cycle found (same component already). Otherwise: union(u,v) to merge components.

**Q5: How does Kruskal's MST algorithm use Union-Find?**
A: Sort edges by weight. For each edge (u,v): if find(u) != find(v), it's safe (no cycle), add to MST and union(u,v). Continue until n-1 edges added.

**Q6: Why is Union-Find faster than DFS for cycle detection in dynamic graphs?**
A: Union-Find: O(α(n)) per edge operation. DFS: O(n+m) each time. If adding edges incrementally, Union-Find amortized better (no restart).

---

## ✅ Interview Readiness Check

After Week 6, confidently answer:
- [ ] 5 graph representation questions
- [ ] 5 BFS questions
- [ ] 5 DFS questions
- [ ] 5 topological sort questions
- [ ] 6 Union-Find questions

**Total: 26 Q&A pairs mastered**

**If 90%+ confident → Ready for Week 7+**

