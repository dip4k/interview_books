# Week 6: Summary & Quick Reference

**Week:** 6 | **Topic:** Graph Foundations | **Difficulty:** Hard | **Time:** 25-30 hours

---

## 📊 FIVE TECHNIQUES AT A GLANCE

| Technique | Problem | Solution | Time | Space | Interview % |
|-----------|---------|----------|------|-------|------------|
| **Graph Repr.** | Store graph | Matrix or List | - | O(n²) or O(n+m) | Foundation |
| **BFS** | Shortest path | Level-by-level queue | O(V+E) | O(V) | 15-20% |
| **DFS** | Connectivity | Recursive/stack | O(V+E) | O(V) | 20-25% |
| **Topo Sort** | Dependencies | DFS/Kahn's | O(V+E) | O(V) | 10-15% |
| **Union-Find** | Components | Parent pointers | O(α(n)) | O(V) | 10-15% |

---

## 🎯 ALGORITHM DECISION TREE

```
Need to solve graph problem?

├─ Find connected components?
│  └─ Union-Find (Day 5)
├─ Find shortest path (unweighted)?
│  └─ BFS (Day 2)
├─ Need all paths or backtrack?
│  └─ DFS (Day 3)
├─ Need to order dependencies?
│  └─ Topological Sort (Day 4)
└─ How to store graph?
   ├─ Dense? → Adjacency Matrix
   └─ Sparse? → Adjacency List
```

---

## 📝 CODE TEMPLATES

### Template 1: Adjacency List

```python
from collections import defaultdict, deque

graph = defaultdict(list)
graph[1].append(2)
graph[2].append(3)
```

### Template 2: BFS

```python
def bfs(graph, start):
    visited = {start}
    queue = deque([start])
    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

### Template 3: DFS (Recursive)

```python
def dfs(graph, node, visited):
    visited.add(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

### Template 4: Topological Sort

```python
def topo_sort(graph, n):
    visited = [False] * n
    stack = []
    def dfs(node):
        visited[node] = True
        for neighbor in graph[node]:
            if not visited[neighbor]:
                dfs(neighbor)
        stack.append(node)
    for i in range(n):
        if not visited[i]:
            dfs(i)
    return stack[::-1]
```

### Template 5: Union-Find

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py: return False
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1
        return True
```

---

## ⚡ COMMON MISTAKES & FIXES

| Mistake | Why Wrong | Fix |
|---------|-----------|-----|
| BFS without visited set | Infinite loop in cycles | Always track visited |
| DFS too deep in large graph | Stack overflow | Use iterative or be careful |
| Topo sort on graph with cycle | Returns invalid order | Check for cycle first |
| Union-Find without path compression | O(n) per operation | Always update parent |
| Choose matrix for sparse graph | O(n²) memory wasted | Use adjacency list |

---

## 🧠 PATTERN RECOGNITION

**BFS keywords:**
- Shortest path, level-by-level, closest, degree

**DFS keywords:**
- All paths, backtrack, connected components, cycle

**Topo Sort keywords:**
- Dependencies, ordering, prerequisites, DAG

**Union-Find keywords:**
- Connected, components, grouping, merging

**Matrix vs List:**
- Dense (>20%) → Matrix
- Sparse (<5%) → List

---

## 📊 COMPLEXITY COMPARISON

| Problem | Naive | BFS | DFS | Topo | UF |
|---------|-------|-----|-----|------|-----|
| **Connected?** | O(n²) | O(V+E) | O(V+E) | - | O(α(n)) |
| **Shortest path** | O(n²) | O(V+E) | ✗ | - | - |
| **Components** | O(n²) | O(V+E) | O(V+E) | - | O(mα(n)) |
| **Cycle detect** | O(n²) | O(V+E) | O(V+E) | O(V+E) | O(α(n)) |

---

## ✅ INTERVIEW CHECKLIST

**Before Interview:**
- [ ] Code all 5 algorithms from scratch?
- [ ] Explain each in 30 seconds?
- [ ] Know when to use each?
- [ ] Handle disconnected graphs?
- [ ] Track complexity?

**During Interview:**
- [ ] Clarify problem requirements
- [ ] Identify algorithm needed
- [ ] Implement cleanly
- [ ] Test with examples
- [ ] Discuss trade-offs

---

## 📋 QUICK FACTS

| Fact | Details |
|------|---------|
| **BFS** | Queue (FIFO), shortest unweighted path |
| **DFS** | Stack (LIFO), explore deep, backtrack |
| **Topo** | DFS finishing order reversed, works on DAGs only |
| **Union** | Path compression + union by rank = O(α(n)) |
| **Graph Repr** | Matrix O(n²) space, List O(n+m) space |

---

**Quick Reference Version:** 1.0 Week 6 Complete

