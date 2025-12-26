# ❓ WEEK 3: ALL 35 QUESTIONS & DETAILED ANSWERS

**Complete Question Bank - Use After Each Day**

---

## 📌 HOW TO USE THIS FILE

- **After each day:** Attempt that day's 7 questions
- **Saturday review:** Redo all 35 questions
- **Self-test:** Cover answers, try to answer
- **Scoring:** 5 points per question = 175 total
- **Target:** 140+ points (80%) for mastery

---

## ✅ DAY 1: ELEMENTARY SORTS (7 Questions)

### **Q1.** What's the time complexity of insertion sort on nearly sorted data?

**Your Answer:** _______________

**Answer:** O(n) best case

**Explanation:** If array is nearly sorted, inner while loop executes few times. With optimized version checking swaps, can detect sorted in O(n) comparisons.

**Key Insight:** Insertion adapts to data! Almost sorted = almost linear.

---

### **Q2.** Compare bubble sort vs insertion sort - which does more work on reverse sorted data?

**Your Answer:** _______________

**Answer:** Both do O(n²) work, but bubble does more swaps. Bubble: n²/2 swaps. Insertion: n²/2 shifts (slightly faster).

**Explanation:** On [5,4,3,2,1]:
- Bubble: Every comparison results in swap
- Insertion: Every shift moves one element

**Key Insight:** Insertion more efficient in practice.

---

### **Q3.** Why is selection sort not stable, while bubble and insertion are?

**Your Answer:** _______________

**Answer:** Selection sort swaps with position i, breaking relative order of equal elements.

**Example:** [2, 1, 2] with selection
- Find min: 1 (index 1)
- Swap with index 0: [1, 2, 2] ✗ (lost which 2 was first!)

Bubble/insertion preserve order by shifting/moving carefully.

**Key Insight:** Stability matters when sorting objects with multiple fields.

---

### **Q4.** Derive Big-O of bubble sort from code:
```python
for i in range(n):
    for j in range(n-1-i):
        if arr[j] > arr[j+1]:
            swap(arr[j], arr[j+1])
```

**Your Answer:** _______________

**Answer:** O(n²)

**Derivation:**
- Outer loop: n iterations
- Inner loop: (n-1) + (n-2) + ... + 1 = n(n-1)/2 iterations total
- Each iteration: O(1)
- Total: n(n-1)/2 = O(n²)

**Key Insight:** Sum of 1 to n = n(n+1)/2, always O(n²).

---

### **Q5.** When would you prefer insertion sort over quick sort?

**Your Answer:** _______________

**Answer:** When n < 50 and simplicity matters, or data is nearly sorted.

**Explanation:** 
- n < 50: O(n²) is fine, code is simple
- Nearly sorted: O(n) best case beats O(n log n) average
- Real-world: Java uses insertion for small arrays in hybrid sort

**Key Insight:** Simple often beats clever for small inputs.

---

### **Q6.** Can you optimize bubble sort to O(n) best case? How?

**Your Answer:** _______________

**Answer:** Yes! Add flag to detect if already sorted:

```python
def bubble_sort_optimized(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(n-1-i):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True
        if not swapped:  # Already sorted!
            break
```

**Key Insight:** Optimization based on algorithm understanding.

---

### **Q7.** If you have 1 million items, how much slower is bubble (O(n²)) vs insertion (adaptive)?

**Your Answer:** _______________

**Answer:** ~10,000x slower (worst case: 10^12 ops vs 10^8 ops for nearly sorted)

**Calculation:**
- 1M² = 10^12 operations (bubble)
- 1M log(1M) ≈ 20M operations (optimized insertion, avg)
- Ratio: 10^12 / 10^8 = 10,000x

**Key Insight:** Complexity dominates at scale. Constants don't matter.

---

## ✅ DAY 2: ADVANCED SORTS (7 Questions)

### **Q8.** Why is merge sort guaranteed O(n log n) while quick sort can degrade to O(n²)?

**Your Answer:** _______________

**Answer:** Merge sort always divides in half (guaranteed balance). Quick sort depends on pivot (can be poor).

**Explanation:**
- Merge: Always splits 50-50 → balanced tree → log n depth
- Quick: Bad pivot → splits 0-n, 0-(n-1), ... → linear depth

**Key Insight:** Divide-and-conquer guarantees need balanced division.

---

### **Q9.** Draw the recursion tree for merge sort on n=8. How many levels? Total work?

**Your Answer:** _______________

**Answer:**
```
Level 0: [8 items] → 1 array, 8 ops = 8
Level 1: [4,4] → 2 arrays, 4 ops each = 8
Level 2: [2,2,2,2] → 4 arrays, 2 ops = 8
Level 3: [1,1,...] → 8 arrays, 1 op (merge) = 8

Levels: log₂(8) = 3
Total: 8 × 3 = 24 = 8 log 8 = O(n log n)
```

