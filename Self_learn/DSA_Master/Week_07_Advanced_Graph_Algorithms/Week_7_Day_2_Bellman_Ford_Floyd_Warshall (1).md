# Week 7, Day 2: Bellman-Ford & Floyd-Warshall

**Week:** 7 | **Day:** 2 | **Topic:** Bellman-Ford & Floyd-Warshall Algorithms  
**Difficulty:** Hard | **Time:** 100 minutes | **Prerequisites:** Week 7 Day 1

---

## 1️⃣ THE WHY

**Problem Context:**
Some graphs have negative edge weights (e.g., profit instead of cost). Dijkstra fails on negative weights. We need algorithms that handle:
- Negative edge weights
- Detection of negative cycles
- All-pairs shortest paths (not just single-source)

**Why Two Algorithms:**

**Bellman-Ford (Single-Source, Negative Weights):**
- Handles negative weights ✓
- Detects negative cycles ✓
- Slower: O(V × E) = quadratic
- Use when you must handle negatives

**Floyd-Warshall (All-Pairs):**
- Finds shortest path between ALL pairs
- Handles negative weights ✓
- Detects negative cycles ✓
- O(V³) but simpler implementation
- Use when you need all pairs

---

## 2️⃣ THE WHAT

**Algorithm 1: Bellman-Ford**

```
Bellman-Ford Algorithm:

Input: Graph G, source node s
Output: Shortest distances from s (or "negative cycle detected")

1. Initialize: dist[s] = 0, all others = infinity
2. Relax edges V-1 times:
   For each edge (u,v) with weight w:
     If dist[u] + w < dist[v]:
       dist[v] = dist[u] + w
3. Check for negative cycle:
   For each edge (u,v) with weight w:
     If dist[u] + w < dist[v]:
       Return "negative cycle detected"
4. Return distances

Key Insight: If we relax edges V-1 times, shortest paths are found
             If Vth relaxation still improves distances → negative cycle exists
```

**Algorithm 2: Floyd-Warshall**

```
Floyd-Warshall Algorithm:

Input: Graph G (weighted adjacency matrix)
Output: All-pairs shortest path distances

1. Initialize: dist[i][j] = weight of edge (i,j)
2. For each intermediate node k from 0 to V-1:
   For each pair (i,j):
     dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
3. Return dist matrix

Key Insight: Try routing through each intermediate node k
             If path i→k→j shorter, use it
             Order matters: process k in order for correctness
```

---

## 3️⃣ THE HOW

**Bellman-Ford Example:**

```
Graph: A -1-> B
       B -3-> C
       C --(-2)--> D
       A -4-> D

Bellman-Ford from A:

Initial: dist = {A: 0, B: ∞, C: ∞, D: ∞}

Relaxation 1:
  Edge A→B: 0 + 1 = 1 < ∞ → dist[B] = 1
  Edge B→C: 1 + 3 = 4 < ∞ → dist[C] = 4
  Edge C→D: 4 + (-2) = 2 < ∞ → dist[D] = 2
  Edge A→D: 0 + 4 = 4 ≮ 2 (no update)
  dist = {A: 0, B: 1, C: 4, D: 2}

Relaxation 2:
  Edge A→B: 0 + 1 = 1 ≮ 1 (no update)
  Edge B→C: 1 + 3 = 4 ≮ 4 (no update)
  Edge C→D: 4 + (-2) = 2 ≮ 2 (no update)
  Edge A→D: 0 + 4 = 4 > 2 (no update)
  dist = {A: 0, B: 1, C: 4, D: 2} (stable)

Relaxation 3 (not needed, but shows stability):
  No changes

Result: Shortest distances from A
  A→A: 0
  A→B: 1
  A→C: 4
  A→D: 2 (via B and C with negative edge)
```

**Floyd-Warshall Example:**

```
Graph (as matrix, ∞ = no edge):
     A   B   C   D
  A  0   1   ∞   4
  B  ∞   0   3   ∞
  C  ∞   ∞   0  -2
  D  ∞   ∞   ∞   0

Floyd-Warshall (try intermediate nodes):

k = A (routes through A):
  No improvement (A is source for most)

k = B (routes through B):
  Try A→B→C: 1 + 3 = 4 (no improvement, A has no path to C)
  Actually: no improvements because B not connected to A from left

k = C (routes through C):
  A→C: doesn't exist
  B→C: 3, B→C→D: 3 + (-2) = 1 > ∞ (improves!)
  dist[B][D] = 1

k = D (routes through D):
  Check all paths through D
  No improvements (D is sink)

Final Matrix:
     A   B   C   D
  A  0   1   4   2
  B  ∞   0   3   1
  C  ∞   ∞   0  -2
  D  ∞   ∞   ∞   0

All pairs shortest paths computed!
```

