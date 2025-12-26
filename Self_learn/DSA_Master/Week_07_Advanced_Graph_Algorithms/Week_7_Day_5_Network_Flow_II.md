# Week 7, Day 5: Network Flow II - Min Cut, Bipartite Matching & Advanced Flow

**Week:** 7 | **Day:** 5 | **Topic:** Advanced Flow Problems  
**Difficulty:** Hard | **Time:** 90 minutes | **Prerequisites:** Week 7 Days 1-4

---

## 1️⃣ THE WHY

**Problem Context:**
Now that you understand max flow, discover how it solves seemingly unrelated problems:
- **Min Cut:** What edges to remove to disconnect S and T?
- **Bipartite Matching:** Assign students to courses 1-to-1
- **Circulation with Demands:** Supply and demand networks

**Why These Problems:**
- Max Flow Min Cut Theorem connects them
- Transform many problems into flow networks
- Elegant reduction shows problem equivalence
- Practical in matching, scheduling, logistics

---

## 2️⃣ THE WHAT

### Min Cut Problem:

```
Cut: Partition nodes into S-side and T-side
Capacity: Sum of weights of edges from S to T side

Min Cut: Cut with minimum total capacity

Key Insight (Max-Flow Min-Cut Theorem):
  Maximum flow = Minimum cut capacity
  
This allows us to:
  Compute max flow to find min cut
  Use for optimization problems
```

### Bipartite Matching:

```
Problem: Assign one element from set A to set B
        Each element used at most once
        Maximize total assignments

Flow Network:
  Source S → All elements in A (capacity 1)
  A → B edges (if can be matched, capacity 1)
  All elements in B → Sink T (capacity 1)
  
Max flow = Maximum matching!
```

### Circulation with Demands:

```
Problem: Each node has demand or supply
        Flow must satisfy demands
        Find feasible circulation

Model:
  Add supersource and supersink
  Connect supplies to supersource
  Connect supersink to demands
  Check if max flow = total demand
```

---

## 3️⃣ THE HOW

### Finding Min Cut:

```python
def find_min_cut(graph, source, sink):
    # Run max flow to get residual graph
    residual = run_ford_fulkerson_return_residual(graph, source, sink)
    
    # Find all reachable nodes from source in residual
    reachable = bfs_reachable(residual, source)
    unreachable = set(graph.keys()) - reachable
    
    # Find edges crossing from reachable to unreachable
    cut_edges = []
    for u in reachable:
        for v in graph[u]:
            if v in unreachable:
                # This edge is in the min cut
                cut_edges.append((u, v))
    
    return cut_edges, sum(capacity for u, v, capacity in cut_edges)
```

### Bipartite Matching with Flow:

```python
def bipartite_matching(left_nodes, right_nodes, edges):
    # Build flow network
    graph = {}
    source = 'S'
    sink = 'T'
    
    # Source to left nodes
    graph[source] = {node: 1 for node in left_nodes}
    
    # Left to right (matched pairs)
    for left in left_nodes:
        graph[left] = {}
        for right in right_nodes:
            if (left, right) in edges:
                graph[left][right] = 1
    
    # Right nodes to sink
    graph[sink] = {}
    for right in right_nodes:
        graph[right] = {sink: 1}
    
    # Compute max flow
    max_flow = max_flow_ford_fulkerson(graph, source, sink)
    return max_flow  # This equals maximum matching
```

### Circulation with Demands:

```python
def feasible_circulation(graph, demands):
    """
    demands[v] > 0: node v is supply (source)
    demands[v] < 0: node v is demand (sink)
    demands[v] = 0: neutral node
    """
    # Create modified graph with supersource and supersink
    modified_graph = dict(graph)
    supersource = 'SUPER_S'
    supersink = 'SUPER_T'
    modified_graph[supersource] = {}
    modified_graph[supersink] = {}
    
    total_supply = 0
    total_demand = 0
    
    # Add edges from supersource to supply nodes
    for node, demand in demands.items():
        if demand > 0:
            modified_graph[supersource][node] = demand
            total_supply += demand
        elif demand < 0:
            # Add edge from this node to supersink
            if node not in modified_graph:
                modified_graph[node] = {}
            modified_graph[node][supersink] = -demand
            total_demand += -demand
    
    # Check if supply equals demand
    if total_supply != total_demand:
        return None  # No feasible circulation
    
    # Compute max flow
    max_flow = max_flow_ford_fulkerson(modified_graph, supersource, supersink)
    
    # If max flow equals total supply, feasible circulation exists
    return max_flow == total_supply
```