**Key Insight:** Each level does O(n) work regardless of tree shape.

---

### **Q10.** Quick sort with pivot selection: what makes bad choice?

**Your Answer:** _______________

**Answer:** Picking smallest/largest. Example:

Array: [1,2,3,4,5], pivot=1
```
Less: [], Pivot: 1, Greater: [2,3,4,5]
  Less: [], Pivot: 2, Greater: [3,4,5]
    ...
```

Creates chain → O(n²) comparisons.

**Fix:** Randomize pivot or use median-of-three.

**Key Insight:** Pivot quality determines performance.

---

### **Q11.** Merge sort needs O(n) extra space. Why can't we do it in-place?

**Your Answer:** _______________

**Answer:** Merging two sorted arrays requires temporary space to avoid overwriting.

```
Left: [1, 3, 5], Right: [2, 4, 6]
Merging requires output array to build result
Can't merge in-place without complex logic
```

Quick sort avoids this (in-place partition), hence better space.

**Key Insight:** Merge elegance comes with space cost.

---

### **Q12.** Master theorem: T(n) = 4·T(n/2) + n. What's complexity?

**Your Answer:** _______________

**Answer:** O(n²)

**Application:**
- a=4, b=2, f(n)=n
- log_b(a) = log₂(4) = 2
- d=1 (degree of n)
- Since d < log_b(a): **T(n) = Θ(n^log_b(a)) = Θ(n²)**

**Key Insight:** Master theorem determines complexity directly.

---

### **Q13.** Why do most languages default to quick sort instead of merge?

**Your Answer:** _______________

**Answer:** Quick sort advantages:
1. In-place (O(log n) space vs O(n))
2. Cache-friendly (less data movement)
3. Average O(n log n) matches merge
4. Randomization prevents pathological cases

Merge sort better for: Stable sorts, guaranteed O(n log n), external sorting.

**Key Insight:** Trade-offs determine language choice.

---

## ✅ DAY 3: HASHING FUNDAMENTALS (7 Questions)

### **Q14.** Simple hash function for strings into array of size 10. What's the risk?

**Your Answer:** _______________

**Answer:** Collisions! Multiple strings hash to same index.

**Example:** hash(key) = sum(characters) % 10
```
"ab" = 1+2 = 3 % 10 = 3
"ba" = 2+1 = 3 % 10 = 3 (COLLISION!)
```

**Solution:** Better function or collision handling (chaining, open addressing).

**Key Insight:** Simple hash functions have high collision rates.

---

### **Q15.** What's load factor and when should you rehash?

**Your Answer:** _______________

**Answer:** Load factor λ = n / m (items / buckets)

```
λ = 0.5: ~50% buckets filled, few collisions
λ = 1.0: Full, many collisions
λ = 2.0: Twice full, terrible collisions

Rehash when λ > threshold (typically 0.75-2.0)
```

**Why:** More collisions → longer chains → slower lookups

**Key Insight:** Rehashing maintains O(1) average.

---

### **Q16.** Explain chaining collision resolution with example.

**Your Answer:** _______________

**Answer:** Store list at each hash index.

```
Hash table size 3:
hash("alice") = 0
hash("bob") = 1
hash("charlie") = 0 (collision!)

Index 0: [("alice", 25), ("charlie", 22)]
Index 1: [("bob", 30)]
Index 2: []

Lookup "charlie":
1. hash("charlie") = 0
2. Check index 0 list
3. Scan: find ("charlie", 22)
4. Return 22
```

**Complexity:** O(1 + chain_length)

**Key Insight:** Collisions accepted, handled with list.

---

### **Q17.** Why use prime-sized array for hash table?

**Your Answer:** _______________

**Answer:** Prime size with modulo hash minimizes collisions.

**Theory:** Hash function h(k) = k % p (p prime)
- Prime size ensures good distribution
- Non-prime: patterns create clustering

**Example:**
```
Size 10: hash(0)=0, hash(10)=0, hash(20)=0 (bad!)
Size 11: hash(0)=0, hash(10)=10, hash(20)=9 (better!)
```

**Key Insight:** Math behind hash tables matters.

---

### **Q18.** Hash table insert, lookup, delete worst case?

**Your Answer:** _______________

**Answer:** O(n) worst case (all keys collide)

**Explanation:**
- Best: O(1) - no collision
- Average: O(1 + λ) where λ is load factor
- Worst: O(n) - all hash to same bucket (linear scan)

**Prevention:** Good hash function + rehashing

**Key Insight:** Worst case possible but unlikely with good design.

---

### **Q19.** Open addressing vs chaining: which handles deletion better?

