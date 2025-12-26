# Week 7, Day 3: Minimum Spanning Trees

**Week:** 7 | **Day:** 3 | **Topic:** Minimum Spanning Trees (Kruskal's & Prim's)  
**Difficulty:** Hard | **Time:** 100 minutes | **Prerequisites:** Week 7 Days 1-2, Week 6 (Union-Find)

---

## 1️⃣ THE WHY

**Problem Context:**
You have cities connected by roads. You want to build a network connecting all cities with minimum total road construction cost. You can't have cycles (would be redundant). This is the **Minimum Spanning Tree** problem.

**Why MST Matters:**
- Connect all nodes with minimum total weight
- No cycles (tree property)
- Applications: network design, cluster analysis, approximation algorithms
- Two algorithms: Kruskal's (edge-based) and Prim's (node-based)

**Key Difference from Shortest Path:**
- Shortest path: find path between two nodes
- MST: connect ALL nodes with minimum cost, no cycles

---

## 2️⃣ THE WHAT

**Spanning Tree Definition:**

```
Spanning Tree:
  Connected graph spanning all nodes
  Exactly V-1 edges (minimum to stay connected)
  No cycles (acyclic)
  
Minimum Spanning Tree:
  Among all spanning trees, pick one with minimum total edge weight
  
Example: 4 cities
  Tree needs 3 edges (not 4)
  Multiple possible trees
  MST picks the one with minimum cost
```

**Algorithm 1: Kruskal's Algorithm**

```
Kruskal's Algorithm (Edge-Based):

Input: Weighted undirected graph
Output: Minimum spanning tree

1. Sort edges by weight (ascending)
2. Use Union-Find structure
3. For each edge in sorted order:
   a. Get endpoints u, v
   b. If u and v in different components:
      - Add edge to MST
      - Union the components
   c. Stop when MST has V-1 edges
4. Return MST
```

**Algorithm 2: Prim's Algorithm**

```
Prim's Algorithm (Node-Based):

Input: Weighted undirected graph, start node s
Output: Minimum spanning tree

1. Start with node s in tree
2. Maintain set of nodes in tree
3. Repeat until all nodes in tree:
   a. Find minimum weight edge (u,v) where:
      - u in tree
      - v not in tree
   b. Add edge and node v to tree
4. Return MST
```

---

## 3️⃣ THE HOW

**Kruskal's Example:**

```
Graph: 4 nodes (A, B, C, D)
Edges:
  A-B: 1
  B-C: 2
  C-D: 3
  A-C: 4
  A-D: 5
  B-D: 6

Kruskal's Algorithm:

Step 1: Sort edges by weight
  A-B: 1 ✓
  B-C: 2 ✓
  C-D: 3 ✓
  A-C: 4 ✓
  A-D: 5 ✓
  B-D: 6 ✓

Step 2: Process edges in order
  Edge A-B (weight 1):
    A and B disconnected → Add to MST
    Components: {A,B}, {C}, {D}
    MST edges: 1

  Edge B-C (weight 2):
    B and C disconnected → Add to MST
    Components: {A,B,C}, {D}
    MST edges: 2

  Edge C-D (weight 3):
    C and D disconnected → Add to MST
    Components: {A,B,C,D}
    MST edges: 3
    
    → All 4 nodes connected with 3 edges
    → Stop (V-1 = 3 edges found)

  (Remaining edges not processed)

MST: A-B (1) + B-C (2) + C-D (3) = Total: 6
```

**Prim's Example:**

```
Same graph, starting from A:

Step 1: Tree = {A}
  Available edges from tree:
    A-B: 1 (min)
    A-C: 4
    A-D: 5
  Add edge A-B, node B
  Tree: {A, B}
  Total: 1

Step 2: Tree = {A, B}
  Available edges from tree:
    A-C: 4
    A-D: 5
    B-C: 2 (min)
    B-D: 6
  Add edge B-C, node C
  Tree: {A, B, C}
  Total: 1 + 2 = 3

Step 3: Tree = {A, B, C}
  Available edges from tree:
    A-D: 5
    C-D: 3 (min)
    B-D: 6
  Add edge C-D, node D
  Tree: {A, B, C, D}
  Total: 1 + 2 + 3 = 6
  
  → All nodes in tree, done

MST: A-B (1) + B-C (2) + C-D (3) = Total: 6
```

