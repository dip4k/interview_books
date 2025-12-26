# Hash Tables II: Collision Resolution - Chaining vs Open Addressing

## 🗓 Metadata
**Topic:** Collision Resolution Strategies  
**Week:** Week 3  
**Day:** Day 5 of 5  
**Category:** Hash Table Implementation  
**Difficulty:** 🟡 Medium / 🔴 Hard  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

**We have hash tables that achieve O(1) average lookup.**

**But collisions are inevitable** (birthday paradox: √m items cause collisions in table of size m).

**The hard problem:** When two keys hash to the same slot, where do we put the second one?

Two competing strategies:
1. **Chaining:** Allow multiple items per slot (use linked list)
2. **Open Addressing:** Find another empty slot in the same array

**Trade-offs are significant:**
- Chaining: Simple, but pointer overhead, cache-unfriendly
- Open addressing: Faster in practice, but complex deletion

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy 1: Chaining (Cinema Seat Reservation)

**Movie theater has 10 seats.** Each seat number = hash slot.

**Chaining approach:**
```
If seat 5 is taken, hang a note: "overflow goes here"
Person 2 wants seat 5 (h=5): Seat 5 taken, follow note
Follow note: finds list [person_A, person_B, person_C]
Check if person 2 in list: O(3) comparisons

Result: Seat 5 has "chain" of people
```

**Why simple:** 
- Easy to implement (linked list per slot)
- Can exceed table size (many items per slot)

**Why slow:**
- Pointer overhead (each item needs next pointer)
- Cache misses: Following linked list jumps around memory
- Deletions are simple but create fragmentation

### Core Analogy 2: Open Addressing (Parking Lot)

**Parking lot has 10 spaces.** Each space = hash slot.

**Open addressing approach:**
```
If space 5 is taken, try:
- Space 5: Taken
- Space 6: Empty? Yes! Park here.

Next person wants space 5:
- Space 5: Taken
- Space 6: Taken
- Space 7: Empty? Yes! Park here.

Result: Like a crowded parking lot with clumps of filled spaces
```

**Why fast:**
- No pointers, everything in array
- Sequential memory access (good cache behavior)
- Fast for finding empty slots

**Why complex:**
- Deletion is tricky (need tombstones)
- Can't exceed table size (table becomes full)
- Clustering: full spaces form dense groups

### Visual Representation

```
CHAINING:
Hash table (size 11) with linked lists

Index  Chain
0      [ ]
1      [person_A] → [person_B] → [ ]
2      [person_C] → [ ]
3      [ ]
4      [person_D] → [person_E] → [person_F] → [ ]
5      [ ]
...

OPEN ADDRESSING:
Hash table (size 11) with linear probing

Index  Value
0      empty
1      person_A
2      person_C
3      person_B (wanted slot 1, moved to 3)
4      person_D
5      person_E (wanted slot 4, moved to 5)
...

Wasted space: Some empty slots remain
```

---

## 3️⃣ The How — Mechanical Walkthrough

### Chaining Implementation

**Data Structure:**
```
class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  ← Array of linked list heads
    
    class LinkedListNode:
        def __init__(self, key, value):
            self.key = key
            self.value = value
            self.next = None

Insert(key, value):
    index = hash(key) mod size
    
    if table[index] is None:
        table[index] = LinkedListNode(key, value)
    else:
        node = table[index]
        while node:
            if node.key == key:
                node.value = value  ← Update if exists
                return
            if node.next is None:
                node.next = LinkedListNode(key, value)  ← Append if new
                return
            node = node.next

Lookup(key):
    index = hash(key) mod size
    node = table[index]
    while node:
        if node.key == key:
            return node.value  ← Found
        node = node.next
    return None  ← Not found

Delete(key):
    index = hash(key) mod size
    node = table[index]
    
    if node and node.key == key:
        table[index] = node.next  ← Remove head
        return
    
    while node:
        if node.next and node.next.key == key:
            node.next = node.next.next  ← Remove middle/end
            return
        node = node.next
```