**Implementation (Python):**

```python
# Bellman-Ford
def bellman_ford(graph, n, start):
    dist = [float('inf')] * n
    dist[start] = 0
    
    # Relax edges V-1 times
    for _ in range(n - 1):
        for u in range(n):
            for v, weight in graph[u]:
                if dist[u] + weight < dist[v]:
                    dist[v] = dist[u] + weight
    
    # Check for negative cycle
    for u in range(n):
        for v, weight in graph[u]:
            if dist[u] + weight < dist[v]:
                return None  # Negative cycle detected
    
    return dist

# Floyd-Warshall
def floyd_warshall(graph, n):
    # Initialize distance matrix
    dist = [[float('inf')] * n for _ in range(n)]
    for i in range(n):
        dist[i][i] = 0
    
    for u in range(n):
        for v, weight in graph[u]:
            dist[u][v] = weight
    
    # Try routing through each intermediate node
    for k in range(n):
        for i in range(n):
            for j in range(n):
                if dist[i][k] + dist[k][j] < dist[i][j]:
                    dist[i][j] = dist[i][k] + dist[k][j]
    
    # Check for negative cycles
    for i in range(n):
        if dist[i][i] < 0:
            return None  # Negative cycle
    
    return dist
```

---

## 4️⃣ VISUALIZATION

**Bellman-Ford Relaxation Progression:**

```
Initial (before relaxation):
  A(0) --1--> B(∞)
  |            |
  4            |
  |            3
  |            |
  D(∞) <--(-2)- C(∞)

After Relaxation 1:
  A(0) --1--> B(1)
  |            |
  4            |
  |            3
  |            |
  D(2) <--(-2)- C(4)

After Relaxation 2:
  A(0) --1--> B(1)
  |            |
  4            |
  |            3
  |            |
  D(2) <--(-2)- C(4)
  [Stable - no more changes]
```

**Floyd-Warshall Grid Evolution:**

```
Initial matrix:
  [0  1  ∞  4]
  [∞  0  3  ∞]
  [∞  ∞  0 -2]
  [∞  ∞  ∞  0]

After k=B (route through B):
  [0  1  4  4]   ← Can't improve much
  [∞  0  3  1]   ← B→C→D improves B→D
  [∞  ∞  0 -2]
  [∞  ∞  ∞  0]

After k=C:
  [0  1  4  2]   ← A→B→C→D improves A→D
  [∞  0  3  1]
  [∞  ∞  0 -2]
  [∞  ∞  ∞  0]
```

---

## 5️⃣ COMPLEXITY ANALYSIS

**Bellman-Ford:**

```
Time Complexity:
  Relaxation loop: V-1 iterations
  Inner loop: iterate all E edges
  Per edge: O(1) comparison and update
  Total: O(V × E)

Example:
  V = 1000 nodes, E = 10,000 edges
  Bellman-Ford: 1000 × 10,000 = 10M operations
  Dijkstra: (1000 + 10,000) × log(1000) ≈ 110K operations
  Bellman-Ford 90x slower!

Space Complexity:
  Distance array: O(V)
  Adjacency list: O(V + E)
  Total: O(V + E)
```

**Floyd-Warshall:**

```
Time Complexity:
  Three nested loops (k, i, j)
  All range over V
  Per triple: O(1)
  Total: O(V³)

Example:
  V = 100 nodes
  Floyd-Warshall: 100³ = 1M operations
  Bellman-Ford: 100 × E
    If dense (E = 5000): 500K operations (2x faster)
    If sparse (E = 100): 10K operations (100x faster)

Space Complexity:
  Distance matrix: O(V²)
  No adjacency list needed
  Total: O(V²)
```

**When To Use Which:**

```
Single-source shortest path:
  Non-negative weights → Dijkstra O((V+E) log V)
  Negative weights → Bellman-Ford O(V × E)

All-pairs shortest path:
  V² queries expected → Floyd-Warshall O(V³)
  Few queries expected → Run Dijkstra V times O(V × (V+E) log V)
  Sparse graph → Bellman-Ford from each source O(V² × E)
```

---

## 6️⃣ SYSTEMS INTEGRATION

**Bellman-Ford Applications:**

1. **Currency Exchange:**
   - Currencies are nodes
   - Exchange rates are weights
   - Detect arbitrage (negative cycle)
   - Bellman-Ford finds negative cycles

