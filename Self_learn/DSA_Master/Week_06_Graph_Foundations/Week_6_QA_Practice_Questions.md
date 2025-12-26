# Week 6: Q&A Practice Questions (12 Per Day)

**Total Questions:** 60 (12 × 5 days)  
**Difficulty Range:** ⭐ Easy to ⭐⭐⭐ Hard  

---

## 📍 DAY 1: GRAPH REPRESENTATIONS (12 Questions)

**Q1 ⭐:** When would you use adjacency matrix?
A: For dense graphs (>20% edges) or when O(1) edge lookup critical.

**Q2 ⭐:** What's the space complexity of adjacency list?
A: O(n+m) where n = vertices, m = edges.

**Q3 ⭐:** Why is adjacency list preferred in most algorithms?
A: BFS/DFS are O(n+m) with list, O(n²) with matrix.

**Q4 ⭐⭐:** For graph with 1000 nodes, 5000 edges, which is better?
A: Adjacency list. 5000 edges << 1,000,000 (matrix).

**Q5 ⭐⭐:** How do you add edge u-v in both representations?
A: Matrix: O(1) update. List: O(1) append.

**Q6 ⭐⭐:** Can you check edge existence in O(1) with adjacency list?
A: No, you need O(degree) search. This is a trade-off.

**Q7 ⭐⭐:** What if graph is weighted?
A: Both store weights. Matrix: matrix[u][v]=weight. List: append (v,weight).

**Q8 ⭐⭐:** How to iterate all edges efficiently?
A: Adjacency list: O(n+m). Matrix: O(n²) (must check all).

**Q9 ⭐⭐⭐:** For complete graph (all edges), which is better?
A: Matrix (O(n²) space same as O(n²) edges).

**Q10 ⭐⭐⭐:** Convert adjacency matrix to list. Time?
A: O(n²) for matrix traversal + O(n+m) for list building = O(n²).

**Q11 ⭐⭐⭐:** Memory for adjacency matrix with 10⁶ nodes?
A: 10¹² entries, ~1TB! Clearly impractical for sparse graphs.

**Q12 ⭐⭐⭐:** Which representation works better for sparse + dynamic graphs?
A: Adjacency list (easier insertions/deletions).

---

## 📍 DAY 2: BFS (12 Questions)

**Q1 ⭐:** What data structure does BFS use?
A: Queue (FIFO). Process nodes in order visited.

**Q2 ⭐:** Why does BFS find shortest path?
A: Explores level-by-level. First visit = shortest distance.

**Q3 ⭐:** Time complexity of BFS?
A: O(V+E) where V=vertices, E=edges.

**Q4 ⭐⭐:** BFS from node 1 in graph with 1-2, 1-3, 2-4. What's distance to 4?
A: Distance = 2 (path 1→2→4).

**Q5 ⭐⭐:** Why mark visited immediately, not when popping?
A: To avoid adding duplicate nodes to queue.

**Q6 ⭐⭐:** Does BFS work on weighted graphs?
A: No, weights are ignored. Use Dijkstra for weighted.

**Q7 ⭐⭐:** What if start node not reachable to some nodes?
A: BFS only visits reachable nodes (returns partial result).

**Q8 ⭐⭐:** How to reconstruct path in BFS?
A: Store parent pointers during traversal.

**Q9 ⭐⭐⭐:** BFS vs DFS for finding shortest path?
A: BFS guarantees shortest. DFS finds path but not necessarily shortest.

**Q10 ⭐⭐⭐:** Find minimum edges to connect two nodes?
A: BFS distance between them.

**Q11 ⭐⭐⭐:** Can BFS find bipartite graph?
A: Yes, color nodes as BFS explores (alternating colors).

**Q12 ⭐⭐⭐:** Compare queue vs stack for graph traversal?
A: Queue = BFS (level-by-level). Stack = DFS (deep first).

---

## 📍 DAY 3: DFS (12 Questions)

**Q1 ⭐:** What data structure does DFS use?
A: Stack (LIFO), either explicit or recursion stack.

**Q2 ⭐:** Can DFS find shortest path?
A: Not necessarily. It finds a path but not shortest.

**Q3 ⭐:** Time complexity of DFS?
A: O(V+E) same as BFS.

**Q4 ⭐⭐:** DFS from node 1 in graph with 1-2, 1-3, 2-4. Visit order?
A: 1 → 2 → 4 → [backtrack] → 3 (or 1 → 3 → [backtrack] → 2 → 4).