**Cost Analysis:**
```
Insert: O(1) expected [find slot O(1), add to list O(1)]
Lookup: O(1 + α) where α = n/m [traverse chain O(1 + α)]
Delete: O(1 + α) [find node O(1 + α), remove O(1)]
```

### Open Addressing: Linear Probing

**Data Structure:**
```
class HashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  ← All values in array
        self.tombstones = set()     ← Track deleted spots

Insert(key, value):
    index = hash(key) mod size
    i = 0
    
    while i < size:
        probe_index = (index + i) mod size
        
        if table[probe_index] is None or probe_index in tombstones:
            table[probe_index] = (key, value)
            tombstones.discard(probe_index)  ← Clear tombstone
            return
        
        if table[probe_index].key == key:
            table[probe_index] = (key, value)  ← Update
            return
        
        i += 1
    
    raise Exception("Table is full")  ← Must resize

Lookup(key):
    index = hash(key) mod size
    i = 0
    
    while i < size:
        probe_index = (index + i) mod size
        
        if table[probe_index] is None:
            return None  ← Empty slot: key not in table
        
        if probe_index not in tombstones and table[probe_index].key == key:
            return table[probe_index].value  ← Found
        
        i += 1
    
    return None  ← Searched all, not found

Delete(key):
    index = hash(key) mod size
    i = 0
    
    while i < size:
        probe_index = (index + i) mod size
        
        if table[probe_index] is None:
            return  ← Not found
        
        if probe_index not in tombstones and table[probe_index].key == key:
            tombstones.add(probe_index)  ← Mark as deleted
            return
        
        i += 1
```

**Key Insight: Tombstones**
```
Why not just delete the entry?

Consider: Insert 1, 2, 3 (all hash to 0, linear probe)
Table: [1, 2, 3, empty, ...]

If we delete 1: [empty, 2, 3, empty, ...]
Lookup 3: hash to 0, find empty → assume not in table!
Wrong! We broke the chain.

Solution: Mark as tombstone (deleted, but still part of chain)
[tombstone, 2, 3, empty, ...]
Lookup 3: hash to 0, skip tombstone, continue, find 3!
```

### Open Addressing: Quadratic Probing

**Linear probing problem:** Clustering

```
If we insert many items hashing to same slot:
[filled, filled, filled, filled, empty, ...]

Creates dense cluster
Each new insertion scans many filled slots

Solution: Don't probe sequentially, probe by squares
```

**Quadratic Probing:**
```
probe_index = (index + i²) mod size  [instead of index + i]

Insert at hash(key) = 5:
i=0: Try (5 + 0²) mod m = 5 (filled)
i=1: Try (5 + 1²) mod m = 6 (filled)
i=2: Try (5 + 2²) mod m = 9 (filled)
i=3: Try (5 + 3²) mod m = 14 mod m (might be empty)
i=4: Try (5 + 4²) mod m = 21 mod m (might be empty)

Result: Jumps further, avoids primary clustering
```

### Open Addressing: Double Hashing

**Problem with linear/quadratic:** Secondary clustering (different starting points probe same sequence).

**Double hashing:**
```
probe_index = (h1(key) + i × h2(key)) mod size

h1: Primary hash function
h2: Secondary hash function (must be coprime with table size)

Insert at h1(key) = 5, h2(key) = 3:
i=0: Try (5 + 0 × 3) mod m = 5 (filled)
i=1: Try (5 + 1 × 3) mod m = 8 (filled)
i=2: Try (5 + 2 × 3) mod m = 11 (might be empty)
i=3: Try (5 + 3 × 3) mod m = 14 mod m

Different h2 values give different probe sequences
No clustering!
```

---

## 4️⃣ Visualization — Simulation & Examples

### Example 1: Chaining

**Scenario:** Insert [7, 18, 29, 14, 23] into hash table of size 11 using chaining

**Hash function:** h(k) = k mod 11