2. **Network Routing (with negative weights):**
   - Profit-based routing (negative = gain)
   - OSPF uses shortest path, but variants handle negatives
   - Bellman-Ford more general

3. **Game Physics:**
   - Gravity/boosts = negative weights
   - Shortest path considering forces
   - Bellman-Ford handles this

**Floyd-Warshall Applications:**

1. **Small Network Analysis:**
   - LAN with <100 computers
   - Need all pairwise distances
   - Floyd-Warshall precompute once, query fast

2. **Transitive Closure:**
   - Is there a path from A to B?
   - Floyd-Warshall easily answers
   - Also handles distances

3. **Game Map Analysis:**
   - Small game worlds
   - Need all distances between checkpoints
   - Floyd-Warshall gives this in O(V³)

---

## 7️⃣ CROSSOVERS & VARIANTS

**Related to Dijkstra (Day 1):**
- Dijkstra: single-source, non-negative, O((V+E) log V)
- Bellman-Ford: single-source, negative allowed, O(V × E)
- Floyd-Warshall: all-pairs, negative allowed, O(V³)

**Advanced Variants:**

1. **SPFA (Shortest Path Faster Algorithm):**
   - Bellman-Ford with queue optimization
   - Average O(E), worst case O(V × E)
   - Practical speedup over Bellman-Ford

2. **Dijkstra with Potential Function:**
   - Reweight edges using potential
   - Makes weights non-negative
   - Run Dijkstra (faster than Bellman-Ford)
   - Requires preprocessing

3. **Johnson's Algorithm:**
   - Bellman-Ford once to get potential
   - Dijkstra from each source V times
   - Overall: O(V² log V + V × E)
   - Better than Floyd-Warshall for sparse graphs

---

## 8️⃣ THEORY & PROOF

**Why Bellman-Ford Relaxation Works:**

```
Claim: After k relaxations, shortest paths of length ≤ k edges are correct

Proof by induction:
  Base case (k=0): dist[s] = 0 correct (source)
  
  Inductive step: Assume true for k-1
    If shortest path to v has ≤ k edges:
      Must go through some node u
      Distance to u found in ≤ k-1 relaxations (induction hypothesis)
      Relaxation k will find u→v edge
      Updates dist[v] correctly
    
  Conclusion: After V-1 relaxations, all shortest paths found
```

**Why Floyd-Warshall Works:**

```
Claim: After processing node k, dist[i][j] = shortest path i→j using only 0..k as intermediate

Proof by induction on k:
  Base case (k=0): Direct edges only (correct)
  
  Inductive step: Assume true for k-1
    Shortest path i→j using 0..k either:
      1. Doesn't use k: equals dist[i][j] from k-1 (induction)
      2. Uses k: equals dist[i][k] + dist[k][j] (both use ≤k-1)
    
    min(option1, option2) = correct path
    
    Formula: dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
    
  Conclusion: After processing all k, correct all-pairs distances
```

---

## 9️⃣ INTUITION & MENTAL MODELS

**Bellman-Ford: The Optimist's Algorithm**

Imagine a message being relayed through network:
- Each person (node) keeps current distance estimate
- When hearing about path from someone else, checks if it's better
- Repeats message-passing V-1 times
- If message still improving at V-1 iterations → cycle that improves = negative cycle

**Floyd-Warshall: The Meeting Point**

For each pair of nodes (A, Z):
- Try having them meet at intermediate node B
- If A→B→Z shorter than A→Z directly, update
- Try all possible meeting points
- Eventually find shortest path

---

## 🔟 KNOWLEDGE CHECK

**Questions:**

1. **Why V-1 relaxations enough for Bellman-Ford?**
   - Answer: Longest shortest path = V-1 edges (visiting each node once)

2. **How to detect negative cycle in Bellman-Ford?**
   - Answer: After V-1 relaxations, try relaxing again; if any update, cycle exists

3. **Why is Floyd-Warshall order-dependent (k must go outer)?**
   - Answer: Must use all intermediate nodes; processing k ensures 0..k all available as intermediates

4. **When would Floyd-Warshall be faster than Bellman-Ford?**
   - Answer: Dense graphs (E close to V²); O(V³) beats O(V×E)

5. **How to use Floyd-Warshall for transitive closure?**
   - Answer: dist[i][j] = 0 if i=j, 1 if edge, ∞ otherwise; then min becomes OR

**Self-Assessment:**
- [ ] Understand Bellman-Ford relaxation concept
- [ ] Can implement Bellman-Ford with cycle detection
- [ ] Understand Floyd-Warshall k-intermediate-node ordering
- [ ] Can choose between algorithms based on problem
- [ ] Know complexity trade-offs

