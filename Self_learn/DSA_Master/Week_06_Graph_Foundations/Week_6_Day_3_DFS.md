# Week 6, Day 3: Depth-First Search (DFS)

**Week:** 6 | **Day:** 3 | **Topic:** DFS & Backtracking  
**Time:** 85 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Days 1-2  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Question:** Explore all nodes in a graph; detect cycles; find paths.

**Applications:**
- Backtracking: puzzles, Sudoku, N-queens
- Cycle detection: deadlock detection
- Topological sort: dependency resolution
- Connected components: graph connectivity

### Why This Matters

- **Most flexible:** Works where BFS doesn't
- **Interview heavy:** 20-25% of graph problems
- **Foundation for advanced algorithms:** DFS-based

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Idea: Explore Deep Before Wide

```
From node, go as deep as possible
  When stuck, backtrack
  Explore alternative paths
  
DFS = recursion depth first
```

### Why It Works

```
Going deep first explores one path completely
When we hit a dead end, we backtrack
  Backtrack = return from recursion
  Try next neighbor
```

---

## 3️⃣ THE HOW — Implementation

```python
def dfs_recursive(graph, node, visited):
    visited.add(node)
    
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs_recursive(graph, neighbor, visited)

def dfs_iterative(graph, start):
    visited = set()
    stack = [start]
    
    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            stack.extend(reversed(graph[node]))  # Maintain order
    
    return visited

# Time: O(V+E), Space: O(V) call stack
```

---

## 4️⃣ VISUALIZATION — Traced Example

```
Graph: 1-2, 1-3, 2-4, 3-5

DFS from 1 (recursive):
  Visit 1
    Visit 2 (first neighbor)
      Visit 4 (first neighbor of 2)
        4 has no unvisited neighbors
      Backtrack to 2
    Backtrack to 1
    Visit 3 (second neighbor)
      Visit 5 (first neighbor of 3)
        5 has no unvisited neighbors
      Backtrack to 3
    Done

Order visited: 1, 2, 4, 3, 5
```

---

## 5️⃣ CRITICAL ANALYSIS

### Complexity

| Metric | Complexity |
|--------|-----------|
| **Time** | O(V+E) |
| **Space** | O(V) call stack |

### DFS vs BFS

```
BFS: Level-by-level, shortest path
DFS: Deep exploration, all paths
```

---

## 6️⃣ REAL SYSTEM INTEGRATION

### Cycle Detection

```
DFS detects back edges (edges to ancestor in DFS tree)
Back edge = cycle exists
Used in deadlock detection
```

### Backtracking Problems

```
Sudoku: fill cell, recurse, if stuck backtrack
  DFS naturally backtracks via recursion
N-queens: place queen, recurse, backtrack if needed
```

---

## 7️⃣ CONCEPT CROSSOVERS

### Stack Data Structure (Week 2)

```
DFS uses recursion (implicit stack)
Or explicit stack for iterative version
Week 2 learned stacks
Week 6 applies to graphs
```

### Trees (Week 5)

```
Tree traversals = DFS on tree!
Preorder, postorder = different DFS orderings
```

---

## 8️⃣ MATHEMATICAL FOUNDATIONS

### DFS Tree Property

```
DFS creates a spanning tree
  Tree edges: edges taken by DFS
  Back edges: edges to ancestors
  Forward edges: edges to descendants
  Cross edges: edges between unrelated nodes

Can classify all edges based on DFS discovery times
```

---

## 🔟 KNOWLEDGE CHECK

1. **Why does DFS use stack (implicit or explicit)?** How is it different from BFS queue?

2. **Can DFS find shortest path?** Why or why not?

3. **How to detect cycles with DFS?** What indicates a back edge?

4. **What's the difference between iterative and recursive?** When use each?

5. **How does DFS help with topological sort?** (Next day's topic)

---

## 📝 KEY TAKEAWAYS

✅ **DFS explores deep before wide**  
✅ **Uses stack (recursion or explicit)**  
✅ **Finds all reachable nodes**  
✅ **Can detect cycles (back edges)**  
✅ **Time: O(V+E), Space: O(V)**  
✅ **Foundation for backtracking**

**Next:** Day 4 — Topological Sort (DFS application)

