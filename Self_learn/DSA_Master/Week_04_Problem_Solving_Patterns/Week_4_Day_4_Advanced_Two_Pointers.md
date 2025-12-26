# Week 4 Day 4: Advanced Two Pointers - Multi-Target Patterns

## 🗓 Metadata
**Topic:** Advanced Two Pointers Patterns  
**Week:** Week 4  
**Day:** Day 4 of 5  
**Category:** Array Manipulation  
**Difficulty:** 🟡 Medium / 🔴 Hard  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

**Three Sum Problem: Find all unique triplets that sum to target.**

```
Array: [-1, 0, 1, 2, -1, -4]
Target: 0
Answer: [[-1, -1, 2], [-1, 0, 1]]
```

**Naive approach (O(n³)):**
```
for i in range(n):
    for j in range(i+1, n):
        for k in range(j+1, n):
            if arr[i] + arr[j] + arr[k] == target:
                add to result
```

**Better approach (O(n²)) using two pointers:**
```
Sort array first: O(n log n)

for each i:
    Use two pointers on rest:
    left = i+1, right = n-1
    while left < right:
        sum = arr[i] + arr[left] + arr[right]
        if sum == target:
            add triplet
            left += 1, right -= 1
        elif sum < target:
            left += 1
        else:
            right -= 1
```

### Why This Matters

**Advanced two pointers:**
1. **Extends from pairs to triples/quads**
2. **Handles multiple targets simultaneously**
3. **Combines sorting + two pointers efficiency**
4. **Handles duplicates in result set**

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy: Locking onto Multiple Targets

**Imagine three laser pointers on a wall:**

```
Wall (sorted array):
[-4, -1, -1, 0, 1, 2]
  i   j           r

Pointer i: Fixed on first element (-4)
Pointers j, r: Hunt for complement to sum to 0

3Sum = arr[i] + arr[j] + arr[r]
     = -4 + (-1) + 2 = -3
-3 < 0 → Need larger sum → j moves right

Once i is fixed, two-pointers find two numbers summing to (target - arr[i])
This reduces 3Sum to multiple 2Sum problems!
```

**Key insight:** Nested approach: fix one, two-pointers on rest.

### Mental Model: Layering Constraints

```
2Sum (sorted): Two pointers from ends
               Reduce O(n²) to O(n)

3Sum (sorted): Fix one element (n iterations)
               Two pointers on rest (n per iteration)
               Total: O(n²) with two pointers
               vs O(n³) brute force

4Sum (sorted): Fix two elements (n² iterations)
               Two pointers on rest (n per iteration)
               Total: O(n³) with two pointers
               vs O(n⁴) brute force
```

---

## 3️⃣ The How — Mechanical Walkthrough

### 3Sum Pattern

```python
def three_sum(arr, target=0):
    arr.sort()
    result = []
    n = len(arr)
    
    for i in range(n - 2):
        # Skip duplicate first elements
        if i > 0 and arr[i] == arr[i-1]:
            continue
        
        # Two sum on rest
        left = i + 1
        right = n - 1
        
        while left < right:
            current_sum = arr[i] + arr[left] + arr[right]
            
            if current_sum == target:
                result.append([arr[i], arr[left], arr[right]])
                
                # Skip duplicates
                while left < right and arr[left] == arr[left + 1]:
                    left += 1
                while left < right and arr[right] == arr[right - 1]:
                    right -= 1
                
                left += 1
                right -= 1
            elif current_sum < target:
                left += 1
            else:
                right -= 1
    
    return result

# Trace
arr = [-1, 0, 1, 2, -1, -4]
sorted: [-4, -1, -1, 0, 1, 2]

i=0 (arr[0]=-4):
  Need two sum = 4
  left=1 (-1), right=5 (2): -1+2=1 < 4 → left++
  left=2 (-1), right=5 (2): -1+2=1 < 4 → left++
  left=3 (0), right=5 (2): 0+2=2 < 4 → left++
  left=4 (1), right=5 (2): 1+2=3 < 4 → left++
  left=5=right, exit

i=1 (arr[1]=-1):
  Need two sum = 1
  left=2 (-1), right=5 (2): -1+2=1 == 1 ✓
  Add [-1, -1, 2]
  Skip duplicates and move pointers
  left=4 (1), right=4, exit

i=2 (arr[2]=-1): Skip (duplicate of previous i)

i=3 (arr[3]=0):
  Need two sum = 0
  left=4 (1), right=5 (2): 1+2=3 > 0 → right--
  left=4 (1), right=4, exit

Result: [[-1, -1, 2], [-1, 0, 1]]
```

### 4Sum Pattern

```python
def four_sum(arr, target):
    arr.sort()
    result = []
    n = len(arr)
    
    for i in range(n - 3):
        if i > 0 and arr[i] == arr[i-1]:
            continue
        
        for j in range(i + 1, n - 2):
            if j > i + 1 and arr[j] == arr[j-1]:
                continue
            
            # Two pointers on rest
            left = j + 1
            right = n - 1
            
            while left < right:
                current_sum = arr[i] + arr[j] + arr[left] + arr[right]
                
                if current_sum == target:
                    result.append([arr[i], arr[j], arr[left], arr[right]])
                    
                    # Skip duplicates
                    while left < right and arr[left] == arr[left + 1]:
                        left += 1
                    while left < right and arr[right] == arr[right - 1]:
                        right -= 1
                    
                    left += 1
                    right -= 1
                elif current_sum < target:
                    left += 1
                else:
                    right -= 1
    
    return result
```

