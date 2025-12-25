# 📘 WEEK 4 DAY 5: CYCLE DETECTION (FLOYD'S ALGORITHM) - Complete Learning Package

**Week 4, Day 5: Problem-Solving Pattern - Cycle Detection in Linked Lists**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT (11 Sections)

### 1️⃣ The Why: Engineering Motivation

**Problem:** Detect if a linked list has a cycle.

Real-world:
- **Memory leak detection:** Find circular references in object graphs
- **Software testing:** Detect infinite loops in state machines
- **Traffic analysis:** Find closed loops in network topology
- **Game development:** Detect circular dependencies in asset loading
- **Data validation:** Ensure no cycles in dependency graphs

**Naive approach:** Mark nodes as visited O(n) space
```python
def has_cycle_naive(head):
    visited = set()
    current = head
    while current:
        if current in visited:
            return True
        visited.add(current)
        current = current.next
    return False
```

**Floyd's algorithm:** Two pointers, no extra space O(1)
```python
def has_cycle_floyd(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next           # Move 1 step
        fast = fast.next.next      # Move 2 steps
        if slow == fast:
            return True
    return False
```

**Performance difference:** Cycle length n: O(n) space vs O(1) space

---

### 2️⃣ The What: Mental Model

**Core Insight:** Two pointers move at different speeds. If cycle exists, fast pointer catches slow pointer.

**Why this works:**
- If no cycle: fast pointer reaches end
- If cycle exists: pointers eventually meet inside cycle
- Fast moves 2x speed of slow
- Meeting guarantees cycle exists

**Visual:**
```
No cycle:
1 → 2 → 3 → 4 → None
slow: 1 → 2 → 3 → 4
fast: 1 → 3 → None

Slow pointer reaches end, fast reaches None.
No meeting → No cycle.

With cycle:
1 → 2 → 3 → 4
        ↓   ↑
        └── 5

slow: 1 → 2 → 3 → 4 → 5 → 3 → 4 → 5 → 3 (meets at 3)
fast: 1 → 3 → 5 → 4 → 3

Fast catches slow → Cycle exists!
```

**Key Property:** In cycle of length c, after c moves of slow pointer, fast pointer meets it.

---

### 3️⃣ The How: Mechanics

**Algorithm Template:**
```python
def has_cycle(head):
    # Handle empty list
    if not head or not head.next:
        return False
    
    # Initialize two pointers
    slow = head
    fast = head
    
    # Move until fast reaches end or they meet
    while fast and fast.next:
        slow = slow.next          # 1 step
        fast = fast.next.next     # 2 steps
        
        # Check if they meet
        if slow == fast:
            return True
    
    # Fast reached end → no cycle
    return False
```

**Step-by-step:**
1. Initialize slow at head, fast at head
2. While fast not at end:
   - Move slow 1 step
   - Move fast 2 steps
   - Check if they're same node
3. If they meet → cycle exists
4. If fast reaches end → no cycle

**Why O(1) space?**
- Only two pointers (constant)
- No hash set/visited tracking
- Pure pointer comparison

**Time complexity:**
- No cycle: O(n) to reach end
- With cycle: O(n) to detect meeting
- Both cases: O(n)

---

### 4️⃣ Visualization: Examples

**Example 1: No Cycle**
```
Linked list: 1 → 2 → 3 → 4 → None

Step 0: slow=1, fast=1
Step 1: slow=2, fast=3
Step 2: slow=3, fast=None (fast.next doesn't exist)

fast reached end → return False (no cycle)
```

**Example 2: Cycle at End**
```
Linked list: 1 → 2 → 3 → 4
                     ↑   ↓
                     └───

Step 0: slow=1, fast=1
Step 1: slow=2, fast=3
Step 2: slow=3, fast=2
Step 3: slow=4, fast=4 (MEET!)

slow == fast → return True (cycle exists)
```

