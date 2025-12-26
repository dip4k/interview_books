# Week 7, Day 4: Network Flow I - Max Flow Basics

**Week:** 7 | **Day:** 4 | **Topic:** Network Flow - Ford-Fulkerson Algorithm  
**Difficulty:** Hard | **Time:** 90 minutes | **Prerequisites:** Week 6-7 Days 1-3

---

## 1️⃣ THE WHY

**Problem Context:**
You have a water pipeline system from source S to sink T. Each pipe has a maximum capacity. What's the maximum water that can flow from S to T without exceeding any pipe's capacity? This is the **Maximum Flow Problem**.

**Why Max Flow Matters:**
- Model bottleneck capacity problems
- Applications: transportation, communication, matching
- Non-obvious problems reduce to flow
- Ford-Fulkerson is elegant greedy approach

**Historical Significance:**
- Ford & Fulkerson (1956): Pioneering algorithm
- Basis for all max flow algorithms
- Showed greedy can be optimal with augmenting paths

---

## 2️⃣ THE WHAT

**Core Concept:**

```
Flow Network:
  - Directed graph with capacities
  - Source S, sink T
  - Each edge has capacity c(u,v)
  
Valid Flow:
  - f(u,v) ≤ c(u,v) (capacity constraint)
  - f(u,v) = -f(v,u) (skew symmetry)
  - Σ f(u,v) = 0 for all u ≠ S,T (flow conservation)
  
Augmenting Path:
  - Path from S to T with available capacity
  - Can push more flow through this path
  - Find and use repeatedly until no path exists
```

**Key Insight:**

```
Greedy Approach:
  1. While there exists augmenting path:
  2. Find bottleneck capacity on path
  3. Add that amount to flow
  4. Mark edges as "used"
  
When no augmenting path exists:
  Maximum flow found (Max-Flow Min-Cut theorem)
```

---

## 3️⃣ THE HOW

**Ford-Fulkerson Algorithm:**

```python
def max_flow_ford_fulkerson(graph, source, sink):
    # Create residual graph (capacities)
    residual = {}
    for u in graph:
        residual[u] = {}
        for v, cap in graph[u]:
            residual[u][v] = cap
            if v not in residual:
                residual[v] = {}
            residual[v][u] = 0  # reverse edge
    
    max_flow = 0
    
    # While augmenting path exists
    while True:
        # Find augmenting path using BFS (Edmonds-Karp)
        path = bfs_find_path(residual, source, sink)
        if not path:
            break
        
        # Find bottleneck (minimum capacity on path)
        bottleneck = float('inf')
        for u, v in zip(path[:-1], path[1:]):
            bottleneck = min(bottleneck, residual[u][v])
        
        # Update residual capacities
        for u, v in zip(path[:-1], path[1:]):
            residual[u][v] -= bottleneck
            residual[v][u] += bottleneck
        
        max_flow += bottleneck
    
    return max_flow

def bfs_find_path(residual, source, sink):
    """Find path with available capacity using BFS"""
    from collections import deque
    queue = deque([(source, [source])])
    visited = {source}
    
    while queue:
        node, path = queue.popleft()
        if node == sink:
            return path
        
        for neighbor in residual.get(node, {}):
            if neighbor not in visited and residual[node][neighbor] > 0:
                visited.add(neighbor)
                queue.append((neighbor, path + [neighbor]))
    
    return None

# Time: O(V × E²) with BFS (Edmonds-Karp)
# Space: O(V + E)
```

---

## 4️⃣ VISUALIZATION

**Max Flow Example:**

```
Graph:
    S --(10)→ A --(10)→ T
    |          ↑
   (10)      (1)
    ↓         |
    B --(10)→ C --(10)→ T

Capacities marked in parentheses

Iteration 1: Find S→A→T
  Bottleneck: min(10, 10) = 10
  Flow: 10
  Update: S-A(0), A-T(0)

Iteration 2: Find S→B→C→T
  Bottleneck: min(10, 10, 10) = 10
  Flow: 10
  Update: S-B(0), B-C(0), C-T(0)

Iteration 3: Find augmenting path?
  S→A: capacity 0 (full)
  S→B: capacity 0 (full)
  No path found!

Maximum Flow: 10 + 10 = 20
```

---

## 5️⃣ CRITICAL ANALYSIS

**Time Complexity:**

```
Basic Ford-Fulkerson (with DFS):
  While loop: at most |max_flow| iterations
  Each iteration: DFS O(V + E)
  Total: O(|max_flow| × (V + E))
  
Problem: |max_flow| can be exponential!
  (If capacities are large)

Edmonds-Karp (with BFS):
  While loop: at most O(VE) iterations
  Each iteration: BFS O(V + E)
  Total: O(VE²)
  
Better: Polynomial time guarantee!
```

**Space Complexity:**
```
Residual graph: O(E)
Path finding: O(V)
Total: O(V + E)
```

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Network Flow Applications:**

1. **Data Center Routing:**
   - Source: data center
   - Sink: destination
   - Capacity: link bandwidth
   - Problem: maximize data throughput