**Q5 ⭐⭐:** What indicates a cycle in undirected graph with DFS?
A: Visiting a node already in current path (back edge).

**Q6 ⭐⭐:** How does DFS handle cycles?
A: Mark visited to avoid revisiting. Cycles naturally handled.

**Q7 ⭐⭐:** What's call stack depth for DFS?
A: Up to V (height of graph as tree). Could cause stack overflow.

**Q8 ⭐⭐:** Recursive vs iterative DFS?
A: Recursive is simpler but risks stack overflow. Iterative is safer.

**Q9 ⭐⭐⭐:** How to detect cycle in directed graph with DFS?
A: Track nodes in current recursion path (recursion stack).

**Q10 ⭐⭐⭐:** What's finishing order in DFS?
A: Order nodes finish (when all neighbors explored).

**Q11 ⭐⭐⭐:** Use DFS to find connected components. How?
A: DFS from each unvisited node creates one component.

**Q12 ⭐⭐⭐:** DFS vs BFS for backtracking problems?
A: DFS natural (recursion = backtrack). BFS awkward.

---

## 📍 DAY 4: TOPOLOGICAL SORT (12 Questions)

**Q1 ⭐:** What does topological sort order?
A: Nodes such that all dependencies come before dependents.

**Q2 ⭐:** When does topological sort work?
A: Only on DAGs (directed acyclic graphs).

**Q3 ⭐:** What happens if graph has cycle?
A: No valid topological order exists.

**Q4 ⭐⭐:** How does DFS-based topological sort work?
A: Reverse of DFS finishing order.

**Q5 ⭐⭐:** Given dependencies 1→2, 2→3, what's topo order?
A: 1, 2, 3 (or any order respecting dependencies).

**Q6 ⭐⭐:** What's Kahn's algorithm?
A: BFS-based: process nodes with in-degree 0, decrement neighbors.

**Q7 ⭐⭐:** Advantage of Kahn's over DFS-based?
A: Naturally detects cycles (queue becomes empty before all processed).

**Q8 ⭐⭐:** Can there be multiple valid topological sorts?
A: Yes, any order respecting dependencies is valid.

**Q9 ⭐⭐⭐:** Is topological order unique for all DAGs?
A: No, only for DAGs with linear dependency structure.

**Q10 ⭐⭐⭐:** Use topological sort for course ordering. How?
A: Nodes = courses, edges = prerequisites, topo order = enrollment sequence.

**Q11 ⭐⭐⭐:** How to detect cycle using topological sort?
A: If topo sort returns fewer than V nodes, cycle exists.

**Q12 ⭐⭐⭐:** Time complexity of topological sort?
A: O(V+E) for both DFS-based and Kahn's.

---

## 📍 DAY 5: UNION-FIND (12 Questions)

**Q1 ⭐:** What does Union-Find do?
A: Manages disjoint sets, supports fast union and find operations.

**Q2 ⭐:** What's the find operation?
A: Returns representative (root) of set containing node.

**Q3 ⭐:** What's the union operation?
A: Merges two sets by connecting their roots.

**Q4 ⭐⭐:** Why start with parent[i] = i?
A: Each node initially its own set representative.

**Q5 ⭐⭐:** What does path compression do?
A: When finding root, update all nodes to point directly to root.

**Q6 ⭐⭐:** Why does path compression help?
A: Next find on same node is O(1).

**Q7 ⭐⭐:** What does union by rank do?
A: Attaches smaller tree under larger to keep trees shallow.

**Q8 ⭐⭐⭐:** Both optimizations together give what complexity?
A: O(α(n)) ≈ O(1) amortized, where α = inverse Ackermann.

**Q9 ⭐⭐⭐:** Detect cycle in undirected graph with Union-Find. How?
A: If union(u,v) fails (already same set), there's a cycle.

**Q10 ⭐⭐⭐:** Find connected components using Union-Find. How?
A: For each edge, union nodes. Connected nodes = same root.

**Q11 ⭐⭐⭐:** Why Union-Find better than BFS for components?
A: O(α(n)) much faster than O(V+E) when m << V.

**Q12 ⭐⭐⭐:** Kruskal's MST uses Union-Find. Why?
A: Efficiently track connected components while adding edges.

---

## 📊 SELF-ASSESSMENT SCORING

- **50-60 correct:** Master level (proceed to Week 7)
- **45-49 correct:** Advanced level (ready, review weak areas)
- **40-44 correct:** Solid level (practice more)
- **<40 correct:** Review needed (extend current week)

---

**Q&A Version:** 1.0 Week 6 Complete

