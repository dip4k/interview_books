# Week 1: Foundations - Interview Q&A Reference

**Week:** 1 | **Focus:** 50+ Interview Questions & Answers  
**Date:** December 27, 2025  
**Level:** Easy to Hard

---

## 🎯 RAM Model & Pointers (Day 1) - 12 Q&A Pairs

### **Q1: What is a pointer and how does dereferencing work?**
A: A pointer is a variable that stores a memory address. Dereferencing (*ptr) follows that address to get the value.
```cpp
int x = 5;
int* ptr = &x;      // ptr stores address of x (~1000)
int y = *ptr;       // y = 5 (dereference: go to address, get value)
```
Key: & gets address, * goes to address.

### **Q2: Why does array access beat linked list access?**
A: Arrays are contiguous; each element is next to the previous. CPU caches fetch nearby memory efficiently. Linked lists scatter elements; chasing pointers causes cache misses.
- Array access: O(1) with cache hit, ~1ns
- List access: O(1) algorithmically, but ~100ns due to cache misses

### **Q3: Explain pointer arithmetic on arrays.**
A: ptr+i adds i*sizeof(element_type) to ptr, not just i.
```cpp
int arr[10];
int* p = &arr[0];    // p = address 1000
int* q = p + 1;      // q = 1004 (not 1001! adds 4 bytes)
*(p+3) == arr[3];    // equivalent forms
```

### **Q4: What is the call stack and how do function calls use it?**
A: The call stack is a data structure that stores function frames. Each call:
1. Allocates a new frame (local variables, return address)
2. Pushes onto stack
3. Returns and pops frame off

Deep recursion → tall stack → overflow.

### **Q5: What is the difference between stack and heap?**
A:
- **Stack:** Small, fast, automatic cleanup, limited (typically 1-8MB)
- **Heap:** Large, slower, manual cleanup (or garbage collection), expensive

Recursion uses stack; malloc/new use heap.

### **Q6: What does "dereferencing a null pointer" do?**
A: Crashes immediately (segmentation fault). Dereferencing follows the address; nullptr is address 0, which is invalid.
```cpp
int* ptr = nullptr;
int x = *ptr;  // CRASH!
```

### **Q7: Can you pass a pointer to a function? What's a "pointer to pointer"?**
A: Yes. int** is a pointer to a pointer (address of a pointer).
```cpp
void modify(int** pptr) {
    **pptr = 10;  // Dereference twice
}
int x = 5;
int* ptr = &x;
modify(&ptr);  // Pass address of the pointer
```

### **Q8: What is a "dangling pointer"?**
A: A pointer to memory that's been freed. Dereferencing it is undefined behavior.
```cpp
int* ptr;
{
    int x = 5;
    ptr = &x;  // ptr points to x
}
// x goes out of scope
int y = *ptr;  // UNDEFINED! ptr is dangling
```

### **Q9: Explain "pointer to array" vs "array of pointers".**
A:
- int* arr[10]   → array of 10 pointers to int
- int (*ptr)[10] → pointer to array of 10 ints

Different memory layouts and usage.

### **Q10: Why does cache locality matter?**
A: CPU caches store nearby memory. Sequential access hits cache (fast ~1ns). Random access misses cache (slow ~100ns). 100x difference!

For loops, access elements in order (arr[0], arr[1], arr[2]) not randomly.

### **Q11: What is virtual memory?**
A: OS maps virtual addresses (what your program sees) to physical addresses (actual RAM). Uses page tables and pointer indirection. Enables multiple processes to coexist.

### **Q12: Can you declare a pointer to void? What's its use?**
A: Yes. void* is a generic pointer (no type information).
```cpp
void* ptr = malloc(100);  // Can point to any type
int* iptr = (int*)ptr;    // Cast to use
```
Used for generic functions, memory allocation.

---

## 📊 Asymptotic Analysis (Day 2) - 13 Q&A Pairs

### **Q13: What is Big-O notation and why do we use it?**
A: Big-O describes worst-case growth rate, ignoring constants and lower-order terms.
- O(n) = linear (grows with input)
- O(n²) = quadratic (grows faster)
- O(2^n) = exponential (impossibly fast)

Why: Predicts algorithm scalability without running code.

### **Q14: Rank these from fastest to slowest: O(1), O(n), O(n²), O(log n), O(2^n).**
A: O(1) < O(log n) < O(n) < O(n²) < O(2^n)

For n=1,000,000: 1 < 20 < 1M < 10^12 < impossible.

### **Q15: Why do constants not matter in Big-O?**
A: For large n, the leading term dominates. 
- 100n vs n: both O(n), grow at same rate
- 1n vs 0.001n²: for large n, n² dominates

Example: n=1,000,000:
- 100n = 100M operations
- 0.001n² = 10^12 operations
Constants fade; growth rate matters.