**Example 3: Cycle in Middle**
```
Linked list: 1 → 2 → 3 → 4 → 5
                ↑       ↓
                └───────

Step 0: slow=1, fast=1
Step 1: slow=2, fast=3
Step 2: slow=3, fast=5
Step 3: slow=4, fast=4 (MEET!)

slow == fast → return True (cycle detected!)
```

---

### 5️⃣ Critical Analysis

**Time Complexity:**
- No cycle: O(n) - fast reaches end
- With cycle of length c, starting at distance d:
  - Slow reaches cycle in d steps
  - Then slow enters cycle
  - Fast catches in at most c more steps
  - Total: O(d + c) = O(n)

**Space Complexity:**
- O(1) - only two pointers, no extra structures

**Comparison:**

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Hash Set | O(n) | O(n) | Extra space for visited set |
| Floyd | O(n) | O(1) | No extra space |
| DFS | O(n) | O(n) | Recursion stack |

**When to Use:**
- When space optimization critical
- Linked list cycle detection
- Linked list problems in general

---

### 6️⃣ Real System Integration

**Memory Leak Detection:**
Runtime systems use cycle detection to find circular references preventing garbage collection.

**Software Testing:**
State machines tested for infinite loops using cycle detection algorithms.

**Network Topology:**
Directed graphs analyzed for cycles to ensure DAG (Directed Acyclic Graph) property.

**Dependency Management:**
Package managers check for circular dependencies in code dependencies.

---

### 7️⃣ Concept Crossovers

**Builds On:**
- Week 1: Linked list traversal
- Week 2: Two pointers concept
- Week 3: Node comparison
- Week 4 Days 1-4: Problem-solving patterns

**Enables:**
- Week 5: Finding cycle start node
- Week 5: Cycle length calculation
- Week 6: Advanced linked list problems
- Week 12: Graph cycle detection

**Related Techniques:**
- DFS cycle detection in graphs
- Union-Find for cycle detection
- Topological sort for cycle checking

---

### 8️⃣ Mathematical Perspective

**Mathematical Proof:**

If cycle exists with length c, after k iterations:
- Slow pointer position: k
- Fast pointer position: 2k (mod cycle_length)

When they meet: k ≡ 2k (mod c), which means k ≡ 0 (mod c)

So after at most c iterations, they must meet.

**Why it always works:**

In a cycle of length c:
- Gap between pointers closes by 1 each step (fast gains 1)
- Max initial gap is c-1
- Within c steps, gap becomes 0
- They must meet

---

### 9️⃣ Algorithmic Design Intuition

**When to Use Floyd's Algorithm:**
1. Cycle detection needed
2. Space optimization important
3. Linked list structure
4. O(n) time acceptable

**When to Use Alternatives:**
- Hash set: clearer code, don't care about space
- DFS: directed graphs
- Union-Find: graph cycle detection

**Problem Patterns:**
- Linked list has cycle?
- Find cycle start node
- Calculate cycle length
- Multiple cycles detection

---

### 🔟 Knowledge Check

1. Why are there two pointers moving at different speeds?
2. Trace Floyd's algorithm on linked list with cycle
3. Why does meeting point guarantee cycle?
4. What if we used 1 and 3 speeds instead of 1 and 2?
5. How to find START of cycle?
6. What if list is circular from start?
7. How to find cycle LENGTH?

---

### 1️⃣1️⃣ Retention Hooks

**One-liner:** "Floyd's tortoise and hare: slow moves 1 step, fast moves 2 steps. In cycle, they always meet."

**Mnemonic - "TORTOISE-HARE":**
- **T**wo pointers: slow and fast
- **O**ne step: slow moves 1
- **R**ace: fast moves 2 (faster)
- **T**hey meet: if cycle exists
- **O**bservation: meeting guarantees cycle
- **I**ntelligent: O(1) space solution
- **S**olution: cycle detection
- **E**fficient: only pointers, no extra data

