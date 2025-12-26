# 📘 WEEK 4.5 DAY 1: HASH MAP / HASH SET - Complete Learning Package

**Week 4.5, Day 1: Data Structure Pattern - Hash-Based Lookup & Frequency Tracking**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT (11 Sections)

### 1️⃣ The Why: Engineering Motivation

**Problem:** Given an array, check if all elements are unique.

Real-world:
- **User registration:** Check if email already exists in database
- **Cache systems:** Store recently accessed items for O(1) lookup
- **Deduplication:** Remove duplicate entries from logs
- **Frequency analysis:** Count word occurrences in document
- **Autocomplete:** Store and lookup common search terms

**Naive approach:** Nested loop O(n²)
```python
def all_unique_naive(arr):
    for i in range(len(arr)):
        for j in range(i+1, len(arr)):
            if arr[i] == arr[j]:
                return False
    return True
```

**Hash Set approach:** O(n) time, O(n) space
```python
def all_unique_hash(arr):
    seen = set()
    for num in arr:
        if num in seen:
            return False
        seen.add(num)
    return True
```

**Performance difference:** 1000 items: 1M ops vs 1K ops (1000x faster!)

---

### 2️⃣ The What: Mental Model

**Core Insight:** Hash data structures trade space for time, enabling O(1) average-case lookup and insertion.

**Hash Set vs Hash Map:**
- **Hash Set:** Stores unique values only, fast membership testing
- **Hash Map:** Stores key-value pairs, fast key lookup and retrieval

**Why this works:**
- Hash function maps values to indices
- O(1) average insertion, deletion, lookup
- O(n) space to store elements
- Collision resolution via chaining or open addressing

**Visual:**
```
Hash Set: {1, 5, 7, 3}
Operations:
  5 in set → O(1) lookup → True
  9 in set → O(1) lookup → False
  set.add(2) → O(1) insertion → {1, 5, 7, 3, 2}

Hash Map: {"apple": 5, "banana": 3, "cherry": 7}
Operations:
  map["apple"] → O(1) lookup → 5
  map["date"] → O(1) lookup → KeyError
  map["date"] = 2 → O(1) insertion
```

**Key Property:** Average case O(1) for basic operations (add, remove, lookup).

---

### 3️⃣ The How: Mechanics

**Hash Set Operations:**
```python
# Create empty set
s = set()

# Add element: O(1)
s.add(5)

# Check membership: O(1)
if 3 in s:
    print("Found")

# Remove element: O(1)
s.remove(5)  # Raises KeyError if not found
s.discard(5)  # Doesn't raise error

# Iterate: O(n)
for item in s:
    print(item)

# Clear all: O(n)
s.clear()
```

**Hash Map Operations:**
```python
# Create empty map
m = {}

# Insert/update: O(1)
m["key"] = "value"

# Lookup: O(1)
value = m["key"]  # Raises KeyError if not found
value = m.get("key", "default")  # Returns default if not found

# Delete: O(1)
del m["key"]

# Check key existence: O(1)
if "key" in m:
    print("Found")

# Iterate keys: O(n)
for key in m.keys():
    print(key)

# Iterate values: O(n)
for value in m.values():
    print(value)

# Iterate key-value pairs: O(n)
for key, value in m.items():
    print(key, value)
```

**Complexity:**
- Insert: O(1) average, O(n) worst case (hash collision)
- Delete: O(1) average, O(n) worst case
- Lookup: O(1) average, O(n) worst case
- Space: O(n) for storing n elements

---

### 4️⃣ Visualization: Examples

**Example 1: Duplicate Detection**
```
Array: [1, 2, 3, 2, 4]

Step 1: seen = {}, num = 1
        1 not in {} → add to seen
        seen = {1}

Step 2: seen = {1}, num = 2
        2 not in {1} → add
        seen = {1, 2}

Step 3: seen = {1, 2}, num = 3
        3 not in {1, 2} → add
        seen = {1, 2, 3}

Step 4: seen = {1, 2, 3}, num = 2
        2 in {1, 2, 3} → DUPLICATE FOUND!
        Return False
```

