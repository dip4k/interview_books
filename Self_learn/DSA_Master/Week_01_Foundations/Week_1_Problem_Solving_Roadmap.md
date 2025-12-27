# Week 1: Foundations - Problem-Solving Roadmap

**Week:** 1 | **Focus:** Strategic approach to Week 1 problems  
**Date:** December 27, 2025

---

## 1️⃣ Overall Problem-Solving Framework

### **The Five-Step Process**

**Step 1: Understand the Problem**
- What is given? (Input)
- What are we solving for? (Output)
- Are there constraints? (Time, space, correctness)

**Step 2: Identify the Complexity Class**
- Is it about memory (RAM model)?
- Is it about speed (Big-O)?
- Is it about recursion (recurrence relations)?

**Step 3: Choose the Approach**
- RAM model problems → analyze memory layout
- Big-O problems → count operations
- Recursion problems → write recurrence, solve
- Space problems → measure allocations

**Step 4: Implement the Solution**
- Code the algorithm
- Trace with small example
- Verify against constraints

**Step 5: Verify**
- Does output match expectation?
- Is complexity acceptable?
- Did you handle edge cases?

---

## 2️⃣ Day-Specific Problem-Solving Roadmap

### **Day 1 (RAM Model): Memory & Pointers Problems**

**Problem Type 1: Understanding Memory Layout**
```
Given: Memory layout with addresses and values
Find: Address of variable, pointer dereference, pointer arithmetic

Strategy:
1. Draw the memory layout
2. Mark each address
3. Identify pointers (store addresses)
4. Trace dereferences
5. Calculate pointer arithmetic
```

**Problem Type 2: Cache Locality**
```
Given: Two access patterns
Find: Which is faster, why

Strategy:
1. Identify sequential vs random access
2. Consider cache line size (~64 bytes)
3. Sequential = cache hit, random = cache miss
4. Sequential is ~100x faster
5. Recommend sequential access
```

**Problem Type 3: Stack vs Heap**
```
Given: Memory allocations
Find: Which use stack, which use heap

Strategy:
1. Local variables, function args → stack
2. malloc/new → heap
3. Recursion → stack (function frames)
4. Determine if stack will overflow (depth > 100K)
```

### **Day 2 (Big-O): Complexity Analysis Problems**

**Problem Type 1: Count Operations**
```
Given: Code snippet
Find: Time complexity

Strategy:
1. Identify loops (for, while, do-while)
2. Count iterations of each loop
3. Count work per iteration (usually O(1))
4. Multiply iterations × work
5. Keep leading term, drop constants
6. Result = O(...)

Example:
for (i=0; i<n; i++)              // n iterations
    for (j=i; j<n; j++)          // n-i iterations
        process();               // O(1) work
Total: n + (n-1) + ... + 1 = n(n+1)/2 = O(n²)
```

**Problem Type 2: Derive Recurrence Relation**
```
Given: Recursive function
Find: Time complexity

Strategy:
1. Write T(n) in terms of T(k) for k < n
2. Identify recursive calls and their sizes
3. Add the non-recursive work
4. Solve recurrence (expansion, Master Theorem)

Example:
int fib(int n) {
    if (n <= 1) return n;                    // O(1)
    return fib(n-1) + fib(n-2);
}
Recurrence: T(n) = T(n-1) + T(n-2) + O(1)
Solution: T(n) = O(2^n)
```

**Problem Type 3: Compare Algorithms**
```
Given: Two or more algorithms
Find: Which is better for what input size

Strategy:
1. Derive complexity for each
2. For different input sizes, compare
   - n=100: Calculate actual operations
   - n=1,000: Compare again
   - n=1,000,000: Compare at scale
3. Consider practical factors
4. Recommend based on input size
```

### **Day 3 (Space Complexity): Memory Analysis Problems**

**Problem Type 1: Analyze Space Usage**
```
Given: Algorithm or code
Find: Space complexity

Strategy:
1. Identify temporary arrays/allocations
2. Identify recursion depth
3. Count space = input + temporary + recursion
4. Keep largest term

Example:
int merge(int arr[], int n) {
    int* temp = malloc(n * sizeof(int));  // O(n) space
    // process
}
Space: O(n) (temp array)
```

