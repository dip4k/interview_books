# Week 6, Day 5: Union-Find (Disjoint Set Union)

**Week:** 6 | **Day:** 5 | **Topic:** Union-Find with Path Compression  
**Time:** 90 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** All previous days  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Question:** Efficiently handle set merging and membership queries.

**Applications:**
- Connected components: which nodes are connected?
- Minimum spanning tree: Kruskal's algorithm
- Social networks: friend groups
- Least common ancestor: tree queries

### Why This Matters

- **Almost constant time:** O(α(n)) ≈ O(1) with optimizations
- **Interview heavy:** 10-15% of graph/advanced problems
- **Elegant:** Simple idea, powerful result

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Idea: Trees of Components

```
Each connected component is a tree
  Root = representative of component
  Path from node to root = find operation

Merging components = union roots
```

### Example

```
Initially: {1}, {2}, {3}, {4}

Union(1,2): {1,2}, {3}, {4}
Union(2,3): {1,2,3}, {4}
Find(1):   3 (find representative)
Find(4):   4
Are 1 and 4 in same component? No (different roots)
```

---

## 3️⃣ THE HOW — Implementation

### Naive Approach

```python
class UnionFindNaive:
    def __init__(self, n):
        self.parent = list(range(n))  # Each node is its own parent
    
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # Path compression
        return self.parent[x]
    
    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        if root_x != root_y:
            self.parent[root_x] = root_y

# Time: O(α(n)) amortized, nearly O(1)
```

### Optimized with Union by Rank

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
    
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # Path compression
        return self.parent[x]
    
    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        
        if root_x == root_y:
            return False  # Already connected
        
        # Union by rank: attach smaller tree under larger
        if self.rank[root_x] < self.rank[root_y]:
            self.parent[root_x] = root_y
        elif self.rank[root_x] > self.rank[root_y]:
            self.parent[root_y] = root_x
        else:
            self.parent[root_y] = root_x
            self.rank[root_x] += 1
        
        return True  # Successfully connected

# Time: O(α(n)) amortized
```

---

## 4️⃣ VISUALIZATION — Traced Example

```
Union-Find operations:

Initial state (each separate):
  1   2   3   4

Union(1,2):
    1       3   4
    |
    2

Union(2,3):
      1     3   4
      |  /
      2-

Union(3,4):
      1     3
      |  /  |
      2    4

Find(1): 1→2→3 (path compression)
Find(4): 4→3
Are 1 and 4 same? Yes! (both have root 3)
```

---

## 5️⃣ CRITICAL ANALYSIS

### Complexity with Optimizations

| Operation | Without Optimization | With Path Compression | With Union by Rank | With Both |
|-----------|---------------------|----------------------|-------------------|-----------|
| **Find** | O(n) | O(log n) | O(log n) | O(α(n)) |
| **Union** | O(n) | O(log n) | O(log n) | O(α(n)) |

Where α(n) = inverse Ackermann function ≈ O(1)

### Path Compression Intuition

```
When finding root, update all pointers on path
  Old: 1→2→3→4→5 (path length 4)
  After find(1): 1→5, 2→5, 3→5, 4→5 (all direct to root)
  Next find(1): O(1)!
```

---

## 6️⃣ REAL SYSTEM INTEGRATION

### Connected Components

```
Given undirected graph, find all components
  For each edge (u,v): union(u,v)
  At end, nodes with same root are connected
  
Time: O(E × α(n)) ≈ O(E)
```

### Kruskal's Minimum Spanning Tree

```
Sort edges by weight
For each edge (u,v) in sorted order:
  If union(u,v) succeeds (not already connected):
    Add edge to MST
  
Total: O(E log E) for sorting + O(E × α(n)) for unions
```

---

## 7️⃣ CONCEPT CROSSOVERS

### Trees (Week 5)

```
Union-Find creates tree of components
Similar to tree representation
Path compression = tree restructuring
```

### Graphs (Weeks 6)

```
Connected components = fundamental graph property
Union-Find is best way to track them
```

---

## 8️⃣ MATHEMATICAL FOUNDATIONS

### Inverse Ackermann Function

```
α(n) is inverse of Ackermann function
  α(n) < 5 for all practical values of n
  For n = 2^65536, α(n) = 5!
  
So O(α(n)) ≈ O(1) in practice
```

### Path Compression Amortized Analysis

```
Complicated analysis shows:
  m operations (finds/unions) on n elements
  Total time: O(m × α(n))
  Amortized: O(α(n)) per operation
```

---

## 🔟 KNOWLEDGE CHECK

1. **Why start with parent[i] = i?** What does this represent?

2. **Path compression: update parent when finding. Why?** What's the benefit?

3. **Union by rank: attach smaller under larger. Why?** What happens otherwise?

4. **Can you use find without union?** Yes, why would you?

5. **How to detect cycle in undirected graph?** Use union-find!

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **Find: Compress Paths**
```
If parent[x] != x:
  parent[x] = find(parent[x])
Flattens tree, speeds up future finds
```

### **Union: Attach by Rank**
```
If smaller rank, attach underneath
Keeps tree shallow
```

### **Complexity Magic**
```
Simple idea + two optimizations = O(α(n))
Nearly constant time!
```

---

## 📝 KEY TAKEAWAYS

✅ **Union-Find manages disjoint sets**  
✅ **Path compression: O(α(n)) per find**  
✅ **Union by rank: keeps tree shallow**  
✅ **Two optimizations together: O(α(n)) ≈ O(1)**  
✅ **Essential for connected components & MST**  
✅ **Elegant algorithm, practical performance**

---

## 🎉 WEEK 6 COMPLETE

**Days 1-5 covered:**
- Graph representations (foundation)
- BFS (shortest paths, breadth-first)
- DFS (exploration, backtracking)
- Topological sort (dependency ordering)
- Union-Find (component management)

**Interview coverage:** 40-60% of graph problems  
**Next:** Week 7 — Advanced Graph Algorithms