**Example 2: Frequency Counting**
```
String: "hello"

Step 1: freq = {}, char = 'h'
        freq['h'] = 1
        freq = {'h': 1}

Step 2: freq = {'h': 1}, char = 'e'
        freq['e'] = 1
        freq = {'h': 1, 'e': 1}

Step 3-4: freq['l'] = 2
        freq = {'h': 1, 'e': 1, 'l': 2}

Step 5: freq['o'] = 1
        freq = {'h': 1, 'e': 1, 'l': 2, 'o': 1}

Result: {'h': 1, 'e': 1, 'l': 2, 'o': 1}
```

**Example 3: Two Sum Lookup**
```
Array: [2, 7, 11, 15], Target: 9

Step 1: num = 2, complement = 9 - 2 = 7
        7 not in seen yet
        seen = {2}

Step 2: num = 7, complement = 9 - 7 = 2
        2 in seen! FOUND!
        Return indices of 2 and 7

Result: [0, 1] (indices of 2 and 7)
```

---

### 5️⃣ Critical Analysis

**Time Complexity:**
- Insert: O(1) average, O(n) worst
- Delete: O(1) average, O(n) worst
- Lookup: O(1) average, O(n) worst
- Iterate: O(n)

**Space Complexity:**
- O(n) to store n elements

**Why O(1) Average?**
Hash function distributes keys uniformly across hash table.
With good hash function, collisions rare.
Therefore, on average, operations are O(1).

**Worst Case O(n)?**
Poor hash function causes many collisions.
All elements hash to same bucket.
Operations degrade to O(n).
In practice, Python's hash functions are very good.

**Comparison to Other Approaches:**

| Approach | Insert | Delete | Lookup | Space |
|----------|--------|--------|--------|-------|
| Array | O(1) | O(n) | O(n) | O(n) |
| Sorted Array | O(n) | O(n) | O(log n) | O(n) |
| Hash Set/Map | O(1) avg | O(1) avg | O(1) avg | O(n) |
| Linked List | O(1) | O(n) | O(n) | O(n) |

---

### 6️⃣ Real System Integration

**Web Caches:**
Recently accessed pages stored in hash map for O(1) retrieval.

**Database Indexing:**
Primary key index uses hash table for O(1) record lookup.

**Compiler Symbol Tables:**
Variable names mapped to memory addresses for O(1) lookup.

**Load Balancing:**
Cache user sessions in hash map for O(1) session retrieval.

---

### 7️⃣ Concept Crossovers

**Builds On:**
- Week 1: Array operations
- Week 2: Time-space tradeoffs
- Week 3: Lookup operations
- Week 4: Pattern recognition

**Enables:**
- Week 4.5: Other patterns (all use hashing)
- Week 5: Advanced algorithms
- Interview problems (70% use hashing!)

**Related Techniques:**
- Set intersection, union, difference
- Frequency-based algorithms
- Grouping problems (anagrams, etc.)

---

### 8️⃣ Mathematical Perspective

**Hash Function Properties:**
- Deterministic: same input → same output
- Uniform distribution: minimize collisions
- Fast to compute: O(1)

**Collision Resolution:**
- Chaining: multiple values per bucket (Python uses this)
- Open addressing: find next empty bucket

**Load Factor:**
- Load factor = n / bucket_count
- When > 0.75, typically resize
- Resizing redistributes elements

---

### 9️⃣ Algorithmic Design Intuition

**When to Use Hash Set:**
1. Need fast membership testing
2. Duplicates matter
3. Order doesn't matter
4. Space not critical

**When to Use Hash Map:**
1. Need key-value associations
2. Fast lookup by key
3. Need frequency counts
4. Store related data

**When NOT to Use:**
1. Need sorted order (use TreeMap)
2. Need range queries (use arrays)
3. Space is very limited
4. Hash collisions likely (rare)

---

### 🔟 Knowledge Check

1. What's average time complexity for hash set operations?
2. When would hash set be slower than O(1)?
3. Trace duplicate detection with hash set
4. What's space tradeoff for hash sets?
5. How do collisions affect performance?
6. When to use set vs. sorted list?
7. How to count element frequencies?

---

### 1️⃣1️⃣ Retention Hooks

**One-liner:** "Hash sets trade O(n) space for O(1) lookup, making membership testing instant."

