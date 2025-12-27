# Week 2, Day 5: Binary Search

## 🗓 Metadata
**Week:** 2 | **Day:** 5 of 5 | **Topic:** Binary Search  
**Category:** Linear Structures | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 2 Days 1-4, Arrays | **Time:** 90-120 minutes

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
You have 1 billion sorted records. Linear search: 1 billion comparisons. Binary search: 30 comparisons.

**Design Problems Solved:**
- O(log n) search in sorted data
- Foundation for databases (B-tree searches), version control (git bisect), standard libraries (bisect module)
- Enables "search by guessing and eliminating half"

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
You're guessing a number 1-1000. Each guess eliminates half the remaining numbers.

```
Range: 1-1000
Guess 500: Too high
Range: 1-499
Guess 250: Too low
Range: 251-499
Guess 375: Too high
Range: 251-374
...
After 10 guesses: Found (log₂1000 ≈ 10)
```

**Visual:**
```
Array (sorted): [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
                [0, 1, 2, 3, 4,  5,  6,  7,  8,  9]  indices

Search for 7:
Step 1: left=0, right=9
        mid=4 → arr[4]=9
        9 > 7, so right=3
        
Step 2: left=0, right=3
        mid=1 → arr[1]=3
        3 < 7, so left=2
        
Step 3: left=2, right=3
        mid=2 → arr[2]=5
        5 < 7, so left=3
        
Step 4: left=3, right=3
        mid=3 → arr[3]=7
        7 == 7, found!
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Algorithm:**
```
BinarySearch(arr, target):
    left = 0, right = n-1
    
    while left <= right:
        mid = (left + right) / 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1  // not found
```

**Cost:** O(log n) — halve search space each iteration

---

## 4️⃣ VISUALIZATION — Simulation & Examples

```
Search for 11 in [1, 3, 5, 7, 9, 11, 13, 15]

left=0, right=7
  mid=3 → arr[3]=7
  7 < 11 → left=4

left=4, right=7
  mid=5 → arr[5]=11
  11 == 11 → return 5 ✓
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Scenario | Cost | Notes |
|----------|------|-------|
| **Found at middle** | O(1) | Best case |
| **Found after k iterations** | O(k) | General case |
| **Not found** | O(log n) | Worst case |
| **Space** | O(1) | Iterative version |

**Precondition:** Array must be sorted! Sorting violations are common bugs.

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Databases:** B-tree nodes use binary search to find child  
**Libraries:** C++ `std::lower_bound`, Python `bisect.bisect`  
**Version Control:** Git bisect finds breaking commit in O(log n) tests  

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds on:** Arrays, sorting  
**Built by:** Divide-and-conquer paradigm  
**Used in:** B-trees, databases, git bisect  

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Recurrence:**
```
T(n) = T(n/2) + O(1)
     = T(n/4) + O(1) + O(1)
     = T(n/2^k) + O(k)

When n/2^k = 1: k = log₂n
So T(n) = O(log n)
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**Use binary search when:**
- Array is sorted
- Need O(log n) search
- Can afford binary search overhead (typically < linear for n > 100)

**Common mistake:** Using on unsorted array (completely breaks algorithm)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why must the array be sorted for binary search to work?

**Q2:** For n=1 million, how many comparisons max? (Linear vs binary)

**Q3:** Can you binary search on a linked list?

**Q4:** What's the formula for middle index? Why (left + right) / 2 not left + (right - left) / 2?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Binary search: O(log n) via divide-by-2. Requires sorted array. Precondition is everything.**

