# Week 6, Day 4: Topological Sort

**Week:** 6 | **Day:** 4 | **Topic:** Topological Sorting of DAGs  
**Time:** 85 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Days 1-3 (DFS especially)  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Question:** Order tasks with dependencies.

**Applications:**
- Build systems: compile order (dependencies first)
- Course prerequisites: which courses before which
- Task scheduling: job dependencies
- Package installation: install dependencies first

### Why This Matters

- **Real-world:** Constant in practical systems
- **Interview staple:** 10-15% of graph problems
- **Elegant:** Beautiful algorithm, elegant solution

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Insight: DFS Finishing Order

```
Topological sort = reverse of DFS finishing order

Why? In DFS:
  If edge u→v, then u finishes AFTER v
  (because we visit v from u)

Reverse finishing order = topological order!
```

### Example

```
Dependencies: 1→2, 2→3, 1→3

DFS from 1:
  Visit 1
    Visit 2
      Visit 3 (finishes first)
    2 finishes
  1 finishes

Finishing order: 3, 2, 1
Reverse: 1, 2, 3 ✓ Topological sort!
```

---

## 3️⃣ THE HOW — Implementation

```python
def topological_sort(graph, n):
    visited = [False] * n
    finish_stack = []
    
    def dfs(node):
        visited[node] = True
        for neighbor in graph[node]:
            if not visited[neighbor]:
                dfs(neighbor)
        finish_stack.append(node)  # Add when finishing
    
    for i in range(n):
        if not visited[i]:
            dfs(i)
    
    return finish_stack[::-1]  # Reverse = topological order

# Time: O(V+E), Space: O(V)
```

### Kahn's Algorithm (Alternative)

```python
from collections import deque, defaultdict

def topological_sort_kahn(graph, n):
    in_degree = [0] * n
    for u in graph:
        for v in graph[u]:
            in_degree[v] += 1
    
    queue = deque([i for i in range(n) if in_degree[i] == 0])
    result = []
    
    while queue:
        node = queue.popleft()
        result.append(node)
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    return result if len(result) == n else None  # None if cycle

# Time: O(V+E), Space: O(V)
```

---

## 4️⃣ VISUALIZATION — Traced Example

```
Graph: Courses: CS101 → CS201, CS101 → CS301, CS201 → CS401

DFS-based topological sort:
  Visit CS101
    Visit CS201
      Visit CS401 (finish first)
      Finish CS201
    Visit CS301 (finish next)
  Finish CS101

Stack (finishing order): CS401, CS201, CS301, CS101
Reverse: CS101, CS201, CS301, CS401 ✓

Interpretation: Take CS101 first, then CS201, etc.
```

---

## 5️⃣ CRITICAL ANALYSIS

### Key Requirement: DAG (Directed Acyclic Graph)

```
Topological sort only works on DAGs!

If cycle exists:
  DFS-based: Still works (ignores cycle)
  Kahn's: Returns None/fails (queue becomes empty)
```

### Complexity

```
Both approaches:
  Time: O(V+E)
  Space: O(V)
```

### When to Use Each

```
DFS-based:
  Simpler, elegant
  Prefer if graph already DFS-traversed

Kahn's:
  Detects cycles naturally
  Prefer for cycle detection
```

---

## 6️⃣ REAL SYSTEM INTEGRATION

### Build Systems (Make, Gradle)

```
Dependency graph: file.o → file.cpp
Topological sort: compile order
Only compile needed files, only recompile dependents
```

### Course Prerequisites

```
Graph: CS201 ← CS101, CS301 ← CS101, CS401 ← CS201 ∧ CS301
Topological sort: course enrollment order
```

---

## 7️⃣ CONCEPT CROSSOVERS

### DFS (Day 3)

```
Topological sort = DFS application
Uses DFS for ordering
```

### Trees (Week 5)

```
Topological sort on tree = level order naturally
On DAG = more complex due to multiple paths
```

---

## 8️⃣ MATHEMATICAL FOUNDATIONS

### Theorem: DFS Finishing Order Gives Topological Sort

**Proof:**
- For edge u→v: if u not visited, we visit v from u (v finishes before u)
- If u already visited: v was visited earlier, so finishes before u
- Therefore: in reverse finishing order, u comes before v ✓

---

## 🔟 KNOWLEDGE CHECK

1. **Why must graph be a DAG?** What fails if there's a cycle?

2. **Why is reverse finishing order correct?** Prove for one edge.

3. **Can topological sort be non-unique?** Give example.

4. **How to detect cycles with topological sort?** Using Kahn's algorithm.

5. **What if multiple sources (in-degree 0)?** Does Kahn's still work?

---

## 📝 KEY TAKEAWAYS

✅ **Topological sort orders DAG tasks**  
✅ **DFS-based: reverse finishing order**  
✅ **Kahn's algorithm: BFS with in-degree**  
✅ **Time: O(V+E), Space: O(V)**  
✅ **Essential for dependency resolution**  
✅ **Works only on DAGs**

**Next:** Day 5 — Union-Find (Disjoint Sets)