**Problem Type 2: Stack Overflow Risk**
```
Given: Recursive function, input size
Find: Will it stack overflow?

Strategy:
1. Determine recursion depth D
2. Stack limit ≈ 100,000-1,000,000 frames
3. If D > limit, stack overflow occurs
4. Recommend: Convert to iteration or tail-recursion

Example:
factorial(1,000,000) → depth 1M → stack overflow!
Solution: Use tail-recursion or iteration
```

**Problem Type 3: Space-Time Trade-Off**
```
Given: Two algorithms, different space/time
Find: Which to choose

Strategy:
1. Check memory constraint (available RAM)
2. Check time constraint (must finish in X seconds)
3. If memory scarce: choose low-space algorithm
4. If time scarce: choose low-time algorithm
5. If both constrained: compromise or optimize

Example:
A: O(n) time, O(1) space
B: O(log n) time, O(n) space
If memory < 4GB and n=1B integers: choose A
If memory abundant and time critical: choose B
```

### **Day 4 (Recursion I): Basic Recursion Problems**

**Problem Type 1: Write Recursive Solution**
```
Given: Problem description
Find: Recursive code

Strategy:
1. Identify base case (simplest instance)
2. Identify recursive case (n in terms of n-1)
3. Ensure progress toward base case
4. Combine results (how to build n from n-1)
5. Code it up

Example:
Sum array recursively:
- Base: sum([], 0) = 0
- Recursive: sum([...], n) = arr[n-1] + sum([...], n-1)
- Code it
```

**Problem Type 2: Trace Recursion by Hand**
```
Given: Recursive function, input
Find: Output (trace execution)

Strategy:
1. Draw call tree
2. Expand until base cases
3. Unwind, computing values bottom-up
4. Verify with code

Example:
fib(3):
  fib(2) + fib(1)
  = (fib(1) + fib(0)) + fib(1)
  = (1 + 0) + 1
  = 2
```

**Problem Type 3: Analyze Recursive Complexity**
```
Given: Recursive function
Find: Time and space complexity

Strategy:
1. Write recurrence T(n) = ...
2. Solve for time complexity
3. Identify recursion depth = space complexity
4. Verify with examples

Example:
factorial(n): T(n) = T(n-1) + O(1)
Time: O(n)
Space (call stack): O(n) (depth n)
```

### **Day 5 (Recursion II): Advanced Recursion Problems**

**Problem Type 1: Optimize with Tail Recursion**
```
Given: Non-tail-recursive function
Find: Tail-recursive equivalent

Strategy:
1. Identify where computation happens (before/after return)
2. If after return: move to accumulator parameter
3. Make recursive call last operation
4. Code tail-recursive version

Example:
Non-tail: factorial(n) = n * factorial(n-1)
Tail: factorialTail(n, acc) = factorialTail(n-1, n*acc)
```

**Problem Type 2: Apply Memoization**
```
Given: Slow recursive function (exponential time)
Find: Memoized version

Strategy:
1. Add a cache (map or array)
2. Check cache before computing
3. Store result in cache before returning
4. Verify time improvement

Example:
fib(40) naive: 2^40 operations
fib(40) memo: 40 operations
Add hash map, check/store → done
```

**Problem Type 3: Recognize Mutual Recursion**
```
Given: Multiple functions calling each other
Find: Structure and base cases

Strategy:
1. Identify which functions call which
2. Find base cases that break cycles
3. Analyze complexity (same as single recursion)
4. Add memoization if needed

Example:
isEven(n) calls isOdd(n-1)
isOdd(n) calls isEven(n-1)
Base: isEven(0)=true, isOdd(0)=false
```

---

## 3️⃣ Decision Tree: Choosing the Right Approach

```
START: "I have a problem to solve"
  ↓
Is it about MEMORY LAYOUT or POINTERS?
  → YES: Go to "RAM Model Approach" (Section 2, Day 1)
  → NO: Continue
  ↓
Is it about COUNTING OPERATIONS or GROWTH RATE?
  → YES: Go to "Big-O Approach" (Section 2, Day 2)
  → NO: Continue
  ↓
Is it about MEMORY USAGE (SPACE)?
  → YES: Go to "Space Complexity Approach" (Section 2, Day 3)
  → NO: Continue
  ↓
Is the function CALLING ITSELF?
  → YES: Go to "Recursion Approach" (Section 2, Days 4-5)
  → NO: Continue (likely a simple loop problem → Big-O)
  ↓
Still not sure? Ask:
  1. Is it fundamentally about performance? → Big-O
  2. Is it fundamentally about memory? → Space
  3. Is it fundamentally about structure? → Recursion
  4. Is it fundamentally about data layout? → RAM Model
```