**After all insertions:**
```
Index  Chain
0      empty
1      [23] → null
2      empty
3      [14] → null
4      empty
5      empty
6      empty
7      [7] → [18] → [29] → null  (all hash to 7!)
8      empty
9      empty
10     empty

Load factor α = 5/11 = 0.45 (acceptable)
Chain at index 7 has length 3
Average chain length = 5/11 = 0.45
```

**Lookup 18:**
```
h(18) = 18 mod 11 = 7
Check chain at 7: [7] → [18] → [29]
Is 18 here? Yes! Found after 2 comparisons.
```

**Lookup 100:**
```
h(100) = 100 mod 11 = 1
Check chain at 1: [23]
Is 100 here? No (100 ≠ 23)
End of chain: Return Not found. O(1 + α) = O(1.45)
```

**Delete 18:**
```
h(18) = 7
Chain at 7: [7] → [18] → [29]
Find 18: Update pointers [7] → [29]
Chain at 7: [7] → [29]
```

### Example 2: Open Addressing (Linear Probing)

**Scenario:** Same insertions with open addressing, table size 11

**Insert 7:**
```
h(7) = 7
Table[7] is empty → Insert
Table: [_, _, _, _, _, _, _, 7, _, _, _]
```

**Insert 18:**
```
h(18) = 7
Table[7] is filled with 7
i=1: Try (7 + 1) mod 11 = 8 → Empty → Insert
Table: [_, _, _, _, _, _, _, 7, 18, _, _]
```

**Insert 29:**
```
h(29) = 7
Table[7] is filled
i=1: Try (7 + 1) mod 11 = 8 → Filled with 18
i=2: Try (7 + 2) mod 11 = 9 → Empty → Insert
Table: [_, _, _, _, _, _, _, 7, 18, 29, _]
```

**Insert 14:**
```
h(14) = 3
Table[3] is empty → Insert
Table: [_, _, _, 14, _, _, _, 7, 18, 29, _]
```

**Insert 23:**
```
h(23) = 1
Table[1] is empty → Insert
Table: [_, 23, _, 14, _, _, _, 7, 18, 29, _]
```

**Result:** Cluster of items starting at index 7
```
Items hash to 7: 7, 18, 29
They occupy consecutive slots: 7, 8, 9
(Primary clustering example)
```

**Lookup 29:**
```
h(29) = 7
i=0: Table[7] = 7 (not 29, continue)
i=1: Table[8] = 18 (not 29, continue)
i=2: Table[9] = 29 (found!) O(3 comparisons)
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Complexity Comparison

| Operation | Chaining | Open Addressing |
|-----------|----------|-----------------|
| **Lookup** | O(1 + α) | O(1/(1-α)) |
| **Insert** | O(1 + α) | O(1/(1-α)) |
| **Delete** | O(1 + α) | O(1/(1-α)) + tombstone |
| **Space** | n + m | Exactly m |
| **Utilization** | Can exceed 100% | Must stay < 100% |

**Why different formulas:**

```
Chaining: Average chain length = n/m = α
         Expected nodes to check = 1 + α

Open Addressing: Expected probe length = 1 + 1/(1-α)
                 As α → 1, cost → ∞

