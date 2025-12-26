# Week 6, Day 1: Graph Representations

**Week:** 6 | **Day:** 1 | **Topic:** Graph Representations & Data Structures  
**Time:** 80 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Week 5.5 (Optimization Techniques)  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Scenario:** Represent relationships between entities.

**Examples:**
- Social network: users (nodes), friendships (edges)
- Road network: cities (nodes), roads (edges)
- Web graph: pages (nodes), links (edges)
- Dependency graph: tasks (nodes), dependencies (edges)

**Challenge:** Choose representation matching problem requirements.

### Why This Matters

- **Efficiency:** Wrong representation = 10x slower
- **Space:** Dense vs sparse graphs need different approaches
- **Scalability:** LinkedIn has 1B+ users; must choose wisely
- **Algorithms:** Some algorithms only work with specific representations

**Why This Matters:** Graph representation choice is foundational for all Week 6+ algorithms.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Insight: Two Representations

**Adjacency Matrix:** 2D array, O(1) edge lookup  
**Adjacency List:** Array of lists, O(1) edge insertion

### When Each Shines

```
Dense Graph (many edges):
  Adjacency matrix better
  Example: Complete graph, social network among small group
  Edge ratio: > 20%

Sparse Graph (few edges):
  Adjacency list better
  Example: Road network, web graph, dependency graph
  Edge ratio: < 5%
```

### Visual Comparison

```
Graph: 1-2, 1-3, 2-3

Adjacency Matrix:      Adjacency List:
  1 2 3                1: [2, 3]
1[0 1 1]               2: [1, 3]
2[1 0 1]               3: [1, 2]
3[1 1 0]
```

---

## 3️⃣ THE HOW — Implementation & Mechanics

### Adjacency Matrix Implementation

```python
class GraphMatrix:
    def __init__(self, n):
        self.n = n
        self.matrix = [[0] * n for _ in range(n)]
    
    def add_edge(self, u, v):
        self.matrix[u][v] = 1
        self.matrix[v][u] = 1  # Undirected
    
    def has_edge(self, u, v):
        return self.matrix[u][v] == 1
    
    def neighbors(self, u):
        return [v for v in range(self.n) if self.matrix[u][v] == 1]

# Space: O(n²), Edge lookup: O(1)
```

### Adjacency List Implementation

```python
from collections import defaultdict

class GraphList:
    def __init__(self, n):
        self.n = n
        self.graph = defaultdict(list)
    
    def add_edge(self, u, v):
        self.graph[u].append(v)
        self.graph[v].append(u)  # Undirected
    
    def has_edge(self, u, v):
        return v in self.graph[u]
    
    def neighbors(self, u):
        return self.graph[u]

# Space: O(n+m), Edge lookup: O(degree)
```

### Weighted Graphs

```python
# Adjacency List with Weights
class WeightedGraph:
    def __init__(self):
        self.graph = defaultdict(list)
    
    def add_edge(self, u, v, weight):
        self.graph[u].append((v, weight))
    
    def neighbors(self, u):
        return self.graph[u]  # Returns (neighbor, weight) pairs

# Example: [(2, 5), (3, 3)] means edges to 2 with weight 5, to 3 with weight 3
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: Building a Graph

```
Graph: 0-1, 0-2, 1-2, 2-3

Adjacency Matrix:
    0 1 2 3
  0[0 1 1 0]
  1[1 0 1 0]
  2[1 1 0 1]
  3[0 0 1 0]

Adjacency List:
  0: [1, 2]
  1: [0, 2]
  2: [0, 1, 3]
  3: [2]
```

### Example 2: Edge Operations

```
Add edge 1-3:

Matrix:
    0 1 2 3
  0[0 1 1 0]
  1[1 0 1 1]  ← changed
  2[1 1 0 1]
  3[0 1 1 0]  ← changed

List:
  0: [1, 2]
  1: [0, 2, 3]  ← added 3
  2: [0, 1, 3]
  3: [2, 1]     ← added 1
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Comparison

| Operation | Matrix | List | Notes |
|-----------|--------|------|-------|
| **Add edge** | O(1) | O(1) amortized | List might realloc |
| **Remove edge** | O(1) | O(degree) | List must search |
| **Check edge** | O(1) | O(degree) | List must search |
| **Neighbors** | O(n) | O(degree) | Matrix must scan row |
| **Space** | O(n²) | O(n+m) | n=nodes, m=edges |
| **Iteration** | O(n²) | O(n+m) | Critical for algorithms |

### When to Use