**H**are faster: 2x speed
- **A**lways detects: if cycle exists
- **R**esult: true or false
- **E**xcellent: O(n) time, O(1) space

**Visual Memory:**
```
Think: "Race on circular track"
- Tortoise (slow) moves 1 position
- Hare (fast) moves 2 positions
- On straight track, hare escapes
- On circular track, hare laps tortoise
```

**Story:** "Two runners on a track. Slow runner runs at 1 m/s, fast runner at 2 m/s. If track is infinite (straight), fast runner escapes. If track is circular, fast runner eventually catches slow runner."

---

## PART 2: QUICK SUMMARY

**Floyd's Algorithm Essence:**

Two pointers at different speeds detect cycles in linked lists using O(1) space.

**When to Use:**
- Detect cycle in linked list ✓
- Space optimization critical ✓
- Tortoise and hare metaphor ✓
- O(n) time acceptable ✓

**Template:**
```python
def has_cycle(head):
    if not head or not head.next:
        return False
    
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    
    return False
```

**Real Problems:**
- Linked list cycle detection
- Find cycle start node (extension)
- Cycle length calculation (extension)
- Circular reference detection

---

## PART 3: SOCRATIC QUESTIONS & ANSWERS

**Q1:** Why use two pointers at different speeds instead of just one?

**A:** Single pointer can't detect cycles - it would just traverse forever. Two at different speeds: if cycle exists, faster pointer will eventually lap slower one, creating meeting point.

---

**Q2:** Trace Floyd's algorithm on: 1 → 2 → 3 → 4 → 3 (cycle back to 3)

**A:**
```
Initial: slow=1, fast=1

Step 1: slow=2, fast=3
Step 2: slow=3, fast=2 (fast skips 3→4, 4→3)
Step 3: slow=4, fast=4 (MEET!)

Result: True (cycle detected)
```

---

**Q3:** Why does meeting guarantee a cycle exists?

**A:** If no cycle, fast pointer reaches None eventually. If they meet, they're on same node at same time. This only happens if there's a cycle to contain them.

---

**Q4:** What if we used 1 and 3 speed instead of 1 and 2?

**A:** Still works! Gap closes faster (2 per step vs 1). Still detects cycles. But 1-2 is standard because it's simplest. 1-3 also fine, just redundant.

---

**Q5:** How to find the START of the cycle (not just detect)?

**A:**
```python
def find_cycle_start(head):
    slow = fast = head
    
    # Find meeting point
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return None  # No cycle
    
    # Reset slow to head
    slow = head
    
    # Move both at same speed
    while slow != fast:
        slow = slow.next
        fast = fast.next
    
    return slow  # Start of cycle
```

---

**Q6:** What if list is circular from the start (1 → 1)?

**A:** Works fine! On first iteration:
- slow moves to 1
- fast moves to 1
- They're equal → cycle detected
- Technically a self-loop, but algorithm handles it

---

**Q7:** How to find the LENGTH of the cycle?

**A:**
```python
def find_cycle_length(head):
    slow = fast = head
    
    # Find meeting point
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break
    else:
        return 0  # No cycle
    
    # Count cycle length
    length = 1
    current = slow.next
    while current != slow:
        length += 1
        current = current.next
    
    return length
```

---

## PART 4: README

**90-Minute Study Guide:**
1. The Why (10 min): Understand cycle problem
2. The What (15 min): Mental model of speeds
3. The How (15 min): Two-pointer mechanics
4. Visualization (20 min): Trace examples
5. Quick Summary (5 min): Key insights
6. Questions (15 min): Test understanding

**Key Skill:** Recognize cycle detection opportunities, implement efficiently

**Practice:** Basic detection, find start, find length variations

**Connection:** Final pattern of Week 4. Combines pointer movement with cycle concepts.

---

**Status:** ✅ Day 5 Complete | **Next:** Week 5 begins!

