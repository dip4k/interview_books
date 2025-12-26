# Week 7: Problem Solving Roadmap

**Week:** 7 | **Topic:** Problem-solving approach for each algorithm  
**Use:** Strategy guide for tackling interview problems

---

## PROBLEM-SOLVING FRAMEWORK

### Step 1: Recognize the Problem Type
```
Read problem statement:
  ✓ Identify what you're optimizing (shortest, maximum, minimum)
  ✓ Identify constraints (capacities, weights, directionality)
  ✓ Identify graph structure (weighted, directed, bipartite, etc.)
  
Map to problem type:
  Find shortest path? → Dijkstra (non-neg) or Bellman-Ford (neg)
  Connect all with min cost? → MST (Kruskal or Prim)
  Maximize flow? → Max-flow (Ford-Fulkerson / Edmonds-Karp)
  Match two sets? → Bipartite matching (via flow)
  Find bottleneck? → Min-cut (max-flow min-cut)
```

### Step 2: Verify Algorithm Applicability
```
Checklist:
  ✓ Do I have a graph structure? (nodes, edges)
  ✓ What are edge properties? (weights, capacities)
  ✓ What's the optimization goal? (minimize, maximize, find)
  ✓ Any special constraints? (negative weights, unit capacities, etc.)
  
Examples:
  "Find shortest path" + "weights ≥ 0" → Dijkstra ✓
  "Find shortest path" + "weights < 0" → Dijkstra ✗, Bellman-Ford ✓
  "Connect all cities min cost" → MST ✓
  "Route goods, maximize flow" → Max-flow ✓
```

### Step 3: Choose Algorithm Variant
```
Dijkstra:
  Standard: priority queue with min-heap
  Graph: adjacency list
  
Bellman-Ford:
  Standard: edge relaxation approach
  Negative cycle detection: check after V-1 iterations
  
Floyd-Warshall:
  Standard: three nested loops (k, i, j)
  Matrix storage
  
Kruskal:
  Requires sorting (O(E log E))
  Requires Union-Find (O(E × α(V)))
  
Prim:
  Requires priority queue
  Requires adjacency list
  
Ford-Fulkerson/Edmonds-Karp:
  Standard: maintain residual graph
  Method: BFS for pathfinding (Edmonds-Karp)
```

---

## DIJKSTRA'S PROBLEM ROADMAP

### Recognition
```
Problem asks for: shortest path, minimum cost path, minimum time
Graph properties: weighted, non-negative weights, directed or undirected
Special: single source to one or many destinations

Examples:
  - Network delay time: find max delay from source to any node
  - Cheapest flight with K stops: shortest path with constraint
  - Minimum cost to reach destination: classic shortest path
```

### Implementation Checklist
```
1. [ ] Build adjacency list from graph
2. [ ] Create distance array (initialize to infinity except source)
3. [ ] Create priority queue (min-heap by distance)
4. [ ] Create parent/path-tracking array (optional, for reconstruction)
5. [ ] While queue not empty:
      [ ] Extract node with minimum distance
      [ ] If already visited, skip
      [ ] Mark as visited
      [ ] For each neighbor:
        [ ] Calculate new distance via current node
        [ ] If shorter, update and push to queue
6. [ ] Return distance array (or specific distance)
```

### Verification
```
Test case:
  Graph: A-1-B-2-C, A-5-C
  Expected: shortest A→C = 3 (via B)
  
Verify:
  [ ] Distance to C is 3, not 5
  [ ] Parent pointers form correct path A→B→C
  [ ] No negative distances (shouldn't happen with non-negative)
```

### Optimization
```
If TLE:
  [ ] Check heap operations (should be O(log V))
  [ ] Verify adjacency list (not dense)
  [ ] Profile: where is time spent?
  
If WA:
  [ ] Check negative weights
  [ ] Check graph initialization
  [ ] Verify algorithm follows standard implementation
```

---

## BELLMAN-FORD & FLOYD-WARSHALL ROADMAP

### Bellman-Ford Recognition
```
Problem asks for: shortest path with negative weights
Or: detect negative cycle
Or: single-source shortest paths (when Dijkstra fails)

Key: negative weights allowed, but need to detect cycles
```

