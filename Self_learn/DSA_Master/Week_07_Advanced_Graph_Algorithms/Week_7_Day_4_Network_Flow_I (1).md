# Week 7, Day 4: Network Flow I - Max Flow Basics

**Week:** 7 | **Day:** 4 | **Topic:** Maximum Flow & Ford-Fulkerson Algorithm  
**Difficulty:** Hard | **Time:** 110 minutes | **Prerequisites:** Week 7 Days 1-3, Week 6

---

## 1️⃣ THE WHY

**Problem Context:**
You operate a water distribution system. Water flows from a source through pipes with capacity limits to a destination sink. Find the maximum water that can flow from source to sink simultaneously respecting capacity constraints.

This is the **Maximum Flow Problem**.

**Why Network Flow:**
- Fundamental in optimization
- Applications: routing, scheduling, bipartite matching
- Foundation for advanced problems (min-cut, circulation)
- Real-world: logistics, telecommunications

**Historical Significance:**
Ford & Fulkerson (1956) proved the max-flow min-cut theorem: maximum flow equals minimum cut capacity.

---

## 2️⃣ THE WHAT

**Maximum Flow Definition:**

```
Network Flow Graph:
  Directed edges with capacities
  Single source (s) and sink (t)
  Flow on edge ≤ capacity
  
Flow Conservation (Kirchoff's Law):
  At each node (except s, t):
    Incoming flow = Outgoing flow
  Source: outgoing flow ≥ incoming
  Sink: incoming flow ≥ outgoing

Maximum Flow Problem:
  Find flow assignment such that:
    - Respects capacity constraints
    - Satisfies flow conservation
    - Maximizes total flow from s to t
```

**Ford-Fulkerson Algorithm:**

```
Ford-Fulkerson Method (Not exact algorithm, framework):

Input: Flow graph, source s, sink t
Output: Maximum flow value

1. Initialize all flows to 0
2. While there exists augmenting path from s to t:
   a. Find path (any method, e.g., DFS/BFS)
   b. Compute bottleneck capacity (min capacity on path)
   c. Augment flow by bottleneck along entire path
   d. Update residual capacities
3. Return total flow

Key Insight: Keep finding ways to push more flow until blocked
             Residual graph shows remaining capacity + reverse edges
```

---

## 3️⃣ THE HOW

**Step-by-Step Example:**

```
Network: s → A → t
         s → B → t
         A → B
         
Capacities:
  s→A: 10
  s→B: 10
  A→B: 2
  A→t: 10
  B→t: 10

Ford-Fulkerson:

Initial: All flows = 0, total flow = 0

Iteration 1: Find augmenting path s→A→t
  Capacity: min(10, 10) = 10
  Augment by 10
  Flows: s→A=10, A→t=10
  Total flow = 10

Iteration 2: Find augmenting path s→B→t
  Capacity: min(10, 10) = 10
  Augment by 10
  Flows: s→B=10, B→t=10
  Total flow = 20

Iteration 3: Find augmenting path s→A→B→t
  Capacity: min(10-10, 2, 10-10) = 0 (A saturated)
  Actually: capacity is min(residual s→A, residual A→B, residual B→t)
           = min(0, 2, 0) = 0
  No augmentation possible!
  
  Alternative: s→B→A (reverse) →t
  This uses backward edge! (residual graph)
  Capacity: min(10-10 reverse, 2 forward, 10-10 reverse) = 0
  Also blocked

No more augmenting paths → Done

Maximum flow = 20
```

**Residual Graph Concept:**

```
Original edge u→v with capacity c and current flow f:
  Forward residual capacity: c - f (can push more)
  Backward residual capacity: f (can undo/reroute)

Residual graph includes both directions:
  Forward: u→v with residual capacity c - f
  Backward: v→u with residual capacity f

Augmenting path uses both forward and backward edges
```

**Implementation (Python):**

