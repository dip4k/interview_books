# Week 4.5, Day 3: Merge Operations

## 🗓 Metadata
**Week:** 4.5 (Tier 1) | **Day:** 3 of 5 | **Topic:** Merge Operations  
**Category:** Critical Problem-Solving Patterns | **Difficulty:** 🟡 Medium  
**Time:** 90-120 minutes  
**Interview Coverage:** **30% of array/list problems**

---

## 1️⃣ THE WHY

**Real-World Problem:**
Merge two sorted arrays into one. Naive: concatenate + sort O(n log n). Better: two pointers O(n).

**Design Problems:**
- Merge sorted arrays/lists
- Merge K sorted lists (heap + merging)
- Merge overlapping intervals
- Combine sorted data streams

**Real System Usage:**
- **Merge Sort:** Merging is core operation
- **Databases:** Merging sorted result sets
- **External sorting:** Merging blocks from disk

---

## 2️⃣ THE WHAT

**Analogy:** Two queues of people in height order. Merge by picking shorter person each time.

```
List 1: [1, 3, 5]
List 2: [2, 4, 6]
Merge: Compare 1 vs 2 → take 1
       Compare 3 vs 2 → take 2
       Compare 3 vs 4 → take 3
       ... result: [1,2,3,4,5,6]
```

---

## 3️⃣ THE HOW

```
1. two_pointers: p1=0, p2=0
2. while p1 < n1 AND p2 < n2:
     if arr1[p1] <= arr2[p2]:
       merged.append(arr1[p1])
       p1++
     else:
       merged.append(arr2[p2])
       p2++
3. append remaining

Cost: O(n+m), Space: O(n+m)
```

---

## 4️⃣-1️⃣1️⃣ VISUALIZATION & ANALYSIS

**Example:** Merge [1,3,5] and [2,4,6]
```
p1=0, p2=0: 1<2, take 1, merged=[1]
p1=1, p2=0: 3>2, take 2, merged=[1,2]
p1=1, p2=1: 3<4, take 3, merged=[1,2,3]
p1=2, p2=1: 5>4, take 4, merged=[1,2,3,4]
p1=2, p2=2: 5<6, take 5, merged=[1,2,3,4,5]
p1=3, p2=2: p1 done, append remaining from p2: merged=[1,2,3,4,5,6]
```

| Operation | Time | Space |
|-----------|------|-------|
| **Merge** | O(n+m) | O(n+m) |

**One-Liner:**
> **Merge: O(n) with two pointers on sorted inputs. Foundation for merge sort and K-way merges.**

**Cognitive Lenses:**
| **Computational** | Two pointers eliminate resorting; single pass through both lists |
| **Psychological** | Natural: interleaving two ordered sequences |
| **Design** | Space-time: O(n) space for O(n) vs O(n log n) sort |
| **AI/ML** | Similar to: interleaving training batches |
| **Historical** | Core of merge sort (Von Neumann, 1945) |