### Floyd-Warshall Recognition
```
Problem asks for: all-pairs shortest paths
Or: transitive closure (reachability)
Or: shortest path in small graph (V ≤ 500)

Key: need paths between ALL pairs, not just one source
```

### Implementation Checklist (Bellman-Ford)
```
1. [ ] Initialize distance array
2. [ ] For i = 0 to V-2:
      [ ] For each edge (u, v, weight):
        [ ] If distance[u] + weight < distance[v]:
          [ ] Update distance[v]
          [ ] Update parent[v] = u (optional)
3. [ ] Check for negative cycle:
      [ ] For each edge (u, v, weight):
        [ ] If distance[u] + weight < distance[v]:
          [ ] Return "negative cycle found"
4. [ ] Return distance array
```

### Implementation Checklist (Floyd-Warshall)
```
1. [ ] Initialize distance matrix (dist[i][j] = edge weight or inf)
2. [ ] For k = 0 to V-1:
      [ ] For i = 0 to V-1:
        [ ] For j = 0 to V-1:
          [ ] dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
3. [ ] Check for negative cycle:
      [ ] For i = 0 to V-1:
        [ ] If dist[i][i] < 0:
          [ ] Return "negative cycle found"
4. [ ] Return distance matrix
```

---

## MINIMUM SPANNING TREE ROADMAP

### Recognition
```
Problem asks for: connect all nodes, minimize total cost
Or: minimum spanning tree
Or: network design with cost minimization

Key: V-1 edges, no cycles, minimum total weight, ALL nodes connected
```

### Kruskal's Checklist
```
1. [ ] Build edge list with weights
2. [ ] Sort edges by weight (ascending)
3. [ ] Initialize Union-Find structure
4. [ ] For each edge in sorted order:
      [ ] Get endpoints u, v
      [ ] If union(u, v) successful (not same component):
        [ ] Add edge to MST
        [ ] If MST has V-1 edges, STOP
5. [ ] Return MST edges
```

### Prim's Checklist
```
1. [ ] Pick starting node (arbitrary)
2. [ ] Initialize priority queue with (0, start_node)
3. [ ] While queue not empty:
      [ ] Extract (weight, node) with min weight
      [ ] If already visited, skip
      [ ] Mark as visited
      [ ] Add to MST
      [ ] For each unvisited neighbor (w, edge_weight):
        [ ] Push (edge_weight, neighbor) to queue
4. [ ] Return MST edges
```

### Verification
```
MST correctness:
  [ ] Exactly V-1 edges
  [ ] All nodes connected
  [ ] No cycles
  [ ] Total weight minimal
  
Test:
  [ ] Total weight equals expected value
  [ ] Can trace path between any two nodes
  [ ] Different MST? Check if weights allow multiple MSTs
```

---

## MAXIMUM FLOW ROADMAP

### Recognition
```
Problem asks for: maximum flow, maximum throughput, capacity constraints
Or: min-cut (bottleneck)
Or: matching (via flow reduction)
Or: circulation problems

Key: capacities on edges, single source/sink, maximize total flow
```

### Ford-Fulkerson/Edmonds-Karp Checklist
```
1. [ ] Build residual graph (forward edges = capacity, backward = 0)
2. [ ] While augmenting path exists from source to sink:
      [ ] Find path (DFS or BFS)
      [ ] If no path, STOP
      [ ] Calculate bottleneck (min residual capacity on path)
      [ ] For each edge on path:
        [ ] Reduce forward residual by bottleneck
        [ ] Increase backward residual by bottleneck
      [ ] Add bottleneck to total flow
3. [ ] Return total flow value
```

### Bipartite Matching via Flow Checklist
```
1. [ ] Create flow network:
      [ ] Node 0: source
      [ ] Nodes 1..n_left: left vertices
      [ ] Nodes (n_left+1)..(n_left+n_right): right vertices
      [ ] Node n_left+n_right+1: sink
2. [ ] Add edges:
      [ ] source → each left (capacity 1)
      [ ] each left → neighbors on right (capacity 1)
      [ ] each right → sink (capacity 1)
3. [ ] Run Edmonds-Karp
4. [ ] Extract matching:
      [ ] For each left node with flow to right node: pair them
5. [ ] Return matching size = max flow value
```