**Your Answer:** _______________

**Answer:** Chaining.

**Why:** 
- Chaining: Remove from list (simple)
- Open addressing: Can't just delete (breaks probing chain)
  - Solution: Mark as "deleted" or rebuild table
  - Expensive!

**Example:** Open addressing deletion
```
Array: [1, 2, 3, 4, 5]
Delete 3: [1, 2, DEL, 4, 5]  // Still need to probe through DEL
```

**Key Insight:** Design choice affects operations.

---

## ✅ DAY 4: HASH APPLICATIONS (7 Questions)

### **Q20.** Counting unique items in [1,2,2,3,3,3]: use what?

**Your Answer:** _______________

**Answer:** Hash set. Time: O(n), Space: O(unique)

```python
seen = set()
for item in arr:
    seen.add(item)
return len(seen)  # 3
```

vs. Sorting: O(n log n) + O(n) scan

**Key Insight:** Hashing better for uniqueness.

---

### **Q21.** Fibonacci(50) without caching: time? With caching?

**Your Answer:** _______________

**Answer:**
- Without cache: O(φ^50) ≈ 10^10 calls (impossible)
- With cache: O(50) calls (one per unique n)

**Cache mechanism:**
```python
cache = {}
def fib(n):
    if n in cache:
        return cache[n]  # O(1)
    # compute once
    cache[n] = result
```

**Key Insight:** Hashing enables dramatic speedups.

---

### **Q22.** Explain Bloom filter false positives.

**Your Answer:** _______________

**Answer:** Bloom filter may say "yes" when actually "no".

**Why:** Multiple items can hash to same bit.

```
Add "alice" → set bit 5
Add "bob" → set bit 5 (coincidence!)
Query "charlie":
  hash("charlie") = 5 → bit set → "might be present"
  But "charlie" never added! (false positive)
```

**No false negatives:** If bit not set, definitely not present.

**Use case:** Space critical, false positives acceptable.

**Key Insight:** Trade-off: space for false positives.

---

### **Q23.** Deduplication vs counting with hash.

**Your Answer:** _______________

**Answer:**

**Dedup (set):**
```python
unique = set(arr)
```
O(n) time, tells you unique items

**Counting (map):**
```python
count = {}
for item in arr:
    count[item] = count.get(item, 0) + 1
```
O(n) time, tells you counts

**Difference:** Dedup = presence, counting = frequency

**Key Insight:** Choose right structure for goal.

---

### **Q24.** Why is caching O(1) lookup despite recursive calls?

**Your Answer:** _______________

**Answer:** Cache lookup is O(1) (hash), computation happens once per unique subproblem.

**Example:** fib(5)
```
fib(5) → compute → cache[5] = result
fib(5) → lookup → O(1) return cached value!
```

**Amortized:** Total time = compute_cost × unique_subproblems + lookups

**Key Insight:** Caching buys massive speedup with O(1) lookups.

---

### **Q25.** When is Bloom filter better than hash set?

**Your Answer:** _______________

**Answer:** When memory is extremely limited.

**Bloom filter:** Constant small space, false positives, no deletions
**Hash set:** Linear space, exact answers, deletions supported

**Example:**
- Bloom: Check if email in blacklist (millions emails, limited RAM)
- Hash set: Cache recently accessed pages (fewer items, exact needed)

**Key Insight:** Understand constraints to choose.

---

## ✅ DAY 5: INTEGRATION & SELECTION (7 Questions)

### **Q26.** Decision matrix: Need sorted output?

**Your Answer:** _______________

**Answer:**
- YES → Use sorting (merge/quick)
  - Cost: O(n log n) to sort, O(log n) to lookup each after
- NO → Use hash if need fast lookup
  - Cost: O(1) lookup

**Example:** Sorted output needed?
- Ranking (top 10): Sort O(n log n)
- Check membership: Hash O(1)

**Key Insight:** First question determines structure.

---

### **Q27.** Hash table fails on range queries. Why?

**Your Answer:** _______________

**Answer:** Hashing distributes items randomly. Can't efficiently iterate "between A and B".

**Example:** Find all ages between 20-30
- Hash: Must scan all buckets (O(n))
- Sorted/Tree: Jump to 20, iterate to 30 (O(log n + k))

**Lesson:** Hash optimizes exact match, not ranges.

**Key Insight:** Structure choice depends on operations.

---

### **Q28.** When would you use sorted array over hash table?

**Your Answer:** _______________

**Answer:** Need range queries or sorted output.

| Feature | Hash | Sorted |
|---------|------|--------|
| Lookup | O(1) | O(log n) |
| Range | O(n) | O(log n + k) |
| Insert | O(1) avg | O(n) |
| Delete | O(1) avg | O(n) |
| Sorted | O(n) | O(1) |

