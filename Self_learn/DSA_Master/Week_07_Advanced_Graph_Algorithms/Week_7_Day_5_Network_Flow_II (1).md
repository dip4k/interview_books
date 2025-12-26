# Week 7, Day 5: Network Flow II - Min-Cut, Bipartite Matching, Advanced Flow

**Week:** 7 | **Day:** 5 | **Topic:** Advanced Network Flow Applications  
**Difficulty:** Hard | **Time:** 120 minutes | **Prerequisites:** Week 7 Days 1-4

---

## 1️⃣ THE WHY

**Problem Context:**
Maximum flow is powerful, but we need deeper applications:
1. **Min-Cut:** Find minimum edges to remove to disconnect source from sink
2. **Bipartite Matching:** Match students to schools, jobs to candidates
3. **Advanced Flow:** Handling min-cost flows, circulation problems

**Why These Extensions:**
- Min-cut shows robustness of network (minimum failure points)
- Bipartite matching is fundamental matching problem
- Min-cost flow optimizes both flow and cost
- Together: solve real-world assignment and routing problems

---

## 2️⃣ THE WHAT

**Part 1: Min-Cut & Max-Flow Min-Cut Theorem**

```
Cut Definition:
  Partition nodes into S (source side) and T (sink side)
  Cut capacity = sum of edge weights from S to T
  
Min-Cut Problem:
  Find cut with minimum capacity
  
Max-Flow Min-Cut Theorem:
  Maximum flow value = minimum cut capacity
  
Consequence:
  Find max flow → find min cut
  Cut edges exactly match flow value
  Edges with saturated capacity (flow = capacity)
```

**Part 2: Bipartite Matching**

```
Bipartite Graph:
  Two sets of nodes (left L, right R)
  Edges only between L and R
  
Matching:
  Set of edges where no node used twice
  
Maximum Matching:
  Matching with maximum number of edges
  
Flow Network Conversion:
  Source → all left nodes (capacity 1)
  Left → right (capacity 1)
  Right nodes → sink (capacity 1)
  
  Max flow = maximum matching size!
```

**Part 3: Min-Cost Max-Flow**

```
Problem:
  Find maximum flow
  Among all max flows, minimize total cost
  Each edge has capacity and cost
  
Applications:
  Route flow with minimum transportation cost
  Minimize congestion penalties
  
Algorithms:
  Successive shortest path (uses Bellman-Ford)
  Cycle cancellation
```

---

## 3️⃣ THE HOW

**Min-Cut Finding:**

```
After running max-flow algorithm:

1. Perform BFS/DFS from source in residual graph
   - Only follow edges with residual capacity > 0
   
2. Mark reached nodes as S (source side)
   - All other nodes are T (sink side)
   
3. Find all edges from S to T with flow = capacity
   - These edges form min-cut
   - Cutting them disconnects source from sink

Example:
  After max-flow of 20:
  
  s → (A: flow=10, cap=10) → t
  s → (B: flow=10, cap=10) → t
  
  Cut {s|A,B,t}:
    Capacity = 10 + 10 = 20 ✓ Equals max-flow
```

**Bipartite Matching Example:**

```
Problem: Match students to projects
  Students: S1, S2, S3
  Projects: P1, P2, P3
  
  S1 interested in: P1, P2
  S2 interested in: P2, P3
  S3 interested in: P1, P3
  
Flow Network:
  source → S1 (cap=1)
  source → S2 (cap=1)
  source → S3 (cap=1)
  
  S1 → P1, P2 (cap=1)
  S2 → P2, P3 (cap=1)
  S3 → P1, P3 (cap=1)
  
  P1 → sink (cap=1)
  P2 → sink (cap=1)
  P3 → sink (cap=1)

Max-Flow:
  S1 → P1 → sink (flow=1)
  S2 → P2 → sink (flow=1)
  S3 → P3 → sink (flow=1)
  
  Max flow = 3 (all students matched!)
```

**Min-Cost Max-Flow Example:**

```
Network:
  s → A (cap=10, cost=1 per unit)
  s → B (cap=10, cost=2 per unit)
  A → t (cap=10, cost=1 per unit)
  B → t (cap=10, cost=1 per unit)
  
Max flow = 20 (send 10 through both paths)
Cost per unit:
  A route: 1 + 1 = 2
  B route: 2 + 1 = 3
  Total cost: 10×2 + 10×3 = 50
  
But could reroute to minimize:
  Send 10 through s→A→t (cost 20)
  Send 10 through s→B→t (cost 30)
  Total: 50 (same, A cheaper)
  
With ability to reroute:
  Could achieve lower cost if graph allows
```