**Mnemonic - "HASH FAST":**
- **H**ash function maps to buckets
- **A**verage O(1) operations
- **S**pace O(n) for storage
- **H**igh-speed lookup guaranteed

**F**ast lookup: constant time
- **A**dd, remove, check: all O(1)
- **S**pace-time tradeoff
- **T**rade memory for speed

**Visual Memory:**
```
Think: "Phone book lookup"
Name → Hash function → Index
John → 5 → Page 5 (O(1) lookup)
Fast because direct access to page
```

**Story:** "A phone book sorted alphabetically lets you find someone's name in O(log n) with binary search. A hash table with perfect hashing finds them in O(1) by directly computing their position."

---

## PART 2: QUICK SUMMARY

**Hash Set/Map Essence:**

Trade space for time to achieve O(1) average lookup, insertion, deletion using hash functions.

**When to Use:**
- Need fast membership testing ✓
- Need frequency counting ✓
- Need O(1) lookups ✓
- Space available ✓

**Template:**
```python
# Duplicate detection
def has_duplicate(arr):
    seen = set()
    for num in arr:
        if num in seen:
            return True
        seen.add(num)
    return False

# Frequency counting
def count_frequencies(arr):
    freq = {}
    for num in arr:
        freq[num] = freq.get(num, 0) + 1
    return freq

# Two sum with hash
def two_sum(arr, target):
    seen = {}
    for num in arr:
        complement = target - num
        if complement in seen:
            return [seen[complement], arr.index(num)]
        seen[num] = num
    return []
```

**Real Problems:**
- Contains Duplicate
- Valid Anagram
- Two Sum
- Group Anagrams
- Intersection of Arrays

---

## PART 3: SOCRATIC QUESTIONS & ANSWERS

**Q1:** What's the average time complexity of hash set operations and why?

**A:** O(1) average. Hash function distributes keys uniformly, so most operations hit their bucket directly without collision. With good hash function, collisions are rare enough to maintain O(1) average.

---

**Q2:** When would hash set operation be slower than O(1)?

**A:** Worst case O(n) when poor hash function causes many collisions. All elements hash to same bucket, operations degrade to linked list search. In practice with Python's hash functions, this is extremely rare.

---

**Q3:** Trace duplicate detection with hash set on [1, 3, 2, 3, 5]

**A:**
```
seen = {}, num = 1 → seen = {1}
seen = {1}, num = 3 → seen = {1, 3}
seen = {1, 3}, num = 2 → seen = {1, 3, 2}
seen = {1, 3, 2}, num = 3 → 3 IN SET! Return True (duplicate found)
```

---

**Q4:** How do you count frequencies of elements?

**A:**
```python
def count_freq(arr):
    freq = {}
    for num in arr:
        freq[num] = freq.get(num, 0) + 1
    return freq

# Example: [1, 2, 2, 3, 3, 3]
# Result: {1: 1, 2: 2, 3: 3}
```

---

**Q5:** What's the space-time tradeoff for hash sets?

**A:** Use O(n) extra space to save time on operations. Without hash set (using array), lookup is O(n). With hash set, lookup is O(1). Trade space for speed.

---

**Q6:** When would you use sorted list instead of hash set?

**A:** When you need sorted order or range queries. Hash set is unordered, so can't get sorted elements or range efficiently. Use TreeMap/sorted list for ordered data.

---

**Q7:** How does collision resolution work?

**A:** Python uses chaining: multiple values hash to same bucket are stored in linked list. When looking up, hash to bucket, then search linked list. With good hash function, linked lists are short, keeping O(1) average.

---

## PART 4: README

**90-Minute Study Guide:**
1. The Why (10 min): Understand performance need
2. The What (15 min): Hash set/map concepts
3. The How (15 min): Implementation mechanics
4. Visualization (20 min): Trace examples
5. Quick Summary (5 min): Key points
6. Questions (15 min): Test understanding

**Key Skill:** Recognize when hashing solves problem, implement efficiently

**Practice:** Duplicate detection, frequency counting, two sum

**Connection:** Foundation for almost all problem-solving. Used in 70% of interview problems!

---

**Status:** ✅ Day 1 Complete | **Next:** Day 2 - Monotonic Stack