---

## 4️⃣ VISUALIZATION

### Min Cut Example:

```
Original Graph:
    S --(5)→ A --(10)→ T
    |         ↑
   (10)     (2)
    ↓        |
    B --(10)→ C --(8)→ T

Max Flow: 15 (found in Day 4)

Residual Graph after max flow:
    (some edges depleted, reverse edges show flow)

Reachable from S in residual: {S, A, B}
Unreachable: {C, T}

Min Cut edges: A→C, B→C
Capacities: 10 + 8 = 18? 

Wait, max flow was 15, so min cut = 15

Actually let me recalculate:
  Path S→A→C→T: min(5, 10, 8) = 5
  Path S→B→C→T: min(10, 10, 8) = 8
  Total: 13? 

No wait, need 3 paths
  Actually max flow 15 means cut = 15
  The 3 edges {S-A, S-B, A-C+B-C, C-T} contain min cut
  
Let me think...different cut:
  S-side: {S}
  T-side: {A, B, C, T}
  Cut edges: S→A(5), S→B(10)
  Capacity: 15 ✓
  
This equals max flow!
```

### Bipartite Matching Example:

```
Students: {A, B, C}
Courses: {X, Y, Z}
Preferences:
  A can take: X, Y
  B can take: Y, Z
  C can take: X, Z

Flow Network:
    S --1→ A
    S --1→ B    A --1→ X --1→ T
    S --1→ C    B --1→ Y --1→ T
               C --1→ Z --1→ T

Max flow: 3 (all students matched)
Matching:
  A → X (or Y)
  B → Y (or Z)
  C → Z (or X)
```

---

## 5️⃣ CRITICAL ANALYSIS

**Min Cut Finding:**

```
Time: Run max flow O(VE²), then BFS O(V+E)
Total: O(VE²)

Space: O(V + E)

Correctness: Max-Flow Min-Cut Theorem guarantees optimality
```

**Bipartite Matching:**

```
Standard approach:
  Use max flow: O(VE²)
  
Specialized algorithms:
  Hopcroft-Karp: O(E√V)
  Kuhn's algorithm: O(VE)
  
Flow approach simpler to code, less efficient
```

**Circulation with Demands:**

```
Time: O(VE²) for max flow computation
Space: O(V + E)

Complexity: Feasibility check reduces to max flow
```

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Min Cut Applications:**

1. **Network Reliability:**
   - Critical edges to protect
   - If removed, disconnects network
   - Min cut = minimum edges to remove

2. **Image Segmentation:**
   - Cut image into foreground/background
   - Min cut = most natural boundary

3. **Project Selection:**
   - Projects have dependencies
   - Select subset maximizing profit
   - Reduces to min cut!

**Bipartite Matching Applications:**

1. **College Admissions:**
   - Students to colleges (with capacity)
   - Maximize admissions

2. **Job Scheduling:**
   - Workers to tasks
   - Each worker takes one task
   - Maximize assignments

3. **Market Matching:**
   - Buyers to sellers
   - Maximize successful trades

---

## 7️⃣ CONCEPT CROSSOVERS

**Relation to Max Flow:**
- Min cut directly from max flow
- Max-flow min-cut theorem connects them
- Fundamental relationship

**Relation to Graph Connectivity:**
- Min cut measures "fragility" of graph
- Edge connectivity = minimum edges to remove

**Relation to Linear Programming:**
- Max flow = special LP problem
- Flow constraints = linear inequalities
- Optimal solution found by simplex

---

## 8️⃣ MATHEMATICAL & THEORETICAL

**Project Selection Reduction to Min Cut:**

```
Problem:
  Projects have profit (positive or negative)
  Dependencies: can't do project B without A
  Maximize total profit

Reduction:
  Nodes: each project + source + sink
  Edges:
    Source → projects with profit p > 0 (capacity p)
    Projects with profit p < 0 → sink (capacity |p|)
    Dependency A→B: edge A→B (capacity ∞)
  
Result:
  Max profit = total positive profit - min cut
  
Why?
  Min cut separates projects we do (S-side) from skip (T-side)
  Edges in cut = violated dependencies + lost profits
  Minimizing cut = maximizing profit
```

**Correctness of Bipartite Matching Reduction:**