### Verification
```
Flow correctness:
  [ ] All flows ≤ capacities
  [ ] Flow conservation (in = out for non-source/sink)
  [ ] Total flow achievable (matches test expectation)
  
Max-flow min-cut verification:
  [ ] After algorithm, find min-cut
  [ ] Min-cut capacity = max-flow value ✓
```

---

## PROBLEM-SOLVING DECISION TREE

```
                        START: Read Problem
                              |
                    What are you optimizing?
                         /  |  |  \
                        /   |  |   \
                      SHORTEST SPANNING MAXIMUM  MIN-CUT /
                       PATHS    TREE    FLOW    MATCHING
                        |        |        |          |
                    Weighted?  Weighted?  Capacities?Reduction?
                    /    \      /   \      |           |
                 Non-neg Negative    All-pairs Fixed    No
                   |       |         |        |         |
                Dijkstra  Bellman  Floyd    Max-Flow  Graph
                           |      Warshall  |      Properties?
                           |        |       |         |
                        Single     Dense?  BFS:      Bipartite?
                        Source     |    Edmonds     /    \
                                  Yes    Karp     Yes   No
                                   |       |      |     |
                                 F-W    Poly-time Flow  Special
                                        O(VE²)   Reduction  Cases
```

---

## COMMON PITFALLS & RECOVERY

### Pitfall 1: Wrong Algorithm Choice
```
Symptom: Got wrong answer (not TLE/MLE)
Diagnosis: Probably chose wrong algorithm for problem type
Recovery:
  [ ] Re-read problem statement carefully
  [ ] Check if weights can be negative (Bellman-Ford needed)
  [ ] Check if all-pairs needed (Floyd-Warshall or run Dijkstra V times)
  [ ] Check if capacities involved (flow problem)
```

### Pitfall 2: Implementation Bug
```
Symptom: Works on examples, fails on hidden tests
Diagnosis: Implementation detail wrong
Recovery:
  [ ] Check graph building (adjacency list correct?)
  [ ] Check base cases (source distance = 0, others = inf)
  [ ] Check termination (all nodes visited for Dijkstra?)
  [ ] Check updates (correct formula for relaxation/flow?)
```

### Pitfall 3: Performance Issues
```
Symptom: TLE (Time Limit Exceeded)
Diagnosis: Algorithm correct but too slow for input size
Recovery:
  [ ] Check complexity vs constraints (V, E, time limit)
  [ ] Look for constant factor improvements (heap vs list, etc.)
  [ ] Check if problem allows approximation or heuristic
  [ ] Verify input parsing isn't the bottleneck
```

### Pitfall 4: Edge Cases
```
Common missed cases:
  [ ] Disconnected graph (shortest path to unreachable = inf)
  [ ] Self-loops (usually ignored unless negative)
  [ ] Multiple edges (keep minimum weight)
  [ ] Negative cycles (Bellman-Ford detects, Dijkstra fails)
  [ ] Single node (distance = 0, tree trivial)
```

---

## EFFICIENT PROBLEM-SOLVING TEMPLATE

### For Each Problem (5-10 minutes to plan)

```
1. READ & UNDERSTAND (1-2 min)
   - Problem type?
   - Graph structure?
   - Constraints?
   - Examples?

2. CHOOSE ALGORITHM (1-2 min)
   - What are we optimizing?
   - Do I recognize the pattern?
   - Which algorithm fits?
   - Any special considerations?

3. PLAN IMPLEMENTATION (2-3 min)
   - Data structures needed?
   - Algorithm steps?
   - Edge cases to handle?
   - Time/space complexity?

4. CODE (15-20 min)
   - Build graph
   - Initialize algorithm state
   - Main algorithm loop
   - Return answer

5. VERIFY (2-3 min)
   - Test with provided examples
   - Check edge cases
   - Verify output format
```

---

**Week 7 Problem-Solving Roadmap Complete**

Use this to systematically approach Week 7 problems with confidence.