---

## 1️⃣1️⃣ RETENTION HOOK

**Bellman-Ford: "Relax All Edges, V-1 Times"**
- This is it: brute force relaxation
- Simple but correct
- Check Vth iteration for negative cycle

**Floyd-Warshall: "Try All Meeting Points"**
- For each pair, try meeting at each intermediate
- If shorter route through meeting point, use it
- Process intermediates in order

---

## 1️⃣2️⃣ COGNITIVE LAYER INTEGRATION

### 🖥️ COMPUTATIONAL LENS: Why Bellman-Ford Is So Slow

**The Hardware Reality:**

```
Bellman-Ford:
  Relaxation loop: V-1 iterations
  Each iteration: scan all E edges
  Memory access: edges stored in adjacency list
  
Cache behavior:
  Edge iteration: sequential (good prefetch)
  But must repeat V-1 times
  Many redundant accesses
  
For V=1000, E=10K:
  Total iterations: 1000 × 10K = 10M edge checks
  Each check: ~1-2 cache cycles
  Total: ~20M cycles

Dijkstra:
  Single pass through V nodes
  Heap extractions: O(log V)
  Total: ~(V log V + E) = ~220K cycles
  
Difference: Bellman-Ford has to be correct even with negative weights
           This correctness cost is O(V×E)
```

---

### 🧠 PSYCHOLOGICAL LENS: Why Students Confuse These

**Misconception 1: "Why Not Use Bellman-Ford Always?"**

Student thinks: "If Bellman-Ford handles negatives, why not use it always?"

Reality:
- Bellman-Ford O(V×E) much slower
- Dijkstra O((V+E) log V) much faster
- For non-negative: Dijkstra 10-100x faster
- Use Bellman-Ford only if negative weights required

**Misconception 2: "Floyd-Warshall Computes Everything?"**

Student thinks: "Floyd-Warshall computes all pairs, so it's the best"

Reality:
- Floyd-Warshall O(V³) = 1B operations for V=1000
- Dijkstra V times: V×(V+E) log V = 220M for sparse
- Floyd only better for small graphs or very dense
- Trade-off: simplicity vs efficiency

---

### 🔄 DESIGN TRADE-OFF LENS: Algorithm Choice

**Decision Tree:**

```
Do you have negative weights?
  NO → Use Dijkstra (fastest)
  YES → Next question

Need all-pairs distances?
  NO → Use Bellman-Ford (single-source)
  YES → Next question

Graph size?
  Small (V < 100) → Floyd-Warshall (simpler code)
  Large → Johnson's or repeated Dijkstra
```

---

### 🤖 AI/ML ANALOGY LENS: Bellman-Ford in RL

**Connection: Value Iteration**

```
Reinforcement learning value iteration:
  V[s] = max reward from state s
  
Update rule:
  V[s] = r(s) + γ × max V[s']
  
This is exactly Bellman-Ford relaxation!
  States = nodes
  Rewards = edge weights
  Relaxation = value update
  
Convergence: Same principle as Bellman-Ford
             After V iterations, converges
```

---

### 📚 HISTORICAL CONTEXT LENS: When We Need Negatives

**The Evolution:**

```
1950s: Dijkstra solves non-negative case
       Problem solved, very efficient

1958: Bellman & Ford independently discover
      Handle negative weights
      Necessary for some applications
      
But: Why ever have negative weights?
     Most real graphs are non-negative
     
Answer: Some applications use profit (negative cost)
        Arbitrage in currency exchange
        Bonus rewards in games
        
Modern usage:
  Bellman-Ford rarely used (negative weight rare)
  Floyd-Warshall for small all-pairs problems
  Most: Dijkstra for non-negative (which is most cases)
```

---

## SUMMARY

**Bellman-Ford:**
- Single-source shortest path
- Handles negative weights
- Detects negative cycles
- Time: O(V × E), Space: O(V + E)
- Use when negative weights required

**Floyd-Warshall:**
- All-pairs shortest path
- Handles negative weights
- O(V³) time, O(V²) space
- Simple implementation
- Use for small graphs or when all pairs needed

**Decision Guide:**
- Non-negative + single-source: Dijkstra
- Negative + single-source: Bellman-Ford
- All-pairs + small: Floyd-Warshall
- All-pairs + large: Dijkstra × V or Johnson's

---

**End of Day 2: Bellman-Ford & Floyd-Warshall**  
**Next:** Day 3 - Minimum Spanning Trees (Kruskal's & Prim's)

