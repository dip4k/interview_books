# 📘 WEEK 3 DAY 2: ADVANCED SORTS (Merge Sort & Quick Sort)

**Week 3, Day 2: Divide-and-Conquer Sorting**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🔴 Hard | Target: 4-5/5

---

## PART 1: MAIN CONTENT

### 1️⃣ The Why

**Problem:** Elementary sorts are O(n²). Can we do better?

**Insight:** Divide problem in half, solve each half, combine.

Real-world:
- **Databases:** Must sort millions of records fast
- **Distributed systems:** Merge sort works well with disk I/O
- **Production code:** Quicksort is default in most languages

**Performance difference:**
```
1 million items:
  Bubble: 10^12 comparisons (hours)
  Merge: 20 million comparisons (0.02 seconds)
  Quick: 20 million average (0.02 seconds)
```

---

### 2️⃣ The What: Mental Model

**Merge Sort: Divide → Conquer → Combine**

```
[3,1,4,1,5,9,2,6]
    ↓ divide in half
[3,1,4,1]  [5,9,2,6]
    ↓ divide in half
[3,1] [4,1] [5,9] [2,6]
    ↓ divide in half
[3][1] [4][1] [5][9] [2][6]
    ↓ merge pairs (conquer)
[1,3] [1,4] [5,9] [2,6]
    ↓ merge pairs
[1,1,3,4] [2,5,6,9]
    ↓ merge all
[1,1,2,3,4,5,6,9]
```

**Quick Sort: Pivot → Partition → Recurse**

```
[3,1,4,1,5,9,2,6]
    ↓ pick pivot (say 3)
[1,2] 3 [4,5,9,6]
       ↓ less than 3
    ↓ recurse on parts
[1,2] 3 [4,5,6,9]
    ↓ combine
[1,2,3,4,5,6,9]
```

---

### 3️⃣ The How: Mechanics

**Merge Sort:**
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])        # Divide
    right = merge_sort(arr[mid:])
    return merge(left, right)           # Conquer & combine

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

**Quick Sort:**
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[0]
    less = [x for x in arr[1:] if x <= pivot]
    greater = [x for x in arr[1:] if x > pivot]
    return quick_sort(less) + [pivot] + quick_sort(greater)
```

---

### 4️⃣ Visualization

**Merge Sort Tree:**
```
              [3,1,4,1,5,9,2,6]
             /                \
        [3,1,4,1]          [5,9,2,6]
        /      \            /      \
      [3,1]   [4,1]      [5,9]   [2,6]
      / \      / \        / \      / \
    [3][1]  [4][1]    [5][9]  [2][6]
      |      |        |      |
    [1,3]  [1,4]    [5,9]  [2,6]
       \      /        \      /
      [1,1,3,4]      [2,5,6,9]
           \            /
        [1,1,2,3,4,5,6,9]

Levels: log₂(8) = 3
Work per level: 8
Total: 8 × 3 = 24 = O(n log n)
```

**Quick Sort Partitioning:**
```
[3,1,4,1,5,9,2,6]  pivot=3
  ↓
less=[1,2,1], pivot=3, greater=[4,5,9,6]
  ↓ recurse less
less=[], pivot=1, greater=[2,1]
  ↓ recurse greater
less=[1], pivot=2, greater=[]
  ↓ done
Result: [1] + [1,2] + [3] + ...
```

---

### 5️⃣ Critical Analysis

| Sort | Best | Average | Worst | Space | Stable |
|------|------|---------|-------|-------|--------|
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | No |

**Key Differences:**
- **Merge:** Guaranteed O(n log n), needs extra space
- **Quick:** Average O(n log n), O(1) extra, worst case bad

**When Quick is Worse:**
```
Pivot selection poor:
[1,2,3,4,5,6,7,8] with pivot=1
  less=[], greater=[2,3,4,5,6,7,8]
  pivot=2
    less=[], greater=[3,4,5,6,7,8]
    ...
