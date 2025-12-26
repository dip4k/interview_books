# Week 6, Day 2: Breadth-First Search (BFS)

**Week:** 6 | **Day:** 2 | **Topic:** BFS & Shortest Paths  
**Time:** 85 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Day 1 (Graph Representations)  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Question:** Find shortest path in unweighted graph.

**Applications:**
- Social networks: degrees of separation (6 degrees)
- GPS: shortest route (number of hops)
- Game AI: closest enemy
- Web crawler: closest page to home

### Why This Matters

- **BFS is fundamental:** Used in Dijkstra, Prim's, more
- **Interview staple:** 15-20% of graph problems
- **Intuitive:** Easier than DFS for many people

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Idea: Explore Level-by-Level

```
Start at node 1, explore:
  Level 0: [1]
  Level 1: All neighbors of 1
  Level 2: All unvisited neighbors of level 1
  ...
  
First time reach a node = shortest path!
```

### Why It Works

```
Exploring level-by-level means:
  - All level 1 nodes are distance 1
  - All level 2 nodes are distance 2
  - ...
  
First arrival at a node = guaranteed shortest path
```

---

## 3️⃣ THE HOW — Implementation

```python
from collections import deque

def bfs(graph, start):
    visited = set([start])
    queue = deque([start])
    distances = {start: 0}
    
    while queue:
        node = queue.popleft()
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
                distances[neighbor] = distances[node] + 1
    
    return distances

# Time: O(V+E), Space: O(V)
```

---

## 4️⃣ VISUALIZATION — Traced Example

```
Graph: 1-2, 1-3, 2-4, 3-4, 4-5

BFS from 1:
Queue: [1], visited: {1}, dist: {1:0}

Pop 1, add neighbors 2,3:
Queue: [2,3], visited: {1,2,3}, dist: {1:0, 2:1, 3:1}

Pop 2, add neighbor 4:
Queue: [3,4], visited: {1,2,3,4}, dist: {1:0, 2:1, 3:1, 4:2}

Pop 3, neighbors 1,4 already visited:
Queue: [4], visited: {1,2,3,4}

Pop 4, add neighbor 5:
Queue: [5], visited: {1,2,3,4,5}, dist: {1:0, 2:1, 3:1, 4:2, 5:3}

Pop 5, no neighbors:
Queue: [], done

Distances: {1:0, 2:1, 3:1, 4:2, 5:3}
```

---

## 5️⃣ CRITICAL ANALYSIS

### Complexity

| Metric | Complexity |
|--------|-----------|
| **Time** | O(V+E) |
| **Space** | O(V) |
| **Correctness** | Guarantees shortest path |

### Edge Cases

- **Single node:** Works correctly
- **Disconnected graph:** Only visits reachable nodes
- **Cycles:** Handled by visited set

---

## 6️⃣ REAL SYSTEM INTEGRATION

### Social Networks

```
"Degrees of separation" between users
BFS finds minimum hops to reach someone
LinkedIn uses this concept
```

### Game AI

```
Find nearest enemy/resource
BFS explores in layers of increasing distance
Optimal for turn-based games
```

---

## 7️⃣ CONCEPT CROSSOVERS

### Queue Data Structure (Week 2)

```
BFS relies on queue (FIFO)
Week 2 learned queues
Week 6 applies queues to graphs
```

### Difference Array (Week 5.5)

```
BFS can track distances
Distances can use difference array pattern for updates
```

---

## 8️⃣ MATHEMATICAL FOUNDATIONS

### Lemma: BFS Finds Shortest Path

**Proof:** 
- When we first visit a node v from u, we've taken shortest path to u (induction)
- Distance to v = distance to u + 1
- No other path can be shorter (since we explore level-by-level)

---

## 🔟 KNOWLEDGE CHECK

1. **Why must we mark visited immediately?** What if we mark only when popping?

2. **What if graph has weighted edges?** Does BFS still work?

3. **How to reconstruct path from BFS?** Store parent pointers.

4. **Complexity with adjacency matrix?** Time becomes O(V²).

5. **Can BFS find connected components?** How?

---

## 📝 KEY TAKEAWAYS

✅ **BFS explores level-by-level**  
✅ **First visit = shortest path**  
✅ **Use queue (FIFO)**  
✅ **Mark visited to avoid cycles**  
✅ **Time: O(V+E), Space: O(V)**  
✅ **Foundation for many algorithms**

**Next:** Day 3 — Depth-First Search (DFS)