```python
from collections import defaultdict, deque

def max_flow_ford_fulkerson(graph, source, sink):
    # graph[u] = [(v, capacity), ...]
    
    # Create residual graph
    residual = defaultdict(lambda: defaultdict(int))
    for u in graph:
        for v, cap in graph[u]:
            residual[u][v] += cap
    
    def bfs(source, sink):
        """Find augmenting path using BFS"""
        parent = {source: None}
        visited = {source}
        queue = deque([source])
        
        while queue:
            u = queue.popleft()
            if u == sink:
                return parent
            
            for v in residual[u]:
                if v not in visited and residual[u][v] > 0:
                    visited.add(v)
                    parent[v] = u
                    queue.append(v)
        
        return None
    
    max_flow = 0
    
    while True:
        parent = bfs(source, sink)
        if parent is None:
            break
        
        # Find bottleneck capacity
        path_flow = float('inf')
        v = sink
        while parent[v] is not None:
            u = parent[v]
            path_flow = min(path_flow, residual[u][v])
            v = u
        
        # Augment flow
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

**Augmenting Path Visualization:**

```
Initial Flow: 0

Graph:     s ----10---- A ----10---- t
           |            |
           |--10--B-----10--|
           |        2       |
           +--------+-------+

Path 1: s→A→t (flow=10)
           s -10→ A -10→ t
           B remains dry

Path 2: s→B→t (flow=10)
           s -10→ B -10→ t
           Connection A↔B unused

Bottleneck in s→A→B→t:
           A already has 10/10 outflow
           Can't increase

Residual graph shows:
  s→A: 0 remaining (forward), 10 backward
  A→t: 0 remaining (forward), 10 backward
  s→B: 0 remaining (forward), 10 backward
  B→t: 0 remaining (forward), 10 backward
```

---

## 5️⃣ COMPLEXITY ANALYSIS

**Ford-Fulkerson Time Complexity:**

```
With DFS (naive):
  Number of augmentations: O(E × max_flow)
  Each augmentation: O(V + E) for DFS
  Total: O((V + E) × E × max_flow)
  
  Problem: max_flow can be arbitrarily large!
  If capacities are large: extremely slow
  
With BFS (Edmonds-Karp):
  Number of augmentations: O(V × E)
  Each augmentation: O(V + E) for BFS
  Total: O((V + E) × V × E) = O(V × E²)
  
  Why BFS better? Finds shortest augmenting path
  Shortest path = fewest edges
  Limits augmentation iterations
```

**Why Capacity Matters:**

```
If capacities are integers 1 to C:
  Naive Ford-Fulkerson: O(E × C) augmentations
  Edmonds-Karp: O(V × E²) regardless of C
  
