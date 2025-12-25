# 🎓 WEEKS 1-2: INTERVIEW PREPARATION & MASTERY GUIDE
## Deep Understanding for Technical Interviews

---

## PART 1: WEEK 1 INTERVIEW QUESTIONS

### Section 1.1: Memory and Complexity

#### Q1: "Explain the call stack to someone who's never heard of it"

**What interviewers are looking for:**
- Can you explain complex concepts simply?
- Do you understand the mechanics?
- Can you connect theory to practice?

**Strong Answer:**
"Think of a stack of papers on your desk. When a function calls another function, we push a new piece of paper (frame) on top. That frame contains:
- Local variables for that function
- Where to return to when done
- Parameters passed in

The stack is a fixed-size region of memory (8MB on Linux). Each function call uses ~24 bytes.

When you have deep recursion (50 levels deep), you need 50 frames × 24 bytes = 1,200 bytes. But if each frame has local variables, it grows to maybe 28KB per frame, so 50 × 28KB = 1.4MB, which exceeds our 8MB limit.

This is why you get stack overflow errors - you've physically run out of space in the stack. It's predictable and calculable."

**Why this is strong:**
- Explains the mechanism (push/pop)
- Gives real numbers (8MB, 24 bytes, 50 levels)
- Shows understanding of why overflow happens
- Connects to real problems

---

#### Q2: "Why does Big O notation ignore constants? Give a practical example where this matters"

**Weak Answer:**
"Big O ignores constants because we only care about asymptotic behavior as n grows to infinity."

**Strong Answer:**
"Big O ignores constants because we're analyzing how algorithms scale. When n is very large, constants become insignificant.

However, constants matter in practice! Consider:
- Algorithm A: 0.1n² (good constant)
- Algorithm B: 100n (worse constant)

At n=100:
- A: 0.1 × 10,000 = 1,000 operations
- B: 100 × 100 = 10,000 operations
- B is 10x faster despite being O(n)!

In the real world, I once optimized a trading system with O(n²) algorithm that ran in 50ms. The constant was small because the inner loop was just arithmetic. When someone suggested switching to O(n log n), it was slower! Why? The O(n log n) algorithm had larger constant due to data structure overhead.

So Big O tells you how algorithms scale, but constants tell you what's actually fast at your data size."

---

#### Q3: "Explain amortized analysis. When does it help?"

**Strong Answer:**
"Amortized analysis spreads the cost of expensive operations over many cheap operations.

Classic example: Dynamic arrays with 2x doubling.

Individual operation:
- Append when space available: O(1)
- Append when full: O(n) because we copy all elements

Naive analysis: Some appends are O(n), so append is O(n)!

Amortized analysis:
- Over n appends, we resize log₂(n) times
- Total copies: 1 + 2 + 4 + 8 + ... + (n/2) = 2n = O(n)
- So per-operation average: O(n) / n = O(1)

This is why Python lists are so efficient despite occasional expensive operations. The expensive operations are rare enough that their cost is spread across many cheap operations.

Amortized analysis helps when:
1. Expensive operations happen rarely
2. You have many cheap operations between them
3. You care about average performance, not worst-case of one operation"

---

### Section 1.2: Recursion Deep-Dive

#### Q4: "You have a recursive function that processes a linked list. At what point will it hit stack overflow? How do you calculate it?"

**Scenario:**
```python
def process_list(node):
    if node is None:
        return 0
    return node.value + process_list(node.next)
```

**Strong Answer:**
"This function will overflow when recursion depth exceeds what the stack can hold.

Stack size on Linux: 8MB
Frame size (estimated):
- Base frame overhead: 24 bytes
- Local variables: node pointer (8 bytes)
- Total: ~32 bytes per frame

Max depth: 8MB / 32 bytes = 262,144 frames

So a linked list with 300,000 nodes will overflow because 300,000 > 262,144.