O(n²) comparisons (each level divides unequally)
```

**Master Theorem:**
```
T(n) = 2·T(n/2) + n
a=2, b=2, d=1, log_2(2)=1
d=log_b(a), so T(n) = Θ(n log n)
```

---

### 6️⃣ Real Systems

**Merge Sort Used For:**
- External sorting (disk-based, large data)
- Stable sorting requirements
- Predictable O(n log n) guarantee

**Quick Sort Used For:**
- In-memory sorting (default in most languages)
- Cache-friendly (in-place operations)
- Average case beats merge sort (less data movement)

**Hybrid Approaches:**
- **Timsort (Python):** Merge+Insertion for real-world data
- **Introsort (C++):** Quick sort, switch to heap if bad

---

### 7️⃣ Connections

**Builds on:** Day 1 (elementary sorts), Week 1 (complexity)

**Enables:** Search algorithms, data structure operations

---

### 8️⃣ Mathematics

**Merge Sort Recurrence:**
T(n) = 2·T(n/2) + n = O(n log n)

**Quick Sort Average:**
T(n) = 2·T(n/2) + n = O(n log n)

**Quick Sort Worst:**
T(n) = T(n-1) + n = O(n²)

---

### 9️⃣ Design Intuition

**Use Merge Sort:**
- Need guaranteed O(n log n)
- External sorting
- Stable required
- Memory available

**Use Quick Sort:**
- In-memory, space limited
- Average case optimal
- Cache matters
- Production code (most languages)

---

### 🔟 Knowledge Check

1. Why is merge sort guaranteed O(n log n)?
2. Why can quick sort be O(n²)?
3. How many levels in merge sort tree for n=1000?
4. Derive T(n) = 2·T(n/2) + n using master theorem
5. Why does quick sort have better space than merge?
6. When would you use merge over quick?
7. How does pivot selection affect quick sort?

### 1️⃣1️⃣ Hooks

**One-liner:** "Merge sort divides and merges (O(n log n) guaranteed), quick sort partitions (O(n log n) average)."

---

## PART 2: QUICK SUMMARY

**Merge Sort:**
- Divide array in half recursively
- Merge sorted halves
- Always O(n log n), needs O(n) extra space
- Stable sort

**Quick Sort:**
- Pick pivot, partition around it
- Recursively sort parts
- Average O(n log n), worst O(n²)
- In-place, not stable

**Choose:**
- Need guarantee: Merge
- Space critical: Quick
- Production: Quick (usually)
- External data: Merge

---

## PART 3: QUESTIONS & ANSWERS

**Q1:** Merge sort on [5,4,3,2,1]?
**A:** Always divides log₂(5)≈3 levels, 5 comparisons per level. O(5×3)=O(n log n).

**Q2:** Quick sort worst case pivot selection?
**A:** Always pick smallest/largest. Creates unbalanced tree: n+(n-1)+...+1=O(n²).

**Q3:** Why is merge sort stable but quick not?
**A:** Merge preserves relative order (takes from left/right carefully). Quick's partitioning breaks order.

**Q4:** Space: quick vs merge?
**A:** Quick: O(log n) stack frames (recursion depth). Merge: O(n) for merge arrays.

**Q5:** How to fix quick sort worst case?
**A:** Randomized pivot selection or 3-way partition. Makes worst case unlikely.

**Q6:** Merge sort on disk?
**A:** Load chunks, sort in memory, merge results back. Perfect for external sorting.

**Q7:** Why do most languages use quick?
**A:** Average O(n log n), O(1) space, cache-friendly. Only need random pivot for safety.

---

## PART 4: README

**90-Minute Study:**
1. Why (15 min): Understand need for O(n log n)
2. What (15 min): Two approaches mentally
3. How (15 min): Trace merge and partition
4. Visualization (15 min): See divide-and-conquer
5. Analysis (10 min): Master theorem

**Key Skill:** Understand why these are O(n log n)

---

**Status:** ✅ Day 2 Complete | **Next:** Day 3 - Hashing Fundamentals

