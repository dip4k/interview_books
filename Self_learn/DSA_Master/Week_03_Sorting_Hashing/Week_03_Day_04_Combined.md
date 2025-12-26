# 📘 WEEK 3 DAY 4: HASH APPLICATIONS & ADVANCED TOPICS

**Week 3, Day 4: Real-World Hashing**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT

### 1️⃣ The Why

**Problem:** Hashing enables many practical applications.

Applications:
- **Deduplication:** Count unique items
- **Caching:** Remember expensive computations
- **Spell checking:** Dictionary lookups
- **Databases:** Index optimization
- **Security:** Password verification

---

### 2️⃣ The What

**Application 1: Deduplication**
```python
def count_unique(arr):
    seen = set()  # hash set
    for item in arr:
        seen.add(item)
    return len(seen)

# [1,2,2,3,3,3] → {1,2,3} → 3
# Time: O(n) average
```

**Application 2: Caching**
```python
def fibonacci(n, cache={}):
    if n in cache:
        return cache[n]
    if n <= 1:
        return n
    result = fibonacci(n-1, cache) + fibonacci(n-2, cache)
    cache[n] = result
    return result

# Without cache: O(2^n)
# With cache: O(n)
```

**Application 3: Finding Duplicates**
```python
def find_first_unique(arr):
    count = {}  # hash map
    for item in arr:
        count[item] = count.get(item, 0) + 1
    for item in arr:
        if count[item] == 1:
            return item
    return None
```

---

### 3️⃣ The How

**Bloom Filter:** Space-efficient set membership
```python
class BloomFilter:
    def __init__(self, size=100):
        self.bits = [False] * size
        self.size = size
    
    def add(self, item):
        index = hash(item) % self.size
        self.bits[index] = True
    
    def contains(self, item):
        index = hash(item) % self.size
        return self.bits[index]
    
    # False positives possible!
    # No false negatives
```

**Counting Bloom Filter:** Handle deletions
```python
class CountingBloomFilter:
    def __init__(self, size=100):
        self.counters = [0] * size
        self.size = size
    
    def add(self, item):
        index = hash(item) % self.size
        self.counters[index] += 1
    
    def remove(self, item):
        index = hash(item) % self.size
        self.counters[index] -= 1
```

---

### 4️⃣ Visualization

**Deduplication with Hash Set:**
```
Input: [1, 2, 2, 3, 3, 3]

Process:
  Add 1 → {1}
  Add 2 → {1, 2}
  Add 2 → already exists, skip
  Add 3 → {1, 2, 3}
  Add 3 → already exists, skip
  Add 3 → already exists, skip

Result: {1, 2, 3}
Unique count: 3
Time: O(n)
```

**Caching Fibonacci:**
```
fib(5) without cache: 15 calls (exponential)
fib(5) with cache:
  fib(5) → compute
    fib(4) → compute
      fib(3) → compute
        fib(2) → compute
          fib(1) → cached!
        fib(2) → cached!
      fib(3) → cached!
    fib(4) → cached!

5 computations vs 15!
```

---

### 5️⃣ Critical Analysis

**Time Complexities:**

| Operation | Time | Space |
|-----------|------|-------|
| Dedup (set) | O(n) | O(n) |
| Caching | O(1) lookup | O(unique subproblems) |
| Bloom filter | O(1) | O(size) small |
| Count items | O(n) insert, O(1) lookup | O(unique items) |

**Space-Time Trade-offs:**
```
Bloom filter: O(1) space, O(1) query, but false positives
Hash set: O(n) space, O(1) query, exact answers
Sorted array: O(n) space, O(log n) query, exact answers
```

---

### 6️⃣ Real Systems

**Caching Examples:**
- CPU cache (L1, L2, L3) use hash-based indexing
- Database query result caching (Redis, Memcached)
- Browser caches web pages

**Bloom Filters:**
- Database indexes (check if key exists)
- Spam filters (check if email in blacklist)
- Networking (routers filter packets)

**Hash Sets:**
- Spell checkers (is word in dictionary?)
- Deduplication (extract unique values)
- Set operations (union, intersection)

---

### 7️⃣ Connections

Builds on: Days 1-3 (hashing)

Enables: Advanced data structures, optimization

---

### 8️⃣ Mathematics

**Collision Probability (Birthday Paradox):**
```
With m buckets, n items:
P(collision) ≈ 1 - e^(-n²/(2m))

n=100, m=1000: ≈ 4.8% collision
n=100, m=100: ≈ 39% collision
n=1000, m=1000: ≈ 93% collision
```

---

### 9️⃣ Design Intuition

**When to Use:**
- Deduplication: Use hash set
- Caching: Use hash map
- Space critical: Bloom filter
- Membership test: Hash set

---

### 🔟 Knowledge Check

1. What's false positive in Bloom filter?
2. Why is caching O(1) lookup?
3. How many unique items in [1,1,1,2,2,3]?
4. Can Bloom filter have false negative?
5. Dedup complexity vs sorted approach?
6. When would Bloom filter be better?
7. Caching space vs time trade-off?

### 1️⃣1️⃣ Hooks

**One-liner:** "Hashing enables fast dedup, caching, and lookups in practice."

---

## PART 2: QUICK SUMMARY

**Applications:**
- **Dedup:** O(n) time, O(n) space
- **Cache:** O(1) lookup, O(subproblems) space
- **Bloom:** O(1), small space, false positives
- **Count:** O(n) time, O(unique) space

---

## PART 3: QUESTIONS & ANSWERS

**Q1:** Bloom filter false positive vs negative?
**A:** False positive possible (think in set when not). False negative impossible.

**Q2:** Caching fibonacci reduces what?
**A:** Time from O(2^n) to O(n). Each unique subproblem computed once.

**Q3:** Dedup approach comparison?
**A:** Hash set: O(n). Sorted: O(n log n) + O(n) scan. Hash wins!

**Q4:** Bloom filter trade-off?
**A:** O(1) space/time but false positives. Useful when space critical.

**Q5:** Why cache helps?
**A:** Avoids recomputation. Hash lookup O(1) vs recomputing O(expensive).

**Q6:** When is Bloom better than hash set?
**A:** Space critical and false positives acceptable.

**Q7:** Counting items with hash?
**A:** Hash map: count[item] = count.get(item,0) + 1. O(n) time, O(unique) space.

---

## PART 4: README

**90-Minute Study:**
1. Why (15 min): Real applications
2. What (15 min): Dedup, caching, Bloom
3. How (15 min): Implementation patterns
4. Visualization (15 min): See applications
5. Analysis (10 min): Space-time tradeoffs

**Key Skill:** Recognize when hashing applies

---

**Status:** ✅ Day 4 Complete | **Next:** Day 5 - Sorting & Hashing Integration