**Implementation (Bipartite Matching):**

```python
from collections import deque, defaultdict

def max_bipartite_matching(left_adj, n_left, n_right):
    """
    left_adj[u] = list of right nodes u connects to
    Returns maximum matching size
    """
    
    # Build flow network
    # Node 0: source
    # Nodes 1..n_left: left vertices
    # Nodes (n_left+1)..(n_left+n_right): right vertices
    # Node n_left+n_right+1: sink
    
    source = 0
    sink = n_left + n_right + 1
    
    capacity = defaultdict(lambda: defaultdict(int))
    
    # Source to left
    for u in range(1, n_left + 1):
        capacity[source][u] = 1
    
    # Left to right
    for u in range(1, n_left + 1):
        for v in left_adj[u]:
            capacity[u][n_left + v] = 1
    
    # Right to sink
    for v in range(1, n_right + 1):
        capacity[n_left + v][sink] = 1
    
    # Run Edmonds-Karp (BFS-based Ford-Fulkerson)
    residual = defaultdict(lambda: defaultdict(int))
    for u in capacity:
        for v in capacity[u]:
            residual[u][v] = capacity[u][v]
    
    max_flow = 0
    
    while True:
        # BFS
        parent = {source: None}
        queue = deque([source])
        
        while queue and sink not in parent:
            u = queue.popleft()
            for v in residual[u]:
                if v not in parent and residual[u][v] > 0:
                    parent[v] = u
                    queue.append(v)
        
        if sink not in parent:
            break
        
        # Find bottleneck
        path_flow = float('inf')
        v = sink
        while parent[v] is not None:
            u = parent[v]
            path_flow = min(path_flow, residual[u][v])
            v = u
        
        # Augment
        v = sink
        while parent[v] is not None:
            u = parent[v]
            residual[u][v] -= path_flow
            residual[v][u] += path_flow
            v = u
        
        max_flow += path_flow
    
    return max_flow
```

---

## 4️⃣ VISUALIZATION

**Min-Cut Visualization:**

```
After max-flow computation:

Forward edges (saturated):
  s =10→ A =10→ t
  s =10→ B =10→ t

Residual graph:
  s ←10← A ←10← t
  s ←10← B ←10← t
  (Plus any unsaturated edges)

BFS from s in residual:
  Can reach: s, A, B (via reverse edges)
  Cannot reach: t (no path in residual)
  
Min-cut = S|T boundary:
  S = {s, A, B}
  T = {t}
  
Cut edges (s→t capacity):
  s→A (cap 10), s→B (cap 10)
  Total: 20 = max-flow ✓
```

**Bipartite Matching Visualization:**

```
Initial graph (bipartite):
  S1 ─────── P1
   ├─ P2     ├── sink
   └─ P3    
  S2 ─────── P2
   ├─ P1     ├── sink
   └─ P3
  S3 ─────── P3
   ├─ P2     ├── sink
   └─ P1

Max matching (3 pairs):
  S1 → P1 ✓
  S2 → P2 ✓
  S3 → P3 ✓
```

---

## 5️⃣ COMPLEXITY ANALYSIS

**Min-Cut Finding:**

```
After max-flow computed:
  BFS/DFS in residual graph: O(V + E)
  Finding cut edges: O(E)
  Total: O(V + E) additional after flow

Min-cut is free after max-flow!
```

**Bipartite Matching Using Flow:**

```
Network structure:
  V = n_left + n_right + 2 (source, sink)
  E = n_left + (edges) + n_right
    ≤ n_left + n_left×n_right + n_right
    = O(n_left × n_right) for complete bipartite

Max-flow using Edmonds-Karp:
  Time: O(V × E²) = O((L+R) × E²)
  For dense bipartite: E = L×R
  Time: O((L+R) × (L×R)²) = O((L+R)×L²×R²)

This seems bad, but:
  Hopcroft-Karp: O(E × √V)
  For bipartite: O(√(L+R) × edges)
  Better in practice
```

**Min-Cost Max-Flow:**

```
Using successive shortest paths:
  Run shortest-path max times
  Each shortest path: O(V × E) with Bellman-Ford
  Total: O(maxflow × V × E)
  
Can be slow if maxflow large!

Using cost-scaling:
  O(V² × E) independent of maxflow
  Better theoretical guarantee
```