**Adjacency Matrix:**
- Dense graphs (>20% edges)
- Need O(1) edge lookup
- Small graphs (n < 1000)
- Weighted edges still work

**Adjacency List:**
- Sparse graphs (<5% edges)
- Need fast neighbor iteration
- Large graphs (n > 10,000)
- Preferred for most algorithms

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Social Networks (Sparse)

```
Facebook: 3B users, ~200 friends average
Edge ratio: 200 * 2 / (3B²) ≈ 0.0000001%

Use: Adjacency list
Why: Extremely sparse, need to iterate neighbors quickly
```

### Game Maps (Mixed)

```
Game world: 100 locations, many connections
Edge ratio: ~50%

Use: Adjacency list (still preferred)
Why: Algorithms work better with list, iteration faster
```

### DNA Sequences (Dense)

```
Comparing k sequences: each might connect to many others
Edge ratio: high

Use: Matrix or list depending on size
Why: If k small (< 1000), matrix. If large, list.
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Week 5: Trees Return

```
Trees = special graphs
  Tree representation = adjacency list
  Operations similar to tree traversal
```

### Week 5.5: Data Structure Choice

```
Adjacency list = list of lists
  Builds on understanding 2D structures
  Optimization principle: choose structure for algorithm
```

### Coming: BFS/DFS

```
Day 2-3: Need to iterate neighbors efficiently
  Adjacency list dominates
  Matrix slower for sparse graphs
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### Graph Terminology

**Definition:** Graph G = (V, E)
- V = vertices (nodes)
- E = edges (connections)

**Undirected:** Edge (u,v) = edge (v,u)  
**Directed:** Edge u→v ≠ edge v→u

**Dense:** |E| = Θ(|V|²)  
**Sparse:** |E| = Θ(|V|)

### Space Complexity Proof

**Matrix:** O(n²) always
```
n × n array = n² entries = O(n²)
```

**List:** O(n+m)
```
n lists (one per node) = O(n)
m edges (each stored twice for undirected) = O(m)
Total = O(n+m)
```

For sparse graphs: O(n+m) << O(n²)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why Adjacency List for Algorithms?

```
BFS/DFS need: for each node, iterate neighbors
  Matrix: O(n) per node = O(n²) total
  List: O(degree) per node = O(n+m) total

For sparse graph (m << n²):
  List is dramatically faster
```

### Why Matrix for Small Dense Graphs?

```
O(1) edge lookup useful when:
  1. Need to check specific edges frequently
  2. Graph is dense (n² not much larger than n+m)
  3. Constant factors matter more than asymptotic
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **When would you use adjacency matrix over list?** What makes a graph "dense"?

2. **Why does matrix need O(n) to list neighbors?** Why list only O(degree)?

3. **For a complete graph with n=1000, which is faster?** Calculate space for both.

4. **Can you convert between representations?** What's the time cost?

5. **For weighted graphs, how do you store weights?** Works with both representations?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **Matrix vs List Decision**

```
Dense (>20% edges)? → Matrix (faster lookup)
Sparse (<5% edges)? → List (faster iteration)
In doubt? → List (works for all, standard choice)
```

### **Space Rule**

```
Matrix: O(n²) always
List: O(n+m) exactly
For sparse: List saves orders of magnitude
```

### **Complexity Rule**

```
Any graph operation:
  Matrix: typically O(n²) or better
  List: typically O(n+m) or better
```

---

## 📊 SUPPLEMENTARY: Quick Comparison

| Metric | Matrix | List |
|--------|--------|------|
| Space | O(n²) | O(n+m) |
| Add edge | O(1) | O(1) |
| Remove edge | O(1) | O(degree) |
| Check edge | O(1) | O(degree) |
| List neighbors | O(n) | O(degree) |
| BFS/DFS | O(n²) | O(n+m) |
| Best for | Dense graphs | Sparse graphs |

---

## 🔗 EXTERNAL RESOURCES

**Visualization:**
- Graph visualization tools: https://www.cs.usfca.edu/~galles/visualization/Dijkstra.html

**Practice:**
- Graph problems: https://leetcode.com/tag/graph/

---

## 📝 KEY TAKEAWAYS

✅ **Two main representations: matrix and list**  
✅ **Matrix: O(n²) space, O(1) lookup**  
✅ **List: O(n+m) space, O(degree) lookup**  
✅ **Use list for sparse graphs (standard choice)**  
✅ **Use matrix for dense graphs or when lookup critical**  
✅ **Representation choice impacts algorithm efficiency**

**Next:** Day 2 — Breadth-First Search (BFS)