**Implementation (Python):**

```python
# Kruskal's with Union-Find
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
        if px == py:
            return False
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1
        return True

def kruskal(n, edges):
    # edges: list of (weight, u, v)
    edges.sort()
    uf = UnionFind(n)
    mst = []
    total = 0
    
    for weight, u, v in edges:
        if uf.union(u, v):
            mst.append((u, v, weight))
            total += weight
            if len(mst) == n - 1:
                break
    
    return mst, total

# Prim's with priority queue
import heapq

def prim(n, graph):
    # graph: adjacency list of (neighbor, weight)
    visited = [False] * n
    min_heap = [(0, 0)]  # (weight, node)
    mst = []
    total = 0
    
    while min_heap:
        weight, u = heapq.heappop(min_heap)
        
        if visited[u]:
            continue
        
        visited[u] = True
        if weight > 0:  # Skip initial 0-weight
            mst.append((u, weight))
            total += weight
        
        for v, w in graph[u]:
            if not visited[v]:
                heapq.heappush(min_heap, (w, v))
    
    return mst, total
```

---

## 4️⃣ VISUALIZATION

**Kruskal's MST Construction:**

```
Initial: 4 isolated nodes
  A   B   C   D

Add A-B (weight 1):
  A-B   C   D
  ___

Add B-C (weight 2):
  A-B-C   D
  _____

Add C-D (weight 3):
  A-B-C-D
  _______

Done: MST has A-B (1) + B-C (2) + C-D (3)
```

**Prim's MST Construction (Starting A):**

```
Tree = {A}, exploring...

Add B via A-B (weight 1):
  A---B    C   D
   \(1)

Tree = {A,B}, exploring...

Add C via B-C (weight 2):
  A---B---C   D
   \(1)\(2)

Tree = {A,B,C}, exploring...

Add D via C-D (weight 3):
  A---B---C---D
   \(1)\(2)\(3)

Complete MST!
```

---

## 5️⃣ COMPLEXITY ANALYSIS

**Kruskal's Algorithm:**

```
Time Complexity:
  Sort edges: O(E log E)
  Union-Find operations: O(E × α(V)) where α = inverse Ackermann (~4)
  Total: O(E log E) dominated by sorting
  
Space Complexity:
  Edges list: O(E)
  Union-Find: O(V)
  Total: O(V + E)

Performance:
  E = V²: O(V² log V)
  E = V: O(V log V)
```

**Prim's Algorithm:**

```
Time Complexity with Binary Heap:
  V extract-min operations: O(V log V)
  E decrease-key operations: O(E log V)
  Total: O((V + E) log V)

With Fibonacci Heap:
  Extract-min: O(V log V)
  Decrease-key: O(E) amortized
  Total: O(E + V log V)

Space Complexity:
  Priority queue: O(V)
  Adjacency list: O(V + E)
  Total: O(V + E)
```

**Comparison:**

```
Kruskal's: O(E log E) = good for sparse graphs
           Simpler to implement
           No need to pick start node

Prim's: O((V+E) log V) with heap = better for dense graphs
        Need to pick start node (doesn't matter)
        More complex with priority queue
```

---

## 6️⃣ SYSTEMS INTEGRATION

**Real-World Applications:**

1. **Network Design:**
   - Telecom: connect cities with minimum cable cost
   - Airline routes: connect hubs with minimum fuel consumption
   - Internet backbone: connect data centers with minimum latency

2. **Cluster Analysis (MST-based clustering):**
   - Single-linkage clustering uses MST
   - Find natural clusters by removing heavy edges
   - MST identifies cluster boundaries

3. **Approximation Algorithms:**
   - Traveling Salesman Problem (TSP)
   - MST gives 2-approximation
   - Find MST, then Eulerian tour, then shortcut

4. **Game Level Design:**
   - Connect important locations
   - Minimum path network for players
   - MST ensures all accessible

---

## 7️⃣ CROSSOVERS & VARIANTS

**Related to Previous Days:**

