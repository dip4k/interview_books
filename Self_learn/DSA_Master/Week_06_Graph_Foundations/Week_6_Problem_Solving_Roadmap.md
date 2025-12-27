# Week 6: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for ALL Week 6 problems:**

1. **Analyze** graph structure (directed? weighted? cycles?)
2. **Classify** problem type (shortest path? ordering? connectivity?)
3. **Match** algorithm (BFS? DFS? Topological? Union-Find?)
4. **Choose** representation (matrix or list?)
5. **Implement** with proper data structures

---

## 🎯 Pattern Decision Tree

```
Is it a shortest path problem?
├─ YES, unweighted? → BFS
├─ YES, weighted? → Dijkstra's (Week 7)
└─ NO → Continue

Is it a dependency/ordering problem?
├─ YES → Topological Sort (verify DAG first!)
└─ NO → Continue

Is it a connectivity/cycle problem?
├─ YES, undirected cycle? → Union-Find or DFS
├─ YES, directed cycle? → DFS only
└─ NO → Continue

Need all nodes at distance k?
├─ YES → BFS with level tracking
└─ NO → Continue

Exploring graph properties (traversal)?
├─ Need specific order → DFS or BFS
└─ Any order → Either works
```

---

## 🌳 Algorithm-Specific Roadmaps

### BFS Roadmap (Shortest Path Unweighted)

**When:** Shortest path, level-order, unweighted graph

**Template:**
```
1. graph = adjacency list
2. queue = [start]
3. visited = {start}, distance = {start: 0}
4. While queue:
     u = queue.pop_front()
     For each neighbor v:
       if v not visited:
         visited.add(v)
         distance[v] = distance[u] + 1
         queue.push_back(v)
5. Return distance[target]
```

**Examples:** Shortest path, maze, word ladder

---

### DFS Roadmap (Exploration, Cycles, Topological)

**When:** Explore, detect cycles, topological sort

**Template (recursive):**
```
1. DFS(u):
     mark u visited
     pre_order.append(u)
     For each neighbor v:
       if v not visited:
         DFS(v)
     post_order.append(u)
2. For each unvisited u:
     DFS(u)
3. Use post_order for topological sort (reversed)
```

**Examples:** Cycles, topological sort, connectivity

---

### Topological Sort Roadmap (DAG Ordering)

**When:** Dependencies, build order, prerequisites

**Template (DFS-based):**
```
1. Verify no cycles (run DFS, no back edges)
2. Run DFS with post_order tracking
3. Reverse post_order = topological sort
4. Check: all dependencies before dependents
```

**Template (Kahn's):**
```
1. Compute in-degree of each vertex
2. queue = [vertices with in-degree 0]
3. While queue:
     u = queue.pop_front()
     output.append(u)
     For each neighbor v:
       in_degree[v]--
       if in_degree[v] == 0:
         queue.push_back(v)
4. If |output| != n: cycle exists
```

**Examples:** Course schedule, build order, npm dependencies

---

### Union-Find Roadmap (Dynamic Connectivity)

**When:** Cycles, connected components, MST (Kruskal's)

**Template:**
```
1. Implement find(x) with path compression
2. Implement union(x, y) with rank
3. For cycle detection:
     if find(u) == find(v): cycle exists
     else: union(u, v)
4. For connectivity: find(x) == find(y)
```

**Examples:** Cycle detection, Kruskal's MST, connected components

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "BFS for weighted shortest path"
**Recovery:** BFS only for unweighted. Use Dijkstra's for weighted.

### Pitfall 2: "Topological sort on graph with cycles"
**Recovery:** Verify DAG first (no cycles). Check |output| == n (Kahn's).

### Pitfall 3: "Choose matrix representation for large sparse graph"
**Recovery:** Use O(n+m) list, not O(n²) matrix. Save 100x+ space.

### Pitfall 4: "Implement Union-Find without path compression"
**Recovery:** Add path compression: parent[x] = find(parent[x]). Massive speedup.

### Pitfall 5: "Forget visited set in BFS/DFS"
**Recovery:** Must track visited. Cycles cause infinite loops without it.

---

## 📋 Quick Reference Matrix

| Problem | Algorithm | Representation | Time | Space |
|---------|-----------|-----------------|------|-------|
| Shortest unweighted | BFS | List | O(n+m) | O(n) |
| Topological order | DFS | List | O(n+m) | O(n) |
| Cycle detection | DFS or UF | List | O(n+m) | O(n) |
| Connected components | BFS/DFS or UF | List | O(n+m) | O(n) |
| Dynamic connectivity | Union-Find | Array | O(α(n)) | O(n) |

---

**Master this roadmap. Each Week 6 problem fits exactly one pattern.**