### Duplicate Handling

**Critical for correctness:** Skip duplicates to avoid returning same triplet multiple times

```python
# Skip duplicate at current position
if i > 0 and arr[i] == arr[i-1]:
    continue

# When moving pointers, skip duplicates
while left < right and arr[left] == arr[left + 1]:
    left += 1
while left < right and arr[right] == arr[right - 1]:
    right -= 1
```

---

## 4️⃣ Visualization — Examples & Trace

### Visual Trace: 3Sum

```
Sorted: [-4, -1, -1, 0, 1, 2]
Target: 0

i=0 (fix -4), need sum = 4:
         L                 R
[-4, -1, -1, 0, 1, 2]
-1 + 2 = 1 < 4 → L moves

         L           R
[-4, -1, -1, 0, 1, 2]
-1 + 2 = 1 < 4 → L moves

            L        R
[-4, -1, -1, 0, 1, 2]
0 + 2 = 2 < 4 → L moves

               L     R
[-4, -1, -1, 0, 1, 2]
1 + 2 = 3 < 4 → L moves

               L = R (stop)

i=1 (fix -1), need sum = 1:
      L                  R
[-4, -1, -1, 0, 1, 2]
-1 + 2 = 1 == 1 ✓ Found!
Add [-1, -1, 2]

Skip duplicates and move:
            L    R
[-4, -1, -1, 0, 1, 2]
0 + 1 = 1 == 1 ✓ Found!
Add [-1, 0, 1]

            L = R (stop)

Result: [[-1, -1, 2], [-1, 0, 1]]
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Time Complexity

**3Sum:** O(n²)
```
Sorting: O(n log n)
Outer loop: n iterations
Inner two pointers: n iterations each
Total: O(n log n + n²) = O(n²)
```

**4Sum:** O(n³)
```
Sorting: O(n log n)
Two nested loops: O(n²) iterations
Inner two pointers: O(n) per iteration
Total: O(n log n + n³) = O(n³)
```

**kSum generalization:** O(n^(k-1))

### Duplicate Handling is Critical

**Without duplicate handling:**
```
arr = [-1, -1, 2]
Would return same triplet multiple times
```

**With duplicate handling:**
```
Skip arr[i] if it equals arr[i-1]
Skip arr[left] if it equals arr[left+1]
Skip arr[right] if it equals arr[right-1]
Guarantees unique results
```

### Edge Cases

**Edge Case 1: All same elements**
```
arr = [0, 0, 0, 0]
target = 0

All combinations form [0, 0, 0]
Return: [[0, 0, 0]] (one time)
Duplicate handling ensures this
```

**Edge Case 2: Empty or too small**
```
arr = [1, 2] for 3Sum
Can't form triplet → Return []
```

**Edge Case 3: Negative numbers**
```
Works same way, sorting handles negatives
```

---

## 6️⃣ Real System Integration

### Database Queries

**Find all entries matching multiple criteria:**
```
Find customers with balance, age, score summing to threshold
Similar pattern: fix one, search rest
```

---

## 7️⃣ Concept Crossovers

### Builds On

**Two Pointers (Day 1):** Foundation for nested two pointers

**Sorting (Week 3):** Essential preprocessing

### Builds Toward

**Integration (Day 5):** Combine with other techniques

---

## 8️⃣ Mathematical & Theoretical Perspective

### Proof: 3Sum Correctness with Two Pointers

```
When two pointers are used on sorted array:
- If sum too small, left moves right (increases)
- If sum too large, right moves left (decreases)

This exploration pattern with fixed i finds all valid pairs
since for each pair (left, right), we know:
- All elements left of left are smaller
- All elements right of right are larger

So we're guaranteed to find pair if it exists for this i.
```

---

## 9️⃣ Algorithmic Design Intuition

### When to Use Advanced Two Pointers

```
Is array sorted or sortable?
  ├─ YES → Consider multiple pointers
  ├─ NO  → Sort first

Need multiple elements summing to target?
  ├─ YES → Nested two pointers ✓
  ├─ NO  → Single two pointers
  
Need unique results?
  ├─ YES → Handle duplicates carefully
  ├─ NO  → Simpler code
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Why can't we use 3Sum approach without sorting?**

Think: What would happen if array is unsorted?

**Question 2: How does duplicate handling prevent returning same triplet?**

Think: What if we didn't skip duplicates?

**Question 3: Why is 4Sum O(n³) not O(n²)?**

Think: How many nested fixed positions? How many two-pointer iterations?

**Question 4: Could you solve 3Sum with hash tables instead?**

Think: Time vs space trade-off.

**Question 5: How would you extend to kSum (arbitrary k)?**

Think: Pattern for recursion/nesting.

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Advanced two pointers: Fix k-2 elements, apply two pointers on rest. Requires sorting and duplicate handling. Time: O(n^(k-1)).**

---

## 📚 Supplementary Data

| Problem | Approach | Time | Space |
|---------|----------|------|-------|
| 3Sum | Sort + nested two pointers | O(n²) | O(1) |
| 4Sum | Sort + nested two pointers | O(n³) | O(1) |
| kSum | Recursive with two pointers | O(n^(k-1)) | O(1) |

---

## 🔗 External References

1. **LeetCode:**
   - 3Sum: https://leetcode.com/problems/3sum/
   - 4Sum: https://leetcode.com/problems/4sum/
   - 3Sum Closest: https://leetcode.com/problems/3sum-closest/

---

**Word Count:** ~2,000 words  
**Reading Time:** 60-70 minutes  
**Status:** ✅ Complete