### **Q16: What's the difference between Big-O, Big-Omega, Big-Theta?**
A:
- **O (Big-O):** Upper bound (worst case)
- **Ω (Big-Omega):** Lower bound (best case)
- **Θ (Big-Theta):** Tight bound (average case)

Example: Quicksort is O(n²) worst, Ω(n) best, Θ(n log n) average.

### **Q17: How do you count operations to derive Big-O?**
A:
1. Identify loops and recursion
2. Count iterations/calls
3. Count work per iteration
4. Multiply: total = iterations × work
5. Keep leading term, drop constants

Example: Two nested loops of n: n × n = O(n²).

### **Q18: What's the complexity of this?**
```cpp
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
        process();  // O(1)
    }
}
```
A: 
- i=0: n iterations
- i=1: n-1 iterations
- i=2: n-2 iterations
- Total: n + (n-1) + (n-2) + ... + 1 = n(n+1)/2 = O(n²)

### **Q19: What's the complexity of binary search?**
A: O(log n).
Each call halves the search space:
- n → n/2 → n/4 → ... → 1
- Number of halvings = log₂(n)

Recurrence: T(n) = T(n/2) + O(1) = O(log n).

### **Q20: What's the complexity of merge sort?**
A: O(n log n) always (best, average, worst).
- Divide: O(log n) depth
- Merge: O(n) work per level
- Total: log n levels × n work = O(n log n)

Recurrence: T(n) = 2T(n/2) + n = O(n log n) by Master Theorem.

### **Q21: What's the Master Theorem and when do you use it?**
A: Solves recurrences of form T(n) = aT(n/b) + f(n).
```
If f(n) = O(n^(logb(a) - ε)): T(n) = Θ(n^logb(a))
If f(n) = Θ(n^logb(a)):       T(n) = Θ(n^logb(a) log n)
If f(n) = Ω(n^(logb(a) + ε)): T(n) = Θ(f(n))
```
Use when recurrence fits the form.

### **Q22: Is O(2n) the same as O(n)?**
A: Yes. Both are O(n). Constants don't matter.
- 2n operations
- n operations
- 0.5n operations
All are O(n) because growth rate is linear.

### **Q23: Can you have an algorithm with better average case than worst case?**
A: Yes! Quicksort:
- Average: O(n log n)
- Worst: O(n²) (when pivot is always largest/smallest)

Best case vs worst case differ.

### **Q24: What does it mean if an algorithm is O(1) amortized?**
A: Average time per operation is O(1) when amortized over many operations.

Example: Dynamic array push_back:
- Single push: O(1) if no resize, O(n) if resize
- Amortized: O(1) over n pushes because resizes are rare

### **Q25: Why is analyzing algorithms important if CPUs are fast?**
A: Moore's law slowed down. We can't rely on hardware getting faster. Good algorithms beat fast hardware.

Example: O(2^n) on 2030 CPU: still slower than O(n) on 2023 CPU for large inputs.

---

## 💾 Space Complexity (Day 3) - 10 Q&A Pairs

### **Q26: How do you analyze space complexity?**
A: Count extra memory beyond input.
- Recursion depth d = O(d) stack space
- Temporary arrays = O(size)
- Hash tables = O(n) space for n elements

Example: Merge sort allocates O(n) temporary array.

### **Q27: What's the space complexity of recursion depth n?**
A: O(n) because each call frame stays on stack until unwinding.

Example: factorial(100) allocates 100 stack frames = O(100) = O(n).

### **Q28: Can you have O(1) space recursion?**
A: Yes, with tail-call optimization. Tail-recursive function's compiler optimizes to O(1).

Example: factorialTail(n, acc) with tail call in recursion.

But: Python doesn't do tail-call optimization. Check your language.

### **Q29: Merge sort is O(n log n) time but O(n) space. Can you do better?**
A: Merge sort requires O(n) space for merging. In-place sorts like quicksort use O(log n) space (recursion depth).

Trade-off: O(n log n) guaranteed time vs O(n) space, or average O(n log n) and O(log n) space.

### **Q30: What's the difference between stack space and heap space in complexity analysis?**
A:
- **Stack:** Recursion depth, function calls. Limited to ~8MB.
- **Heap:** Dynamic allocations (malloc, new). Larger but slower, costs money.

Recursion → stack (limited); memoization → heap (expensive).

### **Q31: How does memoization affect space complexity?**
A: Memoization caches results, trading space for time.
- Without memo: O(n) space (call stack)
- With memo: O(n) space (cache) + O(n) space (call stack) = O(n) still

But: Avoids recomputation, speeds up time O(2^n) → O(n).

### **Q32: Can you optimize space below O(1)?**
A: No. O(1) is the best (constant space). You still need variables to store input pointers, loop counters, etc.

### **Q33: What causes "stack overflow" and how do you prevent it?**
A: Recursion depth exceeds stack limit (~100,000 calls typical).