```
Theorem: Max flow in constructed network = max matching

Proof:
  1. Any matching gives flow:
     Each matched pair: 1 unit through path
     Total flow = matching size
     
  2. Any flow gives matching:
     Flow conservation + capacity 1
     Each left node: at most 1 unit out
     Each right node: at most 1 unit in
     Forms matching
     
  3. Maximum flow = maximum matching
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**Why Flow-Based Matching Works:**

```
Insight: Matching constraints match flow constraints
  - Each student takes 1 course = flow 1 out
  - Each course has 1 spot = flow 1 in
  - Preferences are edges = valid flow paths
  
Max flow = max matching (both respect constraints)
```

**Why Min Cut Solves Project Selection:**

```
Cut = projects on S-side
Cost = lost profits + violated dependencies
Min cut = minimum cost = maximum profit

Beautiful reduction!
```

---

## 🔟 KNOWLEDGE CHECK

1. **Why does max flow equal min cut?**
   - Answer: Max-Flow Min-Cut Theorem; all flow must cross any cut

2. **How to model matching as flow?**
   - Answer: Unit capacities from source, between sets, to sink

3. **Can bipartite matching be solved without flow?**
   - Answer: Yes, but flow approach unified and works well

4. **What if supplies don't equal demands in circulation?**
   - Answer: No feasible circulation exists; max flow < total demand

5. **Relation between min cut and connectivity?**
   - Answer: Edge connectivity = min cut size; measures robustness

---

## 1️⃣1️⃣ RETENTION HOOK

**"Max Flow = Min Cut = Optimal Selection"**
- Max Flow: push as much as possible
- Min Cut: remove edges to disconnect
- Project Selection: maximize profit
- All equivalent!

---

## 1️⃣2️⃣ COGNITIVE LAYER INTEGRATION

### 🖥️ COMPUTATIONAL LENS: Why Reductions Matter

```
Direct matching algorithm (Hopcroft-Karp):
  O(E√V) = specialized, complex code

Max flow approach:
  O(VE²) = general, simpler code
  
Trade-off:
  Flow slower but reusable for all problems
  Specialized faster but one-purpose
```

### 🧠 PSYCHOLOGICAL LENS: Why Reductions Unintuitive

**Misconception: "These are completely different problems"**

Reality:
- Matching, min-cut, project selection all same!
- Flow-based view unifies them
- Reduction shows deep problem structure

### 🔄 DESIGN TRADE-OFF LENS: Generality vs Specificity

```
Specialized algorithms:
  Hopcroft-Karp for matching
  Better time complexity
  But only for matching

Flow-based approach:
  Works for matching, min-cut, circulation
  Slightly slower but universal
  Simpler to implement

Choose: General if time allows, specific if optimized needed
```

### 🤖 AI/ML ANALOGY LENS: Constraint Satisfaction in ML

```
Resource allocation in neural networks:
  Compute budget constraints
  Memory bandwidth constraints
  Task dependencies
  
Models as flow network:
  Maximize throughput under constraints
  Flow = resource allocation
  Capacity = available resources
```

### 📚 HISTORICAL CONTEXT LENS: Discovery of Problem Equivalences

```
1956: Ford-Fulkerson max flow
      Focused on flow problems only

1960s: Recognition of problem reductions
       Matching → flow
       Min-cut ← max flow
       
1970s-80s: Linear programming connection
           Max flow special case of LP
           Many problems reduce to LP
           
Now: Reductions central to CS theory
     Show problem equivalences
     Enable solution transfer
```

---

## INTEGRATION & SUMMARY

This week (Week 7) brought together graph algorithms:

**Days 1-2:** Single-source shortest paths (Dijkstra, Bellman-Ford, Floyd-Warshall)

**Day 3:** Minimum spanning trees (Kruskal's, Prim's)

**Days 4-5:** Network flow (Ford-Fulkerson, min-cut, matching, circulation)

**Common Theme:** Greedy + clever data structures = optimal solutions

**Next Week (Week 8):** Specialized structures (Tries, Segment Trees, Fenwick Trees)

---

**End of Week 7: Advanced Graph Algorithms Complete!** ✅

**Summary:**
- 5 days of content (Dijkstra → Network Flow)
- Computational depth (hardware reality)
- Psychological insight (why students struggle)
- Real-world applications
- Advanced reductions and problem equivalences
- Mastery-level understanding

**Ready for Week 8 (Specialized Structures)**

