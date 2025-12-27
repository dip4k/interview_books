# Week 2: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for ANY Week 2 problem:**

1. **Understand** input, output, constraints
2. **Identify** which structure fits (array, list, stack, queue, binary search?)
3. **Analyze** complexity for your choice
4. **Implement** the solution
5. **Verify** it works (trace examples, check edge cases)

---

## 🎯 Problem-Type Roadmap

### Type 1: Array Access Problems
**Pattern:** "Find element at index i, modify element, access multiple elements"

**Decision:** Use array (O(1) access)

**Template:**
```
Array arr = ...
for i in range:
    val = arr[i]        // O(1)
    process(val)
    arr[i] = newVal     // O(1)
```

**Examples:** Two Sum, Best Time to Buy Stock, Product of Array Except Self

### Type 2: Dynamic Size Problems
**Pattern:** "Size unknown, add/remove elements, need O(1) amortized"

**Decision:** Use dynamic array (vector, ArrayList)

**Template:**
```
Vector v = ...
for item in stream:
    v.add(item)  // O(1) amortized
```

**Examples:** Running sum, building result array, implementing stack

### Type 3: Insertion/Deletion at Known Position
**Pattern:** "Insert/delete at specific position given pointer"

**Decision:** Use linked list (O(1) relink)

**Template:**
```
Node current = ...
Node newNode = new Node(value)
newNode.next = current.next
current.next = newNode  // O(1) insertion
```

**Examples:** Undo/redo, memory allocator, LRU cache

### Type 4: LIFO Access
**Pattern:** "Last in, first out" (undo, recursion, parentheses matching)

**Decision:** Use stack

**Template:**
```
Stack s = ...
s.push(item)      // O(1)
item = s.pop()    // O(1)
```

**Examples:** Valid Parentheses, Undo operations, Backtracking

### Type 5: FIFO Access
**Pattern:** "First in, first out" (BFS, queue, scheduling)

**Decision:** Use queue

**Template:**
```
Queue q = ...
q.enqueue(item)   // O(1)
item = q.dequeue()  // O(1)
```

**Examples:** Level-order traversal, Task scheduling, BFS graph

### Type 6: Searching Sorted Array
**Pattern:** "Find element in sorted array, minimize comparisons"

**Decision:** Use binary search

**Template:**
```
int search(arr, target):
    left = 0, right = n-1
    while left <= right:
        mid = (left + right) / 2
        if arr[mid] == target: return mid
        if arr[mid] < target: left = mid + 1
        else: right = mid - 1
    return -1
```

**Examples:** Binary Search, First Bad Version, Search Insert Position

---

## 🌳 Decision Tree: Choosing Data Structure

```
START: "I need to store and access data"

1. Is the data sorted?
   ├─ YES and need search? → Binary Search
   └─ NO → Continue

2. Do I know the size at start?
   ├─ YES (fixed size) → Array
   └─ NO (unknown) → Dynamic Array or Linked List

3. What operations are frequent?
   ├─ Random access (arr[i])? → Array or Dynamic Array
   ├─ Insert/delete at known position? → Linked List
   ├─ Insert at end only? → Dynamic Array (O(1) amortized!)
   └─ Continue

4. Need special access order?
   ├─ LIFO (last in first out)? → Stack
   ├─ FIFO (first in first out)? → Queue
   └─ Random? → Array or List

DEFAULT: Dynamic Array (vector) ~95% of time
```

---

## 🛠 Common Pitfalls & Recovery

### Pitfall 1: "Linked list for dynamic size"
**Recovery:** Use dynamic array! Better cache (50x), O(1) amortized, simpler.

### Pitfall 2: "Amortized O(1) means always O(1)"
**Recovery:** Occasional O(n) pauses happen. Averaged over n operations, it's O(1) each.

### Pitfall 3: "Insertion O(1) in linked list"
**Recovery:** Only if you have pointer! Finding insertion point is O(n). Total often O(n).

### Pitfall 4: "Binary search on unsorted"
**Recovery:** Array MUST be sorted. Unsorted breaks algorithm completely.