More precisely, I'd measure the actual frame size:
1. Calculate local variable sizes
2. Measure with a small recursion (how deep before overflow)
3. Extrapolate

In practice, I'd test with:
```python
import sys
print(sys.getrecursionlimit())  # Python's limit: usually 1000

# For raw stack:
# depth = available_stack / frame_size
```

And for this specific case, I'd convert to iteration:
```python
def process_list_iter(node):
    total = 0
    current = node
    while current:
        total += current.value
        current = current.next
    return total
```

Now stack depth = 1 (constant), can handle any list size."

---

#### Q5: "When should you use recursion vs iteration?"

**Strong Answer:**
"Use recursion when:
1. **Natural recursive structure:** Trees (height ~log n), graphs
2. **Code clarity:** Recursive solution is much clearer
3. **Depth is safe:** Max recursion depth < 10,000

Avoid recursion when:
1. **Linear data:** Linked lists, arrays (depth = n)
2. **Unknown size:** Can't predict depth
3. **Real-time:** Function call overhead matters

Example: Tree traversal
- Depth: log n (for balanced tree)
- Recursive code: 5 lines, crystal clear
- Iterative code: 20 lines, with explicit stack
- **Use recursion** (depth is safe, code is clearer)

Counter-example: Processing 1M records
- Depth: 1M (if recursive)
- Max safe: ~350K
- **Use iteration** (depth would exceed limit)

The key question: Is the recursion depth bounded and small? If yes, use recursion. If no, use iteration."

---

## PART 2: WEEK 2 INTERVIEW QUESTIONS

### Section 2.1: Arrays and Memory

#### Q6: "Why is sequential access 10-25x faster than random access? Explain caching"

**Strong Answer:**
"Modern CPUs have caches at different levels:
- L1: 32KB, ~4 nanoseconds
- L2: 256KB, ~10 nanoseconds
- L3: 8MB, ~40 nanoseconds
- Main RAM: ~100 nanoseconds

The CPU doesn't fetch one element; it fetches 64-byte cache lines.

Sequential access:
```
Access arr[0] → Fetch cache line containing arr[0..7]
Access arr[1] → Already in L1 cache! (HIT)
Access arr[2] → Already in cache (HIT)
...
Access arr[8] → New cache line (MISS)
```
Hit rate: 87.5% (7 hits per 8 accesses)
Time: 0.875 × 4ns + 0.125 × 100ns = 16.5ns per access

Random access:
```
Access arr[0] → Fetch cache line for 0x1000
Access arr[10000] → Random address 0x2710, different cache line (MISS)
Access arr[20000] → Another cache line (MISS)
```
Hit rate: ~5% (most misses)
Time: 0.05 × 4ns + 0.95 × 100ns = 95.2ns per access

Ratio: 95.2 / 16.5 ≈ 5.8x slower for random!

Real example: Image processing
- Row-major: Sequential pixels, cache-friendly, fast
- Column-major: Jump 40KB each time, cache-unfriendly, slow

This is why data structure layout matters!"

---

#### Q7: "Design an LRU cache that supports get/put in O(1)"

**Strong Answer:**
"An LRU (Least Recently Used) cache needs:
1. Fast lookup: HashMap
2. Track usage order: Doubly-linked list
3. Evict least-used: Remove from end of list

Design:
```
┌──────────────────────────────────────┐
│ HashMap (O(1) lookup)                │
│ key → pointer to Node                │
└──────────────────────────────────────┘
           ↓
┌──────────────────────────────────────┐
│ Doubly-Linked List (track order)     │
│ Head → [1] ↔ [2] ↔ [3] ↔ Tail        │
│      (most recent)  (least recent)    │
└──────────────────────────────────────┘
```

Operations:
```
get(key):
  1. Lookup in HashMap: O(1)
  2. Move to front: Remove from list (O(1)), add to head (O(1))
  3. Return value

put(key, value):
  1. If exists: get, update value, move to front (O(1))
  2. If not exists:
     - Add to HashMap: O(1)
     - Add to front of list: O(1)
     - If capacity exceeded: Remove from tail (O(1))

All operations: O(1)!
```