Example: α = 0.8
Chaining: 1 + 0.8 = 1.8 comparisons
Open: 1 + 1/0.2 = 6 comparisons (much worse!)
```

**Practical implications:**
```
With chaining, can tolerate α = 1.0 or even higher
With open addressing, must keep α < 0.7-0.8
```

### When Each Excels

**Chaining excels when:**
1. Load factor might exceed 1.0 (many collisions okay)
2. Deletion is frequent (simple with linked lists)
3. Simple implementation preferred
4. Memory overhead acceptable (pointers per item)

**Open Addressing excels when:**
1. Space is premium (no extra pointers)
2. Cache efficiency critical (fewer memory hops)
3. Load factor stays low (α < 0.75)
4. Items don't move after insertion (no tombstones accumulation)

### Real Performance Metrics

**1 million items, vary load factor:**

| α | Chaining Lookups | Open Addressing Lookups |
|---|------------------|------------------------|
| 0.5 | 1.5 comparisons | 2 comparisons |
| 0.75 | 1.75 comparisons | 4 comparisons |
| 0.9 | 1.9 comparisons | 10 comparisons |
| 1.0 | 2 comparisons | ∞ (must resize) |

**Cache behavior:**
```
Chaining: Pointer chasing = cache misses (slower in practice)
Open: Linear probing = sequential memory = cache hits (faster in practice)
```

Despite worse Big-O, open addressing is often faster due to CPU caches!

---

## 6️⃣ Real System Integration

### Python Dictionaries (Hybrid Approach)

```python
d = {"apple": 1, "banana": 2}
```

**Python uses open addressing (since Python 3.6+):**
- Compact hash table
- Space-efficient
- Faster cache behavior
- Uses "compact" representation where keys/values are in separate array

**Why Python chose open addressing:**
```
- Space is important (millions of dicts in programs)
- Cache behavior matters (dictionaries are heavily used)
- Deletion is less common than lookup
```

### Java HashMaps (Chaining Approach)

```java
HashMap<String, Integer> map = new HashMap<>();
map.put("apple", 1);
```

**Java uses chaining:**
```
- More flexible (can handle high load factors)
- Simpler to understand for average programmer
- Acceptable memory overhead (pointers are small)
- Tree-based chains for O(log n) when many collisions
```

**Why Java chose chaining:**
```
- Easier to get right (less complex deletion)
- Scales well with hash function quality
- Good balance of simplicity and performance
```

### Database Indexes

**Hash indexes (MySQL, PostgreSQL):**
```sql
CREATE INDEX idx_user_id USING HASH ON users(id);
```

**Use:** Fast exact-match lookups
**Strategy:** Usually open addressing with careful load factor management
**Why:** 
- O(1) lookup
- Space-efficient
- No range queries needed

---

## 7️⃣ Concept Crossovers

### Builds On

**Day 4 concepts:**
- Hash functions
- Load factor
- Collision inevitability

### Builds Toward

**Applications:**
- **Dynamic programming:** Memoization uses chaining (Python dicts)
- **Sliding window:** Frequency counting (Week 4)
- **Graph algorithms:** Adjacency lists use hash tables

---

## 8️⃣ Mathematical & Theoretical Perspective

### Proof: Open Addressing Expected Probes

**Claim:** With open addressing and load factor α, expected probes = 1/(1-α)

**Proof Sketch:**

```
Probability that a random slot is empty: (1 - α)

Probability that first probe hits empty: (1 - α)
Probability that first two probes hit filled, third hits empty: α × (1 - α)
...

Expected probes = Σ i × P(first i-1 filled, i-th empty)
                = Σ i × α^(i-1) × (1 - α)
                = (1 - α) × Σ i × α^(i-1)
                = (1 - α) × 1/(1 - α)²
                = 1/(1 - α)
```

As α increases:
```
α = 0.5: E[probes] = 1/0.5 = 2
α = 0.75: E[probes] = 1/0.25 = 4
α = 0.9: E[probes] = 1/0.1 = 10
```

This is why we must keep α < 0.75 with open addressing!

---

## 9️⃣ Algorithmic Design Intuition

### Decision Framework

```
Choose Chaining when:
  - You might exceed load factor 1.0
  - Deletion is frequent
  - Simple implementation preferred
  - Memory overhead acceptable

Choose Open Addressing when:
  - Space is critical
  - Load factor stays ≤ 0.75
  - Cache efficiency matters
  - Insertion-heavy workload

Choose based on:
  1. Your constraints (memory, speed)
  2. Usage pattern (insert-heavy vs delete-heavy)
  3. Your comfort (simple vs optimized)
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Why is deletion tricky in open addressing but simple in chaining?**