### Pitfall 5: "Wrong structure for access pattern"
**Recovery:** Identify pattern (stack vs queue vs array) BEFORE coding.

### Pitfall 6: "Off-by-one in binary search"
**Recovery:** Use (left + right) / 2, not left + (right-left) / 2. Be careful with boundaries.

---

## 📋 Problem-Solving Template

**For ANY Week 2 problem:**

```
PROBLEM: [Name]

UNDERSTAND:
- Input: [What are we given?]
- Output: [What's the goal?]
- Constraints: [Time/space limits?]
- Examples: [Trace 1-2 examples]

IDENTIFY:
- [Which structure fits best?]
- Why? [Reasoning]
- Access pattern? [Random, sequential, LIFO, FIFO?]

ANALYZE:
- Time: [Complexity of my solution]
- Space: [Memory used]
- Worst case? [When does it happen?]

IMPLEMENT:
- [Solution logic in pseudocode]
- [Trace with example]

VERIFY:
- Test: [Edge cases]
- Correct? [Yes/No]
- Can optimize? [Further improvements?]
```

---

## 🔍 Example Walkthroughs

### Example 1: "Find element in unsorted array"
- **UNDERSTAND:** Search in array, return index or -1
- **IDENTIFY:** Array (no sorting requirement)
- **ANALYZE:** Linear search O(n), can't do better without sorting
- **IMPLEMENT:** Loop through all, compare each
- **VERIFY:** Test found, not found, empty cases

### Example 2: "Implement undo functionality"
- **UNDERSTAND:** User actions, undo reverts to previous
- **IDENTIFY:** Stack (LIFO - last action undone first)
- **ANALYZE:** Push on action O(1), pop on undo O(1)
- **IMPLEMENT:** Stack of actions, pop and revert
- **VERIFY:** Test multiple undos, also test redo (need second stack)

### Example 3: "Search in sorted array"
- **UNDERSTAND:** Find element, minimize comparisons
- **IDENTIFY:** Binary search (sorted array, O(log n))
- **ANALYZE:** O(log n) time, O(1) space (iterative)
- **IMPLEMENT:** Left/right pointers, compare to middle
- **VERIFY:** Test found, not found, array edges

---

## 🎯 Quick Decision Matrix

| Goal | Structure | Why |
|------|-----------|-----|
| Random access by index | Array | O(1) indexing |
| Unknown size | Vector | O(1) amortized append |
| Frequent mid-insert | LinkedList | O(1) relink, but rare! |
| LIFO semantics | Stack | Natural for undo |
| FIFO semantics | Queue | Natural for scheduling |
| Find in sorted | BinarySearch | O(log n) |

---

## ✅ Interview Edge Cases Checklist

### Arrays
- [ ] Empty array
- [ ] Single element
- [ ] All same elements
- [ ] Overflow on large indices

### Dynamic Arrays
- [ ] Single append (to empty)
- [ ] Multiple appends (trigger resize)
- [ ] Delete and append

### Linked Lists
- [ ] Empty list
- [ ] Single node
- [ ] Insert/delete at head

### Stacks
- [ ] Pop from empty stack
- [ ] Multiple push/pop sequences

### Queues
- [ ] Enqueue/dequeue empty
- [ ] Circular buffer wraparound

### Binary Search
- [ ] Target not found
- [ ] Target at boundaries
- [ ] Duplicate elements

---

## 🚀 Practice Problem Sets

### Easy (Warm-up)
1. Array: Rotate Array, Reverse Array
2. Stack: Valid Parentheses
3. Queue: Implement Queue using Stack
4. Binary Search: Basic Binary Search

### Medium (Apply concepts)
1. Array: Product of Array Except Self
2. LinkedList: Reverse Linked List
3. Stack: Next Greater Element
4. Queue: Sliding Window Maximum (preview of Week 4)
5. Binary Search: Search Insert Position

### Hard (Extend thinking)
1. Array: Merge Intervals (prep for Week 4)
2. LinkedList: Merge K Sorted Lists
3. Combined: Design LRU Cache (linkedlist + hashmap)

---

## Summary

**Master the decision tree.** Most Week 2 problems just need choosing the right structure. Implementation is straightforward after that.