Why this works:
- HashMap gives O(1) lookup
- Linked list gives O(1) insertion/deletion
- Combined: Best of both!

Why array doesn't work:
- get(): O(1) lookup
- Move to front: O(n) because we shift all elements
- Total: O(n) per operation (terrible!)

Why not just linked list without HashMap:
- get(): O(n) because we search through list (terrible!)

The combination of HashMap + Linked List is key to O(1) everything."

---

### Section 2.2: Searching and Logarithmic Magic

#### Q8: "Binary search on 1 billion elements: 30 comparisons. Explain why this is so powerful"

**Strong Answer:**
"Binary search divides the search space in half each iteration.

Starting with 1B elements:
```
Iteration 1: 1B → 500M (divide by 2)
Iteration 2: 500M → 250M
Iteration 3: 250M → 125M
...
Iteration 30: ~1 element (found!)
```

Total iterations: log₂(1B) = 30

Why this matters:
- Linear search: 1B comparisons = 1 second
- Binary search: 30 comparisons = 0.00003 seconds
- Speedup: 33 billion times faster!

Real-world impact:
- Database query with 1 billion records
- Without index (linear): 1 second latency (user sees "loading...")
- With index (binary search): 30 microseconds (instant)

This is why:
1. Sorted data is incredibly valuable
2. Database indexes exist
3. B-trees are standard (generalization of binary search)

The key insight: Logarithmic scaling beats linear at scale. At n=1M, log n = 20 but n/2 = 500K. At large scale, log wins overwhelmingly."

---

#### Q9: "Binary search has preconditions: array must be sorted. When is sorting worth the cost?"

**Strong Answer:**
"Preconditions for binary search:
1. Array must be sorted: O(n log n) cost
2. Random access: Needs array, not linked list
3. Must be static (or reindex on changes)

When sorting is worth it:
```
Scenario A: Sort once, search many times
- Sort: O(n log n) = n log n
- Search 1,000 times: 1,000 × O(log n)
- Total: O(n log n + 1,000 log n)

If search happens 1,000 times:
- Linear search: 1,000 × O(n)
- Binary search: O(n log n) + 1,000 × O(log n)

For n = 1M:
- Linear: 1,000 × 1M = 1 billion operations
- Binary: 1M × 20 + 1,000 × 20 = 20M operations
- Speedup: 50x!

Scenario B: Few searches, array changes
- If you search 5 times then modify, re-sort expensive
- Linear search might be better

Decision: Sort if (# searches × n) > (n log n)
Simplifies to: Sort if # searches > log n
For n = 1M: Sort if searches > 20
```

Real world:
- Batch processing (sort once, search many): Sort!
- Streaming data (constantly changing): Maybe not!
- Database: Always sort (create indexes)!"

---

## PART 3: SYSTEM DESIGN QUESTIONS

### Q10: "Design a news feed system that shows 20 posts per page, with millions of users"

**Strong Answer:**
"Architecture decisions:

1. **Data structure for feed:**
   - Need: Recent posts at top, fast pagination
   - Choice: Doubly-linked list or queue
   - Why not array: Can't efficiently remove middle items (O(n))

2. **Finding 'hot' posts:**
   - Track engagement (likes, shares)
   - Use heap (priority queue) for top posts
   - Time: O(log n) to add/update engagement

3. **User feed construction:**
   - Posts from followed users sorted by time
   - Need: Merge multiple sorted lists (from different users)
   - Time: O(k log n) where k = number of followed users

4. **Real-time updates:**
   - New post added → update followers' feeds
   - Use queue for notifications
   - Time: O(1) per follower

5. **Performance at scale:**
   - 1 billion users, each follows ~100 others = 100B relationships
   - Each scroll = fetch 20 posts = O(k log n) = O(100 × log n) ≈ O(700)
   - At 1,000 scrolls/second = 700,000 operations/second (acceptable)