Your reasoning:
- In chaining, just remove the node from the linked list (O(1))
- In open addressing, if you delete, you break the probe chain
- Example: Insert [1,2,3] at hashes [5,5,5]. They land at [5,6,7]. If you delete entry at 6, lookup at 5→6 finds empty and returns "not found"
- Why doesn't chaining have this problem?

**Hint:** Linked lists are separate from array slots.

---

**Question 2: Why is open addressing faster than chaining despite worse Big-O?**

Your reasoning:
- Big-O suggests open addressing is worse (1/(1-α) vs 1+α)
- But in practice, open addressing is often faster
- What's the hidden constant factor in chaining?
- What advantage does open addressing have for modern CPUs?

**Hint:** Cache hits vs cache misses.

---

**Question 3: If you use Python dicts (open addressing), why keep track of tombstones?**

Your reasoning:
- Deletions in open addressing create empty slots
- But we need to distinguish "never inserted" from "deleted"
- Without tombstones, how does lookup break?
- When would you remove tombstones?

**Hint:** Periodically rehash the table to remove tombstones.

---

**Question 4: Is double hashing strictly better than linear probing?**

Your reasoning:
- Double hashing avoids clustering
- But linear probing is simpler
- When would linear probing suffice?
- When would you need double hashing?

**Hint:** Depends on load factor and hash function quality.

---

**Question 5: Why does Java use chaining instead of open addressing?**

Your reasoning:
- Open addressing is faster (cache)
- Chaining is simpler
- Why would simplicity win over speed?
- What's more important for Java developers?

**Hint:** Correctness and maintainability often beat micro-optimizations.

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Chaining: Simple, slow probing, handles high load factors. Open addressing: Fast, complex deletion, must keep α low. Choose based on constraints and workload.**

### Mnemonic: "CHAOS"

- **C**haining: Linked **c**hains per slot
- **H**ashing: Collision **h**andling
- **A**ddressing: **A**ddress empty slot (open)
- **O**verhead: Memory vs speed trade-off
- **S**pace: Utilization vs performance

---

## 📚 Supplementary Data

### Clustering Visualization

```
PRIMARY CLUSTERING (Linear Probing):
Items that hash to same slot form dense group

Insert [5, 16, 27] (all hash to 5):
h(5) = 5:    Table[5] = 5
h(16) = 5:   Table[5] filled → Table[6] = 16
h(27) = 5:   Table[5,6] filled → Table[7] = 27

Result: [_, _, _, _, _, 5, 16, 27, _, _, _] ← Dense cluster

Next insert at hash 6:
h(x) = 6:    Table[6] filled → Table[7] filled → Table[8]
Must scan through cluster created by previous items!

SECONDARY CLUSTERING (Quadratic/Double Hash):
Items with same h1 but different h2 use different sequences

Avoids dense clusters
Better for long probes
```

### Tombstone Accumulation Problem

```
Insert-heavy workload:
1. Insert 1000 items
2. Delete 500 items (creates 500 tombstones)
3. Insert 500 items (encounter tombstones, use them)

Lookup problem:
After many cycles, table is full of tombstones
Probing costs increase (must skip tombstones)

Solution: Periodic rehashing
When α + tombstones_ratio > threshold:
  Rebuild hash table (all non-tombstone items)
  Cost: O(n) but infrequent
```

---

## 🔗 External References

1. **Visualization:**
   - Hash Table Collision Visualizer: https://www.cs.usfca.edu/~galles/visualization/OpenHash.html

2. **Real Implementations:**
   - Python dict source: https://github.com/python/cpython/blob/main/Objects/dictobject.c
   - Java HashMap source: https://github.com/openjdk/jdk/blob/master/src/java.base/share/classes/java/util/HashMap.java

3. **Theory & Analysis:**
   - Knuth's "The Art of Computer Programming" Vol. 3 (classic reference)
   - Donald Knuth's hash table analysis papers

---

**Word Count:** ~2,600  
**Reading Time:** ~75 minutes  
**Status:** ✅ Complete with all 11 sections + supplementary material