---

## 6️⃣ SYSTEMS INTEGRATION

**Real-World Min-Cut Applications:**

1. **Network Robustness:**
   - Min-cut = minimum edges to disconnect network
   - Identifies critical infrastructure
   - Vulnerability analysis

2. **Image Segmentation:**
   - Pixels as nodes, edges between adjacent
   - Source = foreground, sink = background
   - Min-cut separates optimally

3. **Project Selection:**
   - Projects as nodes
   - Edges represent dependencies
   - Max profit with constraints = min-cut formulation

**Real-World Matching Applications:**

1. **Job Placement:**
   - Students to internships
   - Maximum number of placements
   - Each person gets at most one job

2. **School Assignments:**
   - Students to schools
   - Capacity constraints on schools
   - Variant: maximum matching with capacities

3. **Marriage Problem:**
   - Classic: bipartite matching
   - Real-world: more complex (preferences, stability)
   - Stable marriage ≠ max matching

---

## 7️⃣ CROSSOVERS & VARIANTS

**Flow-Based Reductions:**

1. **Maximum Matching → Max-Flow:**
   - Set all edge capacities to 1
   - Source/sink trick
   - Max-flow = matching size

2. **Minimum Vertex Cover → Max-Matching:**
   - In bipartite: vertex cover = 2-approximation of optimal
   - König's theorem: min vertex cover = max matching

3. **Maximum Independent Set:**
   - In bipartite: complement of min vertex cover
   - Can compute using max-flow

**Advanced Variants:**

1. **Circulation with Demands:**
   - Lower bounds on edge flows
   - Must satisfy demand constraints
   - Reduced to flow problem

2. **Multi-Commodity Flow:**
   - Multiple types of flow
   - Each has own source/sink
   - NP-hard in general

3. **Dynamic Flow:**
   - Flow through time
   - Time-dependent capacities
   - Applications: evacuation, traffic

---

## 8️⃣ THEORY & PROOF

**Max-Flow Min-Cut Theorem (Formal):**

```
Theorem:
  For any flow network, maximum flow value equals minimum cut capacity

Proof sketch:
  Direction 1 (Max-flow ≤ Min-cut):
    Flow must cross some cut
    Cannot exceed cut capacity
    So max-flow ≤ any cut capacity
    Therefore max-flow ≤ min-cut
  
  Direction 2 (Max-flow ≥ Min-cut):
    When Ford-Fulkerson terminates, no augmenting path exists
    Let S = source-reachable in residual graph
    Let T = sink (unreachable from S)
    
    For any edge u→v from S to T:
      Residual capacity = 0 (else path would exist)
      So flow = capacity (saturated)
    
    Sum of these flows = flow value
    Sum of these capacities = cut capacity
    
    Therefore flow = cut capacity
```

**König's Theorem (Bipartite Matching):**

```
Theorem:
  In bipartite graph, size of maximum matching = size of minimum vertex cover

Consequence:
  Can compute vertex cover using max-flow
  Maximum matching → Min vertex cover
```

---

## 9️⃣ INTUITION & MENTAL MODELS

**Min-Cut as Infrastructure:**

Think of network as infrastructure system:
- Min-cut = minimum pieces to destroy to disconnect
- Identifies critical dependencies
- Shows network vulnerabilities

**Bipartite Matching as Assignment:**

Think of matching as assigning resources:
- Each person gets one job (max)
- Each job filled by one person (max)
- Want maximum satisfaction (fill as many as possible)

---

## 🔟 KNOWLEDGE CHECK

**Questions:**

1. **Why is min-cut not just counting edge removal?**
   - Answer: Capacity matters; must remove total capacity, not just edges

2. **How does max-flow find min-cut?**
   - Answer: After max-flow, min-cut is edges from source-reachable to sink-unreachable in residual

3. **Can bipartite matching have cycles?**
   - Answer: No; matching is acyclic (uses each node once)

4. **Why use flow for bipartite matching?**
   - Answer: Unified framework; capacity 1 ensures matching property

5. **When would min-cost max-flow be needed?**
   - Answer: When minimizing cost matters, not just maximizing flow (e.g., cost of transportation)

**Self-Assessment:**
- [ ] Understand min-cut definition and finding
- [ ] Can convert bipartite matching to flow problem
- [ ] Know Max-Flow Min-Cut theorem
- [ ] Can identify when flow-based reduction applies
- [ ] Understand real-world applications