6. **Caching hot data:**
   - Cache trending posts (top 1000 viewed)
   - Cache user's recent feed (most scrolled)
   - Use LRU cache with HashMap + Linked List

Key trade-offs:
- Array: O(1) access, O(n) insertion → Bad for dynamic feed
- Linked list: O(n) access, O(1) insertion → Better for insertions
- Combined with cache: Usually best of both"

---

## PART 4: MASTERY ASSESSMENT

### Self-Evaluation: Can You Explain These?

**Week 1:**
- [ ] Stack overflow formula: capacity / frame_size
- [ ] When recursion depth becomes unsafe (>10,000)
- [ ] Amortized analysis for dynamic arrays
- [ ] How memoization reduces overlapping work
- [ ] Space vs time trade-offs in recursion

**Week 2:**
- [ ] Why cache matters: Sequential is 10-25x faster
- [ ] Array indexing: base + index × element_size
- [ ] Dynamic array growth: geometric (2x) vs linear
- [ ] When to use: Array vs Linked vs Hash vs Queue
- [ ] Binary search speedup: 1B elements = 30 comparisons

**Combined:**
- [ ] Choose data structure for given problem
- [ ] Estimate performance (time/space)
- [ ] Explain trade-offs clearly
- [ ] Handle real-world constraints
- [ ] Solve system design problems

---

## PART 5: COMMON INTERVIEW MISTAKES

### Mistake 1: "I'll just optimize later"
**Problem:** By then, architecture is locked in
**Solution:** Design for performance upfront

### Mistake 2: "This is O(n)"
**Problem:** Forgot about constant factors
**Solution:** "This is O(n) with a large constant due to cache misses" or "This is O(n) with good cache locality"

### Mistake 3: "Recursion is cleaner"
**Problem:** Works for small inputs, crashes at scale
**Solution:** Check recursion depth first

### Mistake 4: "Array is always O(1)"
**Problem:** Forgot about cache misses
**Solution:** "Array has O(1) access if sequential, but O(n) slower for random access due to cache"

### Mistake 5: "Binary search is always faster"
**Problem:** Forgot about sorting cost or preconditions
**Solution:** "Binary search is O(log n) but requires sorted data"

---

## PART 6: PREPARATION CHECKLIST

### Before Your Interview:

**Memorize:**
- [ ] Big O classes and their growth rates
- [ ] Max recursion depth: 8MB / 24 bytes = 349,525
- [ ] Cache speedup: 25x difference between sequential and random
- [ ] Binary search: 1B elements = 30 comparisons
- [ ] Data structure operations (access, insert, delete time)

**Practice:**
- [ ] Explain the call stack to a non-programmer
- [ ] Trace through 5 different recursion examples
- [ ] Draw a memory layout for an array access
- [ ] Explain why LRU cache needs both HashMap and Linked List
- [ ] Design a simple system using Week 1-2 concepts

**Have Examples:**
- [ ] One problem you've solved with recursion
- [ ] One problem where you optimized using Big O
- [ ] One problem where data structure choice mattered
- [ ] One problem involving cache or memory

**Ask Questions:**
- "What's more important for your use case: latency or throughput?"
- "What's your typical data size? Small or large?"
- "Do you have memory constraints?"
- "Is this real-time or batch processing?"

---

## PART 7: FINAL TIPS

1. **Always think about scale:** "This works for 100 items, but what about 1 million?"
2. **Consider trade-offs:** "Arrays are fast for access but slow for insertion"
3. **Remember real constraints:** "Stack is 8MB, RAM is finite, caches matter"
4. **Measure, don't guess:** "I'd verify with profiling, but I estimate..."
5. **Explain your reasoning:** "I chose linked list because we need O(1) insertion"

---

**This prepares you not just to pass interviews, but to think like an engineer at scale.**

Good luck! 🚀
