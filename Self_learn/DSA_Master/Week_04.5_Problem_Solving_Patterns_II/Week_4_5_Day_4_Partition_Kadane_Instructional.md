# Week 4.5, Day 4A: Partition

## 🗓 Metadata
**Week:** 4.5 (Tier 1) | **Day:** 4A of 5 | **Topic:** Partition  
**Category:** Critical Problem-Solving Patterns | **Difficulty:** 🟡 Medium  
**Time:** 45-60 minutes  
**Interview Coverage:** **15% of array problems**

---

## 1️⃣ THE WHY

**Real-World Problem:**
Move all zeros to end: [1,0,2,0,3] → [1,2,3,0,0]. In-place, O(1) space.

**Design Problems:**
- Move zeros, ones, twos (Dutch National Flag)
- Partition for quicksort
- Segregate even and odd numbers

**Real System Usage:**
- **Quicksort:** Partitioning is core operation
- **In-place algorithms:** Space optimization

---

## 2️⃣ THE WHAT

**Analogy:** Separating laundry by color in-place. Light clothes go left, dark go right.

---

## 3️⃣ THE HOW

**Two Pointers: Partition with pivot**
```
1. left = 0, right = n-1
2. while left < right:
     while arr[left] < pivot: left++
     while arr[right] >= pivot: right--
     if left < right:
       swap(arr[left], arr[right])
3. return left (partition position)

Cost: O(n), Space: O(1) in-place
```

---

## 4️⃣-1️⃣1️⃣ ANALYSIS

| Operation | Time | Space |
|-----------|------|-------|
| **Partition** | O(n) | O(1) |

**One-Liner:**
> **Partition: O(n) in-place by moving elements smaller than pivot left, larger right.**

---

# Week 4.5, Day 4B: Kadane's Algorithm

## 🗓 Metadata
**Week:** 4.5 (Tier 1) | **Day:** 4B of 5 | **Topic:** Kadane's Algorithm  
**Category:** Critical Problem-Solving Patterns | **Difficulty:** 🟡 Medium  
**Time:** 45-60 minutes  
**Interview Coverage:** **10% of DP/array problems**

---

## 1️⃣ THE WHY

**Real-World Problem:**
Array: [-2,1,-3,4,-1,2,1,-5,4]. Find maximum sum subarray. Naive: O(n³). Better: Kadane O(n).

**Design Problems:**
- Maximum subarray sum
- Maximum product subarray
- Maximum subarray length with constraint

**Real System Usage:**
- **Stock trading:** Max profit buy-sell
- **Signal processing:** Finding peak signal

---

## 2️⃣ THE WHAT

**Core Idea:** At each position, track max sum ending here. If previous + current > current alone, extend. Otherwise, start fresh.

```
Array: [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Max_ending_here: -2, 1, -2, 4, 3, 5, 6, 1, 5
Max_so_far: -2, 1, 1, 4, 4, 5, 6, 6, 6
```

---

## 3️⃣ THE HOW

```
1. max_current = arr[0]
2. max_global = arr[0]
3. for i from 1 to n-1:
     max_current = max(arr[i], max_current + arr[i])
     max_global = max(max_global, max_current)
4. return max_global

Cost: O(n), Space: O(1)
```

---

## 4️⃣-1️⃣1️⃣ ANALYSIS

| Operation | Time | Space |
|-----------|------|-------|
| **Kadane** | O(n) | O(1) |

**One-Liner:**
> **Kadane: O(n) DP by tracking max sum ending at each position. Classic interview pattern.**

**Cognitive Lenses:**
| **Computational** | Single pass; each element processed once |
| **Psychological** | Greedy intuition: reset when sum goes negative |
| **Design** | Space optimization: O(1) vs O(n) DP table |
| **AI/ML** | Similar to: backpropagation (cumulative gradients) |
| **Historical** | Jay Kadane, 1984. Elegant DP pattern. |