Edmonds-Karp is polynomial (doesn't depend on capacity values)
Ford-Fulkerson depends on input values (pseudo-polynomial)

For competition/interview:
  Just mention Edmonds-Karp for polynomial time
  Or scaling algorithms for large capacities
```

**Space Complexity:**
```
Residual graph storage: O(V + E)
DFS/BFS stack/queue: O(V)
Total: O(V + E)
```

---

## 6️⃣ SYSTEMS INTEGRATION

**Real-World Applications:**

1. **Network Routing:**
   - Telecom: maximum throughput between cities
   - Internet: find bottleneck capacities
   - Optimize traffic flow

2. **Airline Scheduling:**
   - Maximize passenger flow through hubs
   - Capacity: flights, seats per flight
   - Find maximum routing

3. **Bipartite Matching:**
   - Source → people, sink → jobs
   - Edge capacity = 1
   - Max flow = maximum matching size
   - Later (Day 5)

4. **Circulation with Demands:**
   - Ensure flow meets minimum demands
   - Extension of max flow
   - Production and distribution networks

---

## 7️⃣ CROSSOVERS & VARIANTS

**Related Algorithms:**

1. **Min-Cut (Day 5):**
   - Max-Flow Min-Cut Theorem
   - Maximum flow equals minimum cut
   - Cutting edges vs flowing through

2. **Dinic's Algorithm:**
   - Faster than Edmonds-Karp
   - Uses level graphs
   - Time: O(V² × E)

3. **Push-Relabel Algorithm:**
   - Preflow approach (different from augmenting path)
   - Time: O(V² × E) or O(V³)
   - Often faster in practice

4. **Scaling Algorithms:**
   - Process capacities from largest to smallest
   - Time: O(E² log C) where C = max capacity
   - Handles large capacities well

---

## 8️⃣ THEORY & PROOF

**Max-Flow Min-Cut Theorem (Sketch):**

```
Max-Flow Value = Min-Cut Capacity

Cut: Partition nodes into S (containing source) and T (containing sink)
Cut capacity: Sum of capacities from S to T

Proof intuition:
  If flow from s to t = F
  Then must cross some cut
  Cannot exceed cut capacity
  
  Conversely, can always find cut equal to max flow
  (The cut separating source side from sink side in final residual)
```

**Why Algorithm Terminates:**

```
Integer capacities (Ford-Fulkerson):
  Each augmentation increases flow by ≥ 1
  Max flow finite
  Terminates in finite steps
  
Polynomial-time variant (Edmonds-Karp):
  BFS ensures shortest augmenting path
  Shortest path length increases over time (monotonically)
  At most V distinct path lengths
  At most O(V × E) augmentations
```

---

## 9️⃣ INTUITION & MENTAL MODELS

**Water Flow Analogy:**

Imagine water pipes:
- Water flows from source to sink
- Each pipe has maximum flow capacity
- Water conservation: inflow = outflow at junctions
- Find total flow that can simultaneously flow through

Ford-Fulkerson = repeatedly finding new ways to push water through

**Residual Graph:**

Current solution isn't "locked in":
- Forward edges: spare capacity to increase flow
- Backward edges: ability to undo previous routing

Augmenting path finds new routes (including undoing previous)

---

## 🔟 KNOWLEDGE CHECK

**Questions:**

1. **Why do we need backward edges in residual graph?**
   - Answer: To reroute flow; undoing one path to enable another

2. **What's the bottleneck capacity on a path?**
   - Answer: Minimum residual capacity on any edge in the path

3. **How does BFS improve Ford-Fulkerson?**
   - Answer: Finds shortest augmenting path, limits total augmentations to O(VE)

4. **Can maximum flow be non-integer with integer capacities?**
   - Answer: No; integer capacities guarantee integer flow (integrality theorem)

5. **What if no augmenting path exists?**
   - Answer: Maximum flow reached; no more flow can be pushed

**Self-Assessment:**
- [ ] Understand max flow problem definition
- [ ] Can trace Ford-Fulkerson by hand
- [ ] Know why Edmonds-Karp is polynomial-time
- [ ] Understand residual graph concept
- [ ] Can implement basic version

---

## 1️⃣1️⃣ RETENTION HOOK

**Ford-Fulkerson: "Keep Finding Augmenting Paths"**

1. Initialize flow = 0
2. While augmenting path exists:
   - Find path from s to t in residual graph
   - Push flow along path (bottleneck = minimum capacity)
   - Update residual capacities
3. Return total flow

**Key Insight:** Residual graph enables rerouting through backward edges

---

## 1️⃣2️⃣ COGNITIVE LAYER INTEGRATION

### 🖥️ COMPUTATIONAL LENS: Why BFS Matters

**The Hardware Reality:**

```
Ford-Fulkerson with DFS:
  Bad case: finding longest path each time
  Example: diamond graph with irrational ratio capacities
  Could take exponential iterations!
  
Ford-Fulkerson with BFS (Edmonds-Karp):
  BFS finds shortest augmenting path
  Path length increases monotonically
  Bounded by O(V) distinct lengths
  At most O(E) iterations per path length
  Total: O(V × E²)
  
Practical difference:
  DFS: unbounded (depends on input structure)
  BFS: guaranteed polynomial
  
This is why algorithm choice matters!
```

---

### 🧠 PSYCHOLOGICAL LENS: Why Flow Is Hard

**Misconception: "Just find any path and push flow"**

Student thinks: "Greedy approach: pick path, push max flow, done?"

Reality:
- Greedy often suboptimal!
- Example: two 1-unit paths to sink, but middle edge splits them
  - Greedy picks one path, blocks the other
  - Optimal requires rerouting (using backward edges)
  
Residual graph enables rerouting that greedy misses

**Misconception: "Backward edges undo flow"**

Student thinks: "Backward edge = delete flow? That's wasteful"

Reality:
- Backward edge doesn't undo flow
- It represents ability to reroute
- Pushing backward = reducing previous flow on forward
- Allows rerouting to find better paths

---

### 🔄 DESIGN TRADE-OFF LENS: Algorithm Selection

**When Ford-Fulkerson Works:**

```
Small capacities: Use vanilla Ford-Fulkerson (DFS)
  Capacities = 1-10: fast enough
  Bounded iterations: ≤ 10 × edges
  
Integer capacities: Guaranteed to terminate
  Don't get stuck in fractions
  Final result is integral
```

**When Need Edmonds-Karp:**

```
Large capacities: Must use BFS
  Capacities = millions: polynomial-time critical
  DFS could take forever
  
Unknown structure: Use BFS
  Could have adversarial inputs
  BFS provides worst-case guarantee
```

**When Need Advanced Algorithms:**

```
Very large graphs: Use push-relabel
  V > 10000: faster in practice
  Dinic's: O(V² E) better for dense
  Scaling: O(E² log C) for huge capacities
```

---

### 🤖 AI/ML ANALOGY LENS: Flow in Neural Networks

**Connection: Information Flow in Attention**

```
Transformer attention:
  Query routes to values through attention weights
  This is like flow routing!
  
Bottleneck attention:
  Capacity limit on attention weights
  Maximum information that can flow
  Similar to network capacity
  
Optimization perspective:
  Maximize information flow to output
  Subject to capacity constraints
  This IS a flow problem!
```

---

### 📚 HISTORICAL CONTEXT LENS: From Theorem to Algorithm

**The Evolution:**

```
1956: Ford & Fulkerson publish max-flow min-cut theorem
      Prove equivalence of concepts
      Propose augmenting path method
      
1962: Edmonds & Karp analyze complexity
      Discover BFS makes polynomial-time
      O(VE²) bound proven
      
1970: Dinic develops faster algorithm
      Uses level graphs
      O(V²E) time
      
1980: Goldberg & Tarjan discover push-relabel
      Different approach: preflow
      Often faster in practice
      
1990s: Scaling algorithms for large capacities
      O(E² log C) independent of capacity values
      
2000s: Specialized algorithms for specific graphs
       Planar graphs, trees, etc.
       Problem-specific optimizations
       
Now: Multiple algorithms in practice
     Simple problems: Edmonds-Karp
     Complex: push-relabel
     Specialized: problem-specific
```

---

## SUMMARY

**Maximum Flow Problem:**
- Find maximum flow from source to sink
- Respect capacity and flow conservation constraints
- No cycles required (unlike trees)

**Ford-Fulkerson Method:**
- Augmenting path framework
- Add flow along any path from s to t (in residual graph)
- Residual graph enables rerouting

**Edmonds-Karp Algorithm:**
- Ford-Fulkerson using BFS
- Polynomial-time: O(VE²)
- Best for interviews/general use

**Key Concepts:**
- Residual graph: represents remaining capacity + undo capability
- Bottleneck: minimum capacity on augmenting path
- Max-Flow Min-Cut: maximum flow = minimum cut capacity

---

**End of Day 4: Maximum Flow Basics**  
**Next:** Day 5 - Network Flow II (Min-Cut, Bipartite Matching, Advanced Flow)