1. **Union-Find (Week 6):**
   - Kruskal's requires efficient Union-Find
   - Time depends on Union-Find implementation
   - Path compression + union by rank → nearly O(1)

2. **Shortest Paths (Days 1-2):**
   - MST finds minimum total weight spanning all nodes
   - Shortest path finds minimum total weight on path
   - Different problems, different algorithms

3. **Greedy Algorithms (Week 10):**
   - Kruskal's is greedy: always pick minimum edge
   - Prim's is greedy: always pick minimum available edge
   - Both provably optimal (matroid theory)

**Advanced Variants:**

1. **Borůvka's Algorithm:**
   - Find minimum edge for each component
   - Merge components
   - O(E log V) but conceptually simpler
   - Parallelizable

2. **MST in Dense Graphs:**
   - O(V²) algorithm without heap overhead
   - Better than Prim's with heap for complete graphs

3. **Maximum Spanning Tree:**
   - Same algorithms, maximize instead of minimize
   - Just negate weights and run MST

---

## 8️⃣ THEORY & PROOF

**Kruskal's Correctness (Cut Property):**

```
Lemma (Cut Property):
  For any cut (partition into two sets) of vertices,
  The minimum weight edge crossing the cut is in some MST

Proof of Kruskal's:
  Kruskal adds edges in minimum weight order
  Each added edge is minimum weight crossing the cut
  By cut property, must be in some MST
  Final tree includes edges in some MST
```

**Prim's Correctness (Same Cut Property):**

```
Prim's Invariant:
  At each step, tree built so far is part of some MST

Proof:
  Initially, any single node is trivially part of MST
  
  When adding edge (u,v) with u in tree, v not in tree:
    By cut property, minimum edge across cut is in some MST
    Prim picks minimum such edge
    Tree remains part of some MST
    
  Induction proves correctness
```

---

## 9️⃣ INTUITION & MENTAL MODELS

**Kruskal's: Greedy Edge Selection**

Imagine you're laying cables:
- Sort all cables by cost (shortest first)
- Lay them one by one
- Skip cables that would create cycle (already connected)
- Continue until all cities connected

**Prim's: Growing Tree**

Imagine a tree growing:
- Start with one node (seed)
- Always grow toward nearest uncovered node
- Eventually covers entire forest
- Never backtracks (greedy expansion)

---

## 🔟 KNOWLEDGE CHECK

**Questions:**

1. **Why does Kruskal's not create cycles?**
   - Answer: Union-Find detects when endpoints already connected; skip those edges

2. **Why does Prim's always pick available minimum edge?**
   - Answer: Always an edge from tree to non-tree; minimize that edge weight

3. **Can MST be non-unique?**
   - Answer: Yes, if multiple edges have same weight. Different MSTs with same total.

4. **How to verify an MST is optimal?**
   - Answer: Check all edges follow cut property; removing any edge increases total cost

5. **Why not use Dijkstra for MST?**
   - Answer: Dijkstra builds shortest paths from source; MST builds minimum total tree

**Self-Assessment:**
- [ ] Understand MST problem definition
- [ ] Can implement Kruskal's with Union-Find
- [ ] Can implement Prim's with priority queue
- [ ] Know when to use which algorithm
- [ ] Understand cut property proof

---

## 1️⃣1️⃣ RETENTION HOOK

**Kruskal's: "Sort Edges, Add If No Cycle"**
- Sort edges by weight
- Process minimum edges first
- Union-Find prevents cycles
- Add until V-1 edges

**Prim's: "Grow Tree From Seed"**
- Start with one node
- Always expand to nearest new node
- Repeat until all nodes added
- Edges form MST

---

## 1️⃣2️⃣ COGNITIVE LAYER INTEGRATION

### 🖥️ COMPUTATIONAL LENS: Why Kruskal's Needs Sorting

**The Hardware Reality:**

```
Kruskal's bottleneck: E log E sorting
  Comparison: O(E log E)
  For E = 1M edges: log(1M) ≈ 20
  Total comparisons: 20M
  Each comparison: 3-5 cycles = 60M-100M cycles
  
Union-Find is fast:
  O(E × α(V)) where α(V) ≈ 4
  For E = 1M: 4M union operations
  Each operation: ~5 cycles = 20M cycles
  
Total time dominated by sorting, not Union-Find!

For dense graph (E = V²):
  E log E = V² log V
  More expensive than Prim's O((V+E) log V)
  
For sparse (E = V):
  E log E = V log V
  Faster than Prim's O(V log V) (assuming good constants)
```