---

## 1️⃣1️⃣ RETENTION HOOK

**Min-Cut: "Edges With Saturated Flow From Source-Side"**
- Run max-flow
- Find reachable nodes in residual graph
- Min-cut = edges from reachable to unreachable
- Cut capacity = max-flow value

**Bipartite Matching: "Flow Network With Unit Capacities"**
- Source to left (cap 1)
- Left to right (cap 1)
- Right to sink (cap 1)
- Max-flow = maximum matching size

---

## 1️⃣2️⃣ COGNITIVE LAYER INTEGRATION

### 🖥️ COMPUTATIONAL LENS: Why BFS Is Essential in Matching

**The Hardware Reality:**

```
Naive matching (DFS):
  Find augmenting path (any path)
  Time: can be O(V × E)
  Total: O(maxflow) iterations
  
Hopcroft-Karp (BFS-based):
  Find shortest augmenting path
  Phases based on path length
  Time: O(√V × E)
  
For complete bipartite (V = L+R, E = L×R):
  Naive: O(L×R) augmentations
  Hopcroft-Karp: O(√(L+R) × L×R)
  
Difference scales dramatically!
  L=R=1000: Naive ~1M ops, Hopcroft-Karp ~100K ops
```

---

### 🧠 PSYCHOLOGICAL LENS: Why Matching Is Non-Obvious

**Misconception: "Greedy matching is optimal"**

Student thinks: "Just greedily match elements; works?"

Reality:
- Greedy matching often suboptimal
- Example: if greedy uses wrong edge early, blocks better matching
- Network flow finds globally optimal

Correction: Matching requires global optimization, not greedy

---

### 🔄 DESIGN TRADE-OFF LENS: When To Use Flow For Matching

**When Flow-based matching makes sense:**

```
Simple bipartite: Use network flow
  O(VE²) acceptable
  Easy to implement
  
Performance-critical: Use Hopcroft-Karp
  O(√V × E) much faster
  More complex implementation

With capacities: Use flow (capacitated matching)
  Some people can take multiple jobs
  No simple greedy solution
```

---

### 🤖 AI/ML ANALOGY LENS: Flow in Attention Mechanisms

**Connection: Optimal Transport in ML**

```
Optimal transport problem:
  Match source distribution to target
  Minimize cost of matching
  
This IS a flow problem!
  Sources and sinks
  Capacity = probability mass
  Cost = distance
  
Wasserstein distance:
  Uses optimal transport
  Related to min-cost flow
  
So deep learning sometimes solves flow problems!
```

---

### 📚 HISTORICAL CONTEXT LENS: From Theory to Practical Tools

**The Evolution:**

```
1956: Ford & Fulkerson prove max-flow min-cut
1970: König proves matching = vertex cover (bipartite)
      Connects matching to min-cost flow
      
1973: Hopcroft & Karp discover better matching algorithm
      √V improvement major breakthrough
      
1970s-80s: Practical implementations
           Network design problems
           Bipartite matching in real systems
           
1990s: Image segmentation using min-cut
       Computer vision breakthrough
       Min-cut widely adopted
       
2000s: Optimal transport in statistics
       Wasserstein distance
       Flow-based methods gain importance
       
Now: Multiple algorithms coexist
     Theory predicts best algorithm
     Practice uses specialized variants
```

---

## SUMMARY

**Min-Cut:**
- Minimum capacity partition separating source from sink
- Equals maximum flow (max-flow min-cut theorem)
- Found by reachability in residual graph after max-flow

**Bipartite Matching:**
- Maximum matching: most edges where no node used twice
- Flow network conversion: unit capacities, source/sink trick
- Max-flow = maximum matching size

**Min-Cost Max-Flow:**
- Find maximum flow with minimum total cost
- Applications: transportation, routing with costs
- Algorithms: successive shortest path, cost-scaling

**Real-World Applications:**
- Network robustness (min-cut)
- Job placement, school assignment (bipartite matching)
- Optimal transportation, routing (min-cost flow)

---

**End of Week 7: Advanced Graph Algorithms Complete**  
**Progression:** Dijkstra → Bellman-Ford/Floyd-Warshall → MST → Max-Flow → Advanced Applications  
**Next Week:** Week 8 - Specialized Structures (Tries, Segment Trees, Fenwick Trees)

