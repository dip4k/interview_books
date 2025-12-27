# Week 7: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for ALL Week 7 problems:**

1. **Analyze** problem (shortest path? spanning? flow?)
2. **Identify** constraints (negative weights? all-pairs? capacities?)
3. **Match** algorithm (Dijkstra? Bellman-Ford? MST? Flow?)
4. **Implement** with proper data structures
5. **Optimize** for constraints and real-world needs

---

## 🎯 Pattern Decision Tree

```
Is it a SHORTEST PATH problem?
├─ Unweighted? → BFS (Week 6)
├─ Non-negative weights? → Dijkstra's
├─ Negative weights? → Bellman-Ford
└─ All-pairs? → Floyd-Warshall

Is it a SPANNING/CONNECTIVITY problem?
├─ Minimum spanning tree? → Kruskal's or Prim's
├─ Which? (sparse→Kruskal's, dense→Prim's)
└─ MST with property? → Specialized MST

Is it a FLOW/MATCHING problem?
├─ Maximum flow? → Ford-Fulkerson or Edmonds-Karp
├─ Bipartite matching? → Flow network
├─ Min-cut? → Max-flow min-cut theorem
└─ Circulation? → Flow with demands
```

---

## 🌳 Algorithm-Specific Roadmaps

### Dijkstra's Roadmap (Shortest Path Non-Negative)

**When:** Single-source shortest path, non-negative weights

**Template:**
```
1. distance[source] = 0, others = ∞
2. pq = [(0, source)]
3. While pq not empty:
   dist, u = pq.pop()
   if u processed: continue
   For each neighbor v of u with weight w:
     if distance[u] + w < distance[v]:
       distance[v] = distance[u] + w
       pq.push((distance[v], v))
4. Return distance
```

**Examples:** GPS routes, network latency, game pathfinding

---

### Bellman-Ford Roadmap (Negative Weights)

**When:** Single-source shortest path, may have negative weights

**Template:**
```
1. distance[source] = 0, others = ∞
2. For i from 1 to n-1:
   For each edge (u,v,w):
     if distance[u] + w < distance[v]:
       distance[v] = distance[u] + w
3. For each edge (u,v,w):
   if distance[u] + w < distance[v]:
     NEGATIVE CYCLE
4. Return distance
```

**Examples:** Currency arbitrage, cost adjustment

---

### Floyd-Warshall Roadmap (All-Pairs)

**When:** All-pairs shortest paths, small graph

**Template:**
```
1. dist = matrix of edge weights
2. For k from 0 to n-1:
   For i from 0 to n-1:
     For j from 0 to n-1:
       dist[i][j] = min(dist[i][j], 
                        dist[i][k] + dist[k][j])
3. Return dist
```

**Examples:** Transitive closure, reachability

---

### Kruskal's MST Roadmap

**When:** Minimum spanning tree, edge-based approach

**Template:**
```
1. Sort edges by weight
2. For each edge (u,v,w):
   if find(u) != find(v):
     add to MST
     union(u,v)
3. Return MST
```

**Examples:** Network backbone, infrastructure

---

### Prim's MST Roadmap

**When:** Minimum spanning tree, vertex-based approach

**Template:**
```
1. Start at vertex s
2. visited = {s}, pq = edges from s
3. While unvisited remain:
   (w,u,v) = pq.pop()
   if v visited: continue
   add edge to MST
   visited.add(v)
   add edges from v to pq
4. Return MST
```

**Examples:** Incremental construction, dense graphs

---

### Edmonds-Karp Roadmap (Network Flow)

**When:** Maximum flow, need polynomial guarantee

**Template:**
```
1. flow = 0, residual = capacity.copy()
2. While augmenting path exists (BFS):
   path = BFS shortest path in residual
   bottleneck = min capacity on path
   For each edge on path:
     residual[u][v] -= bottleneck
     residual[v][u] += bottleneck
   flow += bottleneck
3. Return flow
```

**Examples:** Bipartite matching, image segmentation

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "Dijkstra's with negative weights"
**Recovery:** Detect negative. Use Bellman-Ford instead.

### Pitfall 2: "Floyd-Warshall for large n"
**Recovery:** O(n³) too slow. Use Dijkstra's from each vertex.

### Pitfall 3: "Kruskal's always optimal representation"
**Recovery:** Dense graphs? Prim's O((n+m) log n) better than O(m log m).

### Pitfall 4: "Ford-Fulkerson always polynomial"
**Recovery:** O(flow × m) can be slow. Use Edmonds-Karp O(nm²).

### Pitfall 5: "Don't know algorithm selection"
**Recovery:** Use decision tree above. Match problem type.

---

## 📋 Quick Reference Matrix

| Problem | Algorithm | Time | When |
|---------|-----------|------|------|
| Shortest path unweighted | BFS | O(n+m) | Week 6 |
| Shortest path weighted | Dijkstra's | O((n+m) log n) | Non-negative |
| Shortest path negative | Bellman-Ford | O(n×m) | With negatives |
| All-pairs shortest | Floyd-Warshall | O(n³) | Small graphs |
| MST sparse | Kruskal's | O(m log m) | Sparse |
| MST dense | Prim's | O((n+m) log n) | Dense |
| Maximum flow | Edmonds-Karp | O(n m²) | Polynomial |

---

**Master this roadmap. Each Week 7 problem fits exactly one pattern.**