---

### 🧠 PSYCHOLOGICAL LENS: Why Kruskal's Seems Simple

**Misconception: "Kruskal's is obvious"**

Student thinks: "Just sort edges, add them if no cycle. That's it."

Reality:
- Checking "no cycle" requires Union-Find
- Union-Find itself is non-trivial
- Implementation details matter greatly
- Path compression + union by rank = near-O(1)
- Without optimizations = O(log V) per operation

Correction: Kruskal's simplicity hides complexity in Union-Find

**Misconception: "Prim's with heap is always better"**

Student thinks: "Heap makes everything O(log V), so Prim's is best"

Reality:
- Kruskal's O(E log E) better for sparse (E = O(V))
- Prim's O((V+E) log V) better for dense (E = V²)
- Implementation complexity matters
- Sometimes simpler code > better complexity

Correction: Algorithm choice depends on graph density

---

### 🔄 DESIGN TRADE-OFF LENS: Kruskal vs Prim

**Decision Matrix:**

```
Sparse graph (E ≈ V):
  Kruskal: O(V log V) sorting dominated
  Prim: O(V log V) with heap
  Similar! Pick simpler: Kruskal

Dense graph (E ≈ V²):
  Kruskal: O(V² log V) sorting kills it
  Prim: O(V² log V) with heap is better
  Pick: Prim

Implementation Simplicity:
  Kruskal: sort + Union-Find (two clear concepts)
  Prim: priority queue (more state management)
  Preference: Kruskal (simpler mental model)

Parallel Computing:
  Kruskal: each component can process independently
  Borůvka's variant: naturally parallelizable
  Prim: hard to parallelize (inherently sequential)
```

---

### 🤖 AI/ML ANALOGY LENS: MST in Clustering

**Connection: Agglomerative Clustering**

```
Hierarchical clustering:
  Start with each point as cluster
  Merge closest clusters
  Repeat until one cluster
  
MST Connection:
  Treat clusters as nodes
  Edge weight = distance between clusters
  Single-linkage clustering = MST property
  
Implementation:
  Build MST of points
  Remove heavy edges
  Remaining components = clusters
  
This is why MST used in clustering!
  Finds natural cluster boundaries
```

---

### 📚 HISTORICAL CONTEXT LENS: From Theory to Practice

**The Evolution:**

```
1956: Kruskal's algorithm discovered
      Simple edge-based approach
      "Just sort and build"
      
1957: Prim's algorithm discovered
      Tree-based approach
      "Start from node and grow"
      
Both provably optimal (cut property)
      
1960s: Union-Find structure invented (Fisher)
       Makes Kruskal's practical
       Path compression discovered (Hopcroft)
       
1970s: Union-find optimized (Ackermann inverse)
       O(E log E) becomes O(E α(V))
       α(V) ≈ 4 for practical sizes
       
1980s-90s: Linear MST algorithms discovered
           Not just for comparison-based
           Special structures (integer weights)
           
Now: Standard algorithms in use
     Kruskal's for simplicity
     Prim's for dense graphs
     Borůvka's for parallelization
```

---

## SUMMARY

**Minimum Spanning Tree:**
- Connect all V nodes with exactly V-1 edges
- Minimize total edge weight
- No cycles (tree property)

**Kruskal's Algorithm:**
- Sort edges by weight
- Use Union-Find to detect cycles
- Add edges greedily
- Time: O(E log E), Space: O(V + E)
- Better for sparse graphs

**Prim's Algorithm:**
- Start with one node
- Grow tree by adding minimum edge to new node
- Use priority queue
- Time: O((V+E) log V), Space: O(V + E)
- Better for dense graphs

**When To Use:**
- Sparse: Kruskal's (simpler, faster)
- Dense: Prim's (better complexity)
- Interview: Either (explain trade-offs)

---

**End of Day 3: Minimum Spanning Trees**  
**Next:** Day 4 - Network Flow I (Max Flow Basics)