---

## 4️⃣ Common Pitfalls & Recovery

### **Pitfall 1: Forgetting Constants**
**Problem:** "This is O(n) because it's linear"
**Solution:** Actually count: 100n operations ≠ n operations (100x difference!)
**Recovery:** Count constants initially, drop them only when comparing at scale

### **Pitfall 2: Mixing Up Best/Avg/Worst**
**Problem:** "Binary search is O(1) best case" (right) but forgetting worst case O(log n)
**Solution:** Always state all three
**Recovery:** Analyze: best (when found immediately), average (random), worst (not found)

### **Pitfall 3: Not Accounting for Recursion Depth**
**Problem:** "Recursion is O(1) space" (WRONG)
**Solution:** Recursion depth → call stack → O(depth) space
**Recovery:** Always add recursion depth to space complexity

### **Pitfall 4: Assuming Memoization Always Helps**
**Problem:** Applying memo to function with no repeated calls (no speedup)
**Solution:** Check if subproblems repeat
**Recovery:** Fibonacci repeats (memo helps). Tree traversal doesn't (memo wastes space)

### **Pitfall 5: Getting Lost in Recurrence Relations**
**Problem:** "I can't solve T(n) = T(n/2) + n"
**Solution:** Use Master Theorem or expand by hand
**Recovery:** 
- Simple: T(n) = T(n-1) + O(1) = O(n) (n levels × O(1) = O(n))
- Binary search: T(n) = T(n/2) + O(1) = O(log n) (log n levels)
- Merge sort: T(n) = 2T(n/2) + n = O(n log n) (Master Theorem)

---

## 5️⃣ Problem-Solving Template

**Use this template for any Week 1 problem:**

```
PROBLEM: [Problem name/description]

STEP 1: UNDERSTAND
- Input: [What are we given?]
- Output: [What are we computing?]
- Constraints: [Time/space limits?]

STEP 2: IDENTIFY CATEGORY
- [ ] RAM Model (memory, pointers)
- [ ] Big-O (complexity analysis)
- [ ] Space (memory usage)
- [ ] Recursion (recursive solution)

STEP 3: ANALYZE
- [Approach-specific analysis from Section 2]

STEP 4: IMPLEMENT
- [Code solution]
- [Trace with example input]

STEP 5: VERIFY
- [Check against constraints]
- [Test edge cases]
- [Confirm complexity]

RESULT: [Time: O(...), Space: O(...)]
```

---

## 6️⃣ Example: Complete Problem Walkthrough

**PROBLEM:** "Find sum of array recursively. Analyze complexity."

**STEP 1: UNDERSTAND**
- Input: Array of integers, size n
- Output: Sum of all elements
- Constraints: None specified (use recursion)

**STEP 2: IDENTIFY CATEGORY**
- Recursion (Days 4-5)

**STEP 3: ANALYZE**
- Base case: Empty array → sum = 0
- Recursive case: sum(arr[0..n-1]) = arr[n-1] + sum(arr[0..n-2])
- Recurrence: T(n) = T(n-1) + O(1)
- Solution: T(n) = O(n) time, O(n) space (call stack)

**STEP 4: IMPLEMENT**
```cpp
int sum(int arr[], int n) {
    if (n == 0) return 0;                    // Base case
    return arr[n-1] + sum(arr, n-1);         // Recursive case
}
```

Trace: sum([1,2,3], 3)
- = 3 + sum([1,2,3], 2)
- = 3 + (2 + sum([1,2,3], 1))
- = 3 + (2 + (1 + sum([1,2,3], 0)))
- = 3 + (2 + (1 + 0))
- = 6 ✓

**STEP 5: VERIFY**
- ✓ Base case (n=0) returns 0
- ✓ Recursive case progresses toward base case
- ✓ Trace matches expected output
- ✓ No infinite recursion
- ✓ Time O(n) is acceptable

**RESULT:** 
- Time: O(n)
- Space: O(n) (recursion depth)

---

## Summary

**Use this roadmap to:**
1. **Understand** Week 1 problem types
2. **Navigate** using the decision tree
3. **Avoid** common pitfalls
4. **Apply** the template systematically
5. **Verify** your solution

**Next:** Move to Week 2 once you can solve all problem types confidently.