Prevention:
1. Convert to iteration
2. Increase stack size (OS-dependent)
3. Use tail-recursion (compiler-dependent)

### **Q34: If you need to sort 1 billion integers, what's the space constraint?**
A: 1 billion integers = 4GB (assuming 4 bytes each).
- O(n) space sorts (merge sort): need extra 4GB (total 8GB). Might not fit.
- O(1) space sorts (quicksort): reuse input array. Fits in 4GB.

Choose based on available memory.

### **Q35: What's "amortized space" and does it exist?**
A: Rare. Most algorithms have consistent space usage. Dynamic arrays have "amortized time" (insertions are O(1) amortized), not space.

Space usually doesn't have amortized analysis.

---

## 🔄 Recursion I (Day 4) - 10 Q&A Pairs

### **Q36: What's the recurrence for factorial(n)?**
A: 
```
T(n) = T(n-1) + O(1)  (one recursive call, O(1) multiplication)
T(1) = O(1)           (base case)

Expanding: T(n) = T(n-1) + 1 = T(n-2) + 1 + 1 = ... = O(n)
```

### **Q37: Can you write a recursive sum of array and trace it?**
A:
```cpp
int sum(int arr[], int n) {
    if (n == 0) return 0;                    // Base case
    return arr[n-1] + sum(arr, n-1);         // Recursive case
}
// sum([1,2,3], 3) = 3 + sum([1,2,3], 2)
//                 = 3 + (2 + sum([1,2,3], 1))
//                 = 3 + (2 + (1 + sum([1,2,3], 0)))
//                 = 3 + (2 + (1 + 0))
//                 = 6
```

### **Q38: What happens without a base case?**
A: Infinite recursion → stack overflow.
```cpp
int bad(int n) {
    return bad(n-1);  // No base case!
}
bad(5) → bad(4) → bad(3) → ... → stack overflow!
```

### **Q39: What's the difference between recursion depth and time complexity?**
A:
- **Depth:** How many calls stack up (height of call tree)
- **Time:** Total number of calls (size of call tree)

Example: Fibonacci
- Depth: O(n) (left branch goes n deep)
- Calls: O(2^n) (total nodes in tree)

### **Q40: Can you solve binary search recursively? What's the complexity?**
A:
```cpp
int binarySearch(int arr[], int left, int right, int target) {
    if (left > right) return -1;             // Not found
    int mid = (left + right) / 2;
    if (arr[mid] == target) return mid;
    if (arr[mid] < target) return binarySearch(arr, mid+1, right, target);
    else return binarySearch(arr, left, mid-1, target);
}
```
Complexity:
```
T(n) = T(n/2) + O(1)  (one recursive call, halving search space)
T(1) = O(1)
Result: T(n) = O(log n)
```

### **Q41: When is recursion better than iteration?**
A: When:
1. **Problem is naturally recursive:** Trees, graphs, divide-and-conquer
2. **Code clarity:** Recursion is simpler than iteration
3. **Depth is small:** No stack overflow risk

Example: Tree traversal is naturally recursive (each node has children).

### **Q42: When should you avoid recursion?**
A: When:
1. **Deep recursion expected:** Depth > 10,000 → stack overflow
2. **Simple loop:** No benefit to recursion
3. **Exponential blowup:** Without memoization
4. **Performance critical:** Recursion has function call overhead

Example: Summing array 1 to n: use iteration, not recursion.

### **Q43: What's a "mutual recursion" and when does it appear?**
A: Functions call each other.
```cpp
bool isEven(int n) {
    if (n == 0) return true;
    return isOdd(n-1);
}
bool isOdd(int n) {
    if (n == 0) return false;
    return isEven(n-1);
}
```
Appears in: Parsing (expression → term → factor → expression), state machines.

### **Q44: How do you trace a recursive function by hand?**
A:
1. Write the function
2. Call it with small input
3. Draw the call tree
4. Expand each call until base case
5. Unwind, computing values bottom-up

Example: fib(4) → fib(3) + fib(2) → ... → expand all → compute values → result.

### **Q45: What's the difference between "call depth" and "time complexity" for recursion?**
A:
- **Depth:** Maximum recursion depth (space O(depth))
- **Time:** Total number of calls (time = sum of all operations)

Naive Fibonacci:
- Depth: O(n)
- Time: O(2^n)
Both matter for different reasons.

---

## ⚡ Recursion II (Day 5) - 12 Q&A Pairs

### **Q46: What is "tail recursion" and why does it matter?**
A: Function where recursive call is the last operation (nothing after return).

```cpp
// NOT tail-recursive (multiply after return)
int fact(int n) { return n * fact(n-1); }

// Tail-recursive (result returned directly)
int factTail(int n, int acc=1) { 
    if (n <= 1) return acc;
    return factTail(n-1, n*acc);  // Last operation is return
}
```

