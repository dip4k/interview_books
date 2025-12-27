# Week 6, Day 1: Graph Representations

## 🗓 Metadata
**Week:** 6 | **Day:** 1 of 5 | **Topic:** Graph Representations  
**Category:** Graph Fundamentals | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-5.5 (Arrays, Trees, all prior patterns)  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Model social networks, web pages, road networks, dependencies. Need efficient representation. Adjacency matrix? O(n²) space even for sparse graphs. Adjacency list? O(n+m) space, but different trade-offs. Which to choose?

**Design Problems Solved:**
- Social network relationships (Facebook friends)
- Web page links (Google's web graph)
- Road networks (GPS, routing)
- Dependency resolution (package managers)
- Airline routes and flights
- Computer networks and routing
- Recommendation systems (user-product connections)

**Real System Usage:**
- **Google:** Web graph with billions of pages, adjacency lists (trillions of links)
- **Facebook:** Social graph, adjacency lists + caches
- **LinkedIn:** Connection graph, optimized representations
- **GPS/Maps:** Road network, adjacency lists + spatial indexing
- **Netflix:** Recommendation graph, sparse adjacency lists
- **Package Managers (npm, pip):** Dependency DAG, adjacency lists
- **Router Software:** Network topology, adjacency lists with weights

**Why Graph Representations Matter:**
Choosing right representation determines algorithm efficiency. Social networks: sparse, prefer lists. Dense graphs: matrices sometimes better. Space-time trade-offs critical for billion-node graphs.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think of graph like **contact list in your phone**. Adjacency matrix = page for every person, mark who they know (wasteful space for sparse contacts). Adjacency list = each person's entry lists only their actual contacts (efficient).

```
Social Network: 4 people (A, B, C, D)
Connections: A↔B, B↔C, C↔D

Adjacency Matrix:
     A  B  C  D
  A [0, 1, 0, 0]
  B [1, 0, 1, 0]
  C [0, 1, 0, 1]
  D [0, 0, 1, 0]

Space: O(4²) = 16 cells, but only 6 edges!

Adjacency List:
  A: [B]
  B: [A, C]
  C: [B, D]
  D: [C]

Space: O(4 + 2×4) = 12 (vertices + edges)
```

**Key Invariants:**
1. **Directed vs Undirected:** Directed has direction, undirected symmetric
2. **Weighted vs Unweighted:** Weighted has edge costs, unweighted all 1
3. **Sparse vs Dense:** Sparse m << n², dense m ≈ n²
4. **Representation trade-off:** Matrix O(n²) space, O(1) edge check. List O(n+m) space, O(degree) edge check.

**Visual Representation:**

```
Example Directed Graph:
    A → B
    ↓   ↓
    C ← D

Adjacency List:
  A: [B, C]
  B: [D]
  C: [D]
  D: []

Adjacency Matrix:
     A  B  C  D
  A [0, 1, 1, 0]
  B [0, 0, 0, 1]
  C [0, 0, 0, 1]
  D [0, 0, 0, 0]

Edge List:
  [(A,B), (A,C), (B,D), (C,D)]
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `n`: number of vertices
- `m`: number of edges
- `directed`: boolean (true = directed, false = undirected)

**Representation 1: Adjacency Matrix**
```
1. Create n×n 2D array
2. For each edge (u, v):
     a. matrix[u][v] = 1 (or weight for weighted)
     b. If undirected: matrix[v][u] = 1
3. Access: matrix[u][v] = O(1)
4. Iterate neighbors of u: O(n) scan row

Space: O(n²)
Edge check: O(1)
Iterate neighbors: O(n)
Add edge: O(1)
Remove edge: O(1)
```

**Representation 2: Adjacency List**
```
1. Create array of size n (or hash map)
2. Each element is list of neighbors
3. For each edge (u, v):
     a. list[u].append(v)
     b. If undirected: list[v].append(u)
4. Access neighbor: list[u] = O(1), iterate = O(degree)

Space: O(n + m)
Edge check: O(degree) scan list
Iterate neighbors: O(degree)
Add edge: O(1) amortized
Remove edge: O(degree)
```

**Representation 3: Edge List**
```
1. Create list of edges
2. Each edge = (u, v) or (u, v, weight)
3. For iteration, scan all m edges
4. Not primary representation, but useful for some algorithms

Space: O(m)
Edge check: O(m)
Iterate neighbors: O(m)
Add edge: O(1) amortized
Remove edge: O(m)
```

**Memory Behavior:**
- Adjacency matrix: Dense block of memory, cache-friendly for dense graphs, terrible for sparse
- Adjacency list: Scattered memory, potential cache misses, but only allocates needed space
- Edge list: Compact, but slow to query

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Build graph from edges for social network**

```
Edges (undirected):
(Alice, Bob), (Alice, Charlie), (Bob, Charlie), (Charlie, David)

Adjacency List (best for sparse):
  Alice: [Bob, Charlie]
  Bob: [Alice, Charlie]
  Charlie: [Alice, Bob, David]
  David: [Charlie]

Size: 4 + 2×4 = 12 (4 vertices + 8 directed edges)

Adjacency Matrix (wasteful):
       A  B  C  D
    A [0, 1, 1, 0]
    B [1, 0, 1, 0]
    C [1, 1, 0, 1]
    D [0, 0, 1, 0]

Size: 16 (4² regardless of edges)

For 4 people with 4 edges:
List: 12 units
Matrix: 16 units (not much difference)

But for 1000 people with 4000 edges:
List: 1,000 + 8,000 = 9,000 units
Matrix: 1,000,000 units (100x worse!)
```

**Example 2: Weighted directed graph (flight routes)**

```
Flights (directed with distance):
(New York → Los Angeles, 2500)
(New York → Chicago, 800)
(Chicago → Los Angeles, 2000)
(Los Angeles → Chicago, 2000)

Adjacency List:
  New York: [(Los Angeles, 2500), (Chicago, 800)]
  Chicago: [(Los Angeles, 2000)]
  Los Angeles: [(Chicago, 2000)]

Adjacency Matrix (distance, ∞ = no flight):
        NY    LA    CHI
  NY  [0,   2500,  800]
  LA  [∞,   0,     2000]
  CHI [∞,   2000,  0]

Edges: (NY→LA, NY→CHI, CHI→LA, LA→CHI) = 4 edges
List better: 3 + 2×4 = 11 vs 9 matrix cells
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Matrix | List | Edge List |
|-----------|--------|------|-----------|
| **Space** | O(n²) | O(n+m) | O(m) |
| **Edge check** | O(1) | O(degree) | O(m) |
| **Iterate neighbors** | O(n) | O(degree) | O(m) |
| **Add edge** | O(1) | O(1) amort | O(1) amort |
| **Remove edge** | O(1) | O(degree) | O(m) |
| **Sparse graph** | Bad | Good | Okay |
| **Dense graph** | Good | Okay | Bad |

**Key Insight:** Choose based on graph density and operations needed.

**Real Memory Behavior:**
- Matrix: Contiguous 2D array, good cache locality, wasteful for sparse
- List: Scattered pointers, poor cache locality for random access, efficient space
- For social networks (sparse), list typically 10-100x better space
- For dense problems, matrix acceptable

**Edge Cases & Failure Modes:**
- **Self-loops:** u→u allowed (mark matrix[u][u] = 1 or add u to list[u])
- **Multi-edges:** Multiple edges between same vertices (matrix counts, list duplicates or set)
- **Isolated vertices:** Matrix allocates space, list has empty entry
- **Very large n:** Matrix fails (1 billion vertices = 10^18 cells = impossible)
- **Directed vs undirected confusion:** Must handle symmetry correctly

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Google Web Graph:**
- Billions of pages, trillions of links (extremely sparse)
- Use adjacency lists (essential for space)
- Each page ID maps to list of outgoing links
- PageRank algorithm needs efficient neighbor iteration

**Social Networks (Facebook, LinkedIn):**
- Millions/billions of users, sparse connections
- Adjacency lists with caching
- Matrix impossible (10^18 cells for 1 billion users)
- Bidirectional edges (undirected graph)

**GPS/Navigation (Google Maps):**
- Millions of intersections, multiple road types
- Weighted directed graph (one-way streets, weights = distance)
- Adjacency lists with spatial indexing
- Dijkstra's needs efficient neighbor iteration

**Package Managers (npm, pip):**
- Dependency graph (directed, often DAG)
- Sparse: thousands of packages, millions of edges
- Adjacency lists for efficient traversal
- Topological sort to resolve dependencies

**Computer Networks:**
- Routers = vertices, connections = edges
- Weighted (bandwidth), bidirectional
- Adjacency lists for routing tables
- Dijkstra's for shortest path

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Arrays (matrix storage)
- Hash tables (list implementation)
- Linked lists (adjacency list nodes)
- Basic data structures

**Built Upon By:**
- **Graph algorithms:** BFS, DFS, Dijkstra's, Prim's, Kruskal's
- **All Week 6+:** Every graph algorithm needs representation
- **Specialized variants:** Implicit graphs (game states), dynamic graphs (additions/deletions)

**Used In Algorithms:**
- BFS/DFS (need neighbor iteration)
- Shortest path (Dijkstra's, Bellman-Ford)
- Minimum spanning tree (Prim's, Kruskal's)
- Topological sort (dependency resolution)
- Union-Find (cycle detection, connectivity)

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Formal Definition:**
Graph G = (V, E) where:
- V = set of vertices (|V| = n)
- E = set of edges (|E| = m)
- Edge = (u, v) or (u, v, w) for weighted

**Sparse vs Dense:**
- Sparse: m = O(n) (few edges)
- Dense: m = O(n²) (many edges)
- Complete graph: m = n(n-1)/2 (all pairs connected)

**Space Complexity:**
- Matrix: Θ(n²) always
- List: Θ(n + m) — scales with actual edges
- Savings for sparse: If m = 1000n, list is 1001n vs n²

**Time Complexity (for key operations):**
- Check edge (u,v): Matrix O(1), List O(degree(u))
- Iterate all neighbors: Matrix O(n), List O(degree)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Adjacency Matrix:**

✅ **Use Matrix when:**
- Dense graph (m ≈ n²)
- Need O(1) edge lookup
- Small n (< 5000)
- Floyd-Warshall all-pairs shortest path

✅ **Examples:**
- Complete graphs
- Graph problems with dense connectivity
- Game grids (often O(n²) edges)

❌ **Don't use when:**
- Sparse graph (social networks, web)
- Very large n (billions of vertices)
- Memory limited
- Need efficient neighbor iteration

**When to Use Adjacency List:**

✅ **Use List when:**
- Sparse graph (m << n²)
- Efficient neighbor iteration needed
- Large n (millions/billions)
- Most real-world graphs

✅ **Examples:**
- Social networks
- Web graphs
- Road networks
- Dependency graphs

❌ **Don't use when:**
- Need O(1) edge lookup (check matrix)
- Dense complete graphs
- Simple dense problems (matrix clearer)

**Real-World Trade-offs:**

| Scenario | Choice | Reason |
|----------|--------|--------|
| **Social network** | List | Sparse, huge n |
| **Complete graph** | Matrix | Dense, all pairs |
| **Game grid** | List or implicit | Sparse neighbors |
| **Small dense problem** | Matrix | Clarity, fast lookup |

**Anti-patterns:**

❌ "Always use adjacency list" → Dense graphs may prefer matrix
❌ "Always use adjacency matrix" → Sparse graphs explode space
❌ "Use adjacency matrix for 1 billion vertices" → Impossible (10^18 cells)
❌ "Don't represent self-loops or multi-edges" → Handle correctly in implementation

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why does adjacency list use O(n+m) space while matrix uses O(n²)?

**Q2:** When is O(1) edge lookup (matrix) worth O(n²) space?

**Q3:** For sparse graphs, why is adjacency list 10-100x better than matrix?

**Q4:** How do you handle undirected edges in adjacency list? Why symmetric?

**Q5:** When would you use edge list over matrix or adjacency list?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Graph Representations: Adjacency Matrix (O(n²) space, O(1) lookup) vs Adjacency List (O(n+m) space, O(degree) lookup). Choose based on density.**

**Mnemonic:** "M.A.L." → Matrix (dense), Adjacency List (sparse), Learn trade-offs

**Cognitive Lenses:**

| **Computational** | Space O(n²) vs O(n+m). Lookup O(1) vs O(degree). Trade-off fundamental. |
| **Psychological** | Intuitive: matrix = full table, list = contacts only. Choose fit. |
| **Design Trade-off** | Space vs speed. Matrix: space wasteful, queries fast. List: space efficient, queries slower. |
| **AI/ML Analogy** | Similar to: dense vs sparse matrices in machine learning. Same trade-offs. |
| **Historical Context** | Matrix representation older (1950s). Lists dominated 1970s+. Real world needs sparse. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Build graph from edge list (adjacency list)
2. Build graph from adjacency matrix
3. Convert matrix to list and vice versa
4. Count edges in graph
5. Find vertex degree
6. Check if edge exists (given representation)
7. Add/remove edge
8. Find all neighbors of vertex

**Interview Q&A Highlights:**
- Adjacency matrix vs list: space/time trade-offs
- When use matrix vs list?
- How represent directed vs undirected?
- How represent weighted graphs?
- Space complexity for sparse vs dense?

**Common Misconceptions:**
- ❌ "Always use adjacency list" → ✅ Matrix better for dense graphs
- ❌ "Matrix is always O(n²)" → ✅ True, but acceptable for dense graphs
- ❌ "Can't use matrix for large graphs" → ✅ True for sparse, false for dense
- ❌ "List representation is always faster" → ✅ Only for neighbor iteration, not edge checks
- ❌ "Representation choice doesn't matter" → ✅ Critical for performance on real graphs