Sorted better for: Ranges, extremes, printing order
Hash better for: Lookups, insertions, caching

**Key Insight:** Know your most common operation.

---

### **Q29.** Design choice: URL cache vs database index.

**Your Answer:** _______________

**Answer:**

**URL cache (Facebook):**
- Need: Fast lookup (billions per second)
- Solution: Hash table (O(1))
- Example: `cache[url] = html`

**Database index (MySQL):**
- Need: Range queries (age 20-30), sorted output
- Solution: B-tree (O(log n), maintains order)
- Example: Find all users email > "a@" < "b@"

**Key Insight:** Operations determine choice.

---

### **Q30.** Master trade-off: space vs time in data structures.

**Your Answer:** _______________

**Answer:**

| Structure | Space | Lookup | Insert | Range |
|-----------|-------|--------|--------|-------|
| Array | O(n) | O(n) | O(n) | O(n) |
| Sorted | O(n) | O(log n) | O(n) | O(log n) |
| Hash | O(n) | O(1) avg | O(1) avg | O(n) |
| Tree | O(n) | O(log n) | O(log n) | O(log n) |

More space = more speed (usually). Choose based on constraints.

**Key Insight:** No free lunch. Every choice trades something.

---

### **Q31.** Real system: Design recommendation for 1M users, 10M lookups/sec.

**Your Answer:** _______________

**Answer:** Hash table!

**Why:**
- 10M lookups/sec: Need O(1), not O(log n)
- Hash: 10M × O(1) = manageable
- Tree: 10M × O(log n) = 230M ops (slower)
- Memory: 1M entries × 1KB = 1GB (fine)

**Hybrid:** Cache + Database
- Hot data in hash (fast)
- Cold data in database (persistent)

**Key Insight:** Scale determines choice.

---

### **Q32.** You have code iterating through array repeatedly. Optimize?

**Your Answer:** _______________

**Answer:** Build hash index first, then lookup.

**Before:**
```python
for query in queries:  # 1M queries
    for item in items:  # search 1M items
        if item.id == query:
            process(item)
# Time: 10^12
```

**After:**
```python
index = {}
for item in items:
    index[item.id] = item
for query in queries:
    process(index[query])  # O(1)
# Time: 1M + 1M = 2M
```

**Speedup:** 500,000x!

**Key Insight:** Preprocessing pays off with many queries.

---

### **Q33.** Comparing two approaches: which is better?

**Your Answer:** _______________

**Answer:** Measure! Benchmark on realistic data.

Big-O tells theoretical story:
- Option A: O(n log n) might beat Option B: O(n) if B's constant is huge
- Constants matter in practice
- Cache behavior matters
- Real data matters (edge cases)

**Process:**
1. Understand Big-O
2. Implement both
3. Profile on real data
4. Choose winner

**Key Insight:** Big-O is starting point, not ending point.

---

### **Q34.** Design interview: Implement LRU cache. What structures needed?

**Your Answer:** _______________

**Answer:** Hash map + Doubly-linked list!

**Why:**
- Hash for O(1) lookup (`cache[key]`)
- Linked list for O(1) reordering (recent to front)

```python
class LRUCache:
    def __init__(self, capacity):
        self.cache = {}  # key → node
        self.list = DoublyLinkedList()  # head=recent, tail=old
    
    def get(self, key):
        node = self.cache[key]  # O(1)
        self.list.move_to_front(node)  # O(1)
        return node.value
    
    def put(self, key, value):
        if key in self.cache:
            self.cache[key].value = value
            self.list.move_to_front(...)
        else:
            if len(self.cache) == self.capacity:
                self.cache.pop(self.list.tail.key)
                self.list.remove_tail()
            node = Node(key, value)
            self.cache[key] = node
            self.list.add_to_front(node)
```

**Key Insight:** Combine structures for optimal performance!

---

### **Q35.** Final question: What's most important for DSA success?

**Your Answer:** _______________

**Answer:** Understanding trade-offs and measuring.

1. **Know Big-O:** Theoretical foundation
2. **Understand trade-offs:** Space-time, simplicity-performance
3. **Measure:** Don't assume. Profile real scenarios
4. **Evolve:** Start simple, optimize when needed
5. **Communicate:** Explain choices to team

Engineer's mindset: Choose right tool for problem, know limitations, be willing to revisit.

**Key Insight:** DSA is not just algorithms. It's engineering judgment.

---

## 📊 SCORING GUIDE

**Per question:** 5 points
**Total:** 175 points
**Pass:** 140+ (80%)
**Target:** 160+ (91%)

**By category:**
- Sorting: 14 points
- Hashing: 14 points
- Integration: 7 points

---

**Status:** ✅ Complete Question Bank | Review regularly!