Compiler can optimize tail recursion to O(1) space (reuse stack frame).

### **Q47: Will C++ optimize my tail recursion?**
A: Depends. C++ does NOT guarantee tail-call optimization.
- g++ -O2 flag: yes, usually
- Without optimization: no

You must check compiler behavior and flags. Scheme guarantees it.

### **Q48: How do you convert non-tail-recursive to tail-recursive?**
A: Add accumulator parameter, do computation in accumulator.

```cpp
// Non-tail
int sum(int arr[], int n) {
    if (n == 0) return 0;
    return arr[n-1] + sum(arr, n-1);  // + after return
}

// Tail-recursive
int sumTail(int arr[], int n, int acc=0) {
    if (n == 0) return acc;
    return sumTail(arr, n-1, acc + arr[n-1]);  // computation in arg
}
```

### **Q49: What is memoization and how does it work?**
A: Cache function results to avoid recomputation.

```cpp
unordered_map<int, int> memo;

int fib(int n) {
    if (memo.count(n)) return memo[n];  // Check cache
    if (n <= 1) return n;
    memo[n] = fib(n-1) + fib(n-2);      // Compute and cache
    return memo[n];
}
```

Result: O(2^n) → O(n) time, but uses O(n) space for cache.

### **Q50: How much speedup does memoization give Fibonacci?**
A: MASSIVE.
- fib(40) naive: 2^40 ≈ 1 trillion calls (1000 seconds)
- fib(40) memoized: 40 unique subproblems (milliseconds)

1000x+ speedup by caching.

### **Q51: Is memoization the same as dynamic programming?**
A: Memoization is one technique. DP is broader.
- **Memoization (top-down):** Recursive + caching
- **Tabulation (bottom-up):** Iterative, fill table

Both are dynamic programming. Memoization is recursive DP.

### **Q52: Can you apply memoization to any recursive function?**
A: Yes, if:
1. Function is "pure" (same input → same output)
2. Subproblems repeat (memoization helps)
3. Space available for cache

Example: fib(n) is pure, has repeats, memoization helps.
Example: printTree(node) is not pure (side effects), memoization doesn't help.

### **Q53: What's the space complexity of memoized Fibonacci?**
A: O(n) for cache + O(n) for call stack = O(n) total.

But: Avoids 2^n time, so space is a good trade-off.

### **Q54: What is "mutual recursion" and where does it appear?**
A: Functions call each other (not themselves).
```cpp
bool isEven(int n) {
    if (n == 0) return true;
    return isOdd(n-1);
}
bool isOdd(int n) {
    if (n == 0) return false;
    return isEven(n-1);
}
```
Appears in: Compilers (recursive descent parsing), state machines, game trees.

### **Q55: How do you handle cycles in mutual recursion?**
A: Must have base case that breaks the cycle.

```cpp
// With base case: terminates
bool isEven(int n) { if (n==0) return true; return isOdd(n-1); }
bool isOdd(int n) { if (n==0) return false; return isEven(n-1); }

// Without base case: infinite recursion
bool bad(int n) { return good(n); }
bool good(int n) { return bad(n); }
```

### **Q56: Can you memoize mutual recursion?**
A: Yes. Cache results for each function separately.

```cpp
unordered_map<int, bool> evenMemo, oddMemo;

bool isEven(int n) {
    if (evenMemo.count(n)) return evenMemo[n];
    bool res = (n == 0) || isOdd(n-1);
    evenMemo[n] = res;
    return res;
}
```

### **Q57: What optimization is used in compilers for parsing?**
A: Recursive descent parsing uses mutual recursion matching grammar rules.

Grammar:
```
Expression → Term (('+' | '-') Term)*
Term → Factor (('*' | '/') Factor)*
Factor → '(' Expression ')' | Number
```

Each production becomes a function; they call each other recursively.

---

## 🎯 Final Practice Questions

### **Cross-Topic Integration (Hard)**

**Q58:** Write a tail-recursive power function power(x, n) with memoization. Analyze time and space.

**Q59:** Prove that naive Fibonacci is O(2^n) using recurrence relation.

**Q60:** Compare array access (cache-friendly) vs linked list traversal (cache-unfriendly) Big-O complexity. Why do they have same Big-O but different practice?

---

## Summary

**Week 1 Interview Q&A covers:**
- RAM Model & Pointers (12 Q&A)
- Asymptotic Analysis (13 Q&A)
- Space Complexity (10 Q&A)
- Recursion I (10 Q&A)
- Recursion II (12 Q&A)
- Integration (3 Q&A)

**Total: 60 Q&A pairs** covering all topics.

**How to use:**
1. Read daily instructional file
2. Answer the Q&A pairs (without cheating!)
3. Check your answer
4. Review if incorrect
5. Repeat until confident