2. **Bipartite Matching:**
   - Students to courses (1-1 matching)
   - Add source to all students, all courses to sink
   - Max flow = maximum matching

3. **Airline Scheduling:**
   - Source: flights available
   - Sink: customers demanding travel
   - Capacity: plane capacity
   - Problem: maximize passengers transported

4. **Circulation with Demands:**
   - Supply/demand optimization
   - Models real logistics

---

## 7️⃣ CONCEPT CROSSOVERS

**Relation to Shortest Paths:**
- Dijkstra: picks min distance
- Max flow: finds augmenting paths
- Both: path finding in graphs

**Relation to Greedy Algorithms (Week 10):**
- Max flow: greedy (take augmenting paths)
- Optimal due to Max-Flow Min-Cut theorem

**Relation to Matching Problems:**
- Bipartite matching special case of max flow
- Flow 1 on each edge = matching

---

## 8️⃣ MATHEMATICAL & THEORETICAL

**Max-Flow Min-Cut Theorem:**

```
Theorem: Maximum flow from S to T
         = Minimum capacity of any cut separating S and T

Proof Sketch:
  1. Any flow is bounded by any cut
     (all flow must cross the cut)
  
  2. When no augmenting path exists:
     - Reachable from S in residual graph
     - Unreachable: cut separating them
     - Cut capacity = remaining flow capacity
     - Therefore: flow = cut capacity
  
  3. If flow < cut, augmenting path would exist
     (by reachability definition)

This justifies Ford-Fulkerson termination!
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**Why Augmenting Paths Work:**

```
Greedy Principle:
  Always find path with available capacity
  Push maximum possible flow through
  
Why Optimal?
  Each augmenting path "moves closer" to max flow
  When no more paths exist, can't improve further
  Max-flow min-cut theorem guarantees optimality
```

---

## 🔟 KNOWLEDGE CHECK

1. **Why do we need residual graph?**
   - Answer: Track remaining capacity and allow flow cancellation

2. **What's bottleneck in augmenting path?**
   - Answer: Minimum capacity edge on the path (limits how much can flow)

3. **Can ford-Fulkerson be inefficient?**
   - Answer: Yes, with DFS and irrational capacities. BFS (Edmonds-Karp) fixes this.

4. **What if capacities are not integers?**
   - Answer: Still works, but may not terminate (irrational number issue)

5. **Relation to min cut?**
   - Answer: Max-flow min-cut theorem: they're equal!

---

## 1️⃣1️⃣ RETENTION HOOK

**"Find Augmenting Path, Push Bottleneck Flow"**
- Augmenting: path with capacity available
- Bottleneck: minimum capacity on path
- Repeat until no path exists

---

## 1️⃣2️⃣ COGNITIVE LAYER INTEGRATION

### 🖥️ COMPUTATIONAL LENS: Why BFS Better Than DFS

```
DFS version (basic Ford-Fulkerson):
  Can pick inefficient paths
  Might choose path using small capacity edge first
  Then augment again using larger capacity
  
  Worst case: exponential iterations
  Example: capacity 1000000, might take 1000000 iterations

BFS version (Edmonds-Karp):
  Always picks shortest augmenting path
  Guarantees progress: edge used less if further from sink
  
  Polynomial iterations: O(VE)
  Much faster in practice
```

### 🧠 PSYCHOLOGICAL LENS: Why Max Flow Unintuitive

**Misconception: "Just greedily push max flow each time"**

Reality: Some paths block others
- If you push all flow via suboptimal path first
- You might not be able to reroute
- BFS ensures smart path selection

### 🔄 DESIGN TRADE-OFF LENS: Simple vs Efficient

```
Simple (DFS Ford-Fulkerson):
  Easy to code (10 lines)
  Inefficient on some inputs

Efficient (BFS Edmonds-Karp):
  Slightly harder (BFS instead of DFS)
  O(VE²) guaranteed

Advanced (Dinic's, Push-Relabel):
  Complex but faster in practice
  Used in real systems
```

### 🤖 AI/ML ANALOGY LENS: Distribution Networks

```
Neural network information flow:
  Source: input
  Sink: output
  Capacity: neuron activation capacity
  
Max flow analogy:
  How much information can propagate?
  Bottlenecks in network architecture
  Capacity constraints in inference
```

### 📚 HISTORICAL CONTEXT LENS: Algorithm Evolution

```
1956: Ford-Fulkerson
      Simple, elegant
      Possible infinite loops with irrationals
      
1972: Edmonds-Karp
      BFS ensures polynomial time
      O(VE²)
      
1973: Dinic's Algorithm
      O(V²E)
      Better in practice
      
1986: Push-Relabel
      O(V²√E) or better
      Used in real systems
      
Now: Edmonds-Karp taught in courses
     Dinic's in competitive programming
     Push-relabel in production systems
```

---

**End of Day 4: Network Flow I - Max Flow Basics**  
**Next:** Day 5 - Network Flow II (Advanced Topics)

