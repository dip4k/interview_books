# 📘 WEEK 1 DAY 4: RECURSION II - Complete Learning Package

**Week 1, Day 4: Advanced Recursion Patterns**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🔴 Hard | Target: 4-5/5

---

## PART 1: MAIN CONTENT

### 1️⃣ The Why

**Problem:** Simple recursion covers basic cases. But real problems are messier:
- **Multiple recursive calls:** Not just T(n-1) but T(n-1) + T(n-2)
- **Different bases:** Recursing on different dimensions
- **Performance:** Naive approach = exponential explosion

---

### 2️⃣ The What

**Tail Recursion:** Recursive call is last operation

```python
# Tail recursive (can be optimized to loop)
def factorial_tail(n, acc=1):
    if n <= 1:
        return acc
    return factorial_tail(n-1, n*acc)  # Recursive call is LAST

# Not tail recursive
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n-1)  # Multiplication AFTER call
```

**Tail Call Optimization (TCO):** Reuse stack frame instead of allocating new one.

```
Without TCO:
factorial_tail(5, 1)
  → factorial_tail(4, 5)
    → factorial_tail(3, 20)
      → factorial_tail(2, 60)
        → factorial_tail(1, 120)
          → return 120

Stack depth: 5 frames

With TCO (compiler transforms):
factorial_tail(5, 1) REUSE frame
  | update n=4, acc=5
  | jump back to start
  | update n=3, acc=20
  | jump back to start
  ...
  → return 120

Stack depth: 1 frame
```

**Multiple Recursion:** Function calls itself multiple times

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)  # TWO recursive calls!

fib(5) tree:
       fib(5)
       /    \
    fib(4)  fib(3)
    /  \    /  \
 fib(3) fib(2) fib(2) fib(1)
  ...

Total calls: exponential in n (very bad!)
```

**Mutual Recursion:** Functions call each other

```python
def is_even(n):
    if n == 0: return True
    return is_odd(n-1)

def is_odd(n):
    if n == 0: return False
    return is_even(n-1)

is_even(4):
  → is_odd(3)
    → is_even(2)
      → is_odd(1)
        → is_even(0) → True
```

---

### 3️⃣ The How

**Analyzing Multiple Recursion:**

```
T(n) = T(n-1) + T(n-2)  (like fibonacci)

Unfold:
T(n) = T(n-1) + T(n-2)
     = [T(n-2) + T(n-3)] + T(n-2)
     = 2·T(n-2) + T(n-3)
     ...
     ≈ O(φ^n) where φ ≈ 1.618 (golden ratio)
```

**Recursion Trees:**

```
For T(n) = T(n-1) + T(n-2) + O(1):

       n=5 (1 node, cost 5)
       /  \
      4    3  (2 nodes, cost 4+3)
     / \  / \
    3  2 2  1  (4 nodes, cost 3+2+2+1)
   ...

Total nodes exponential in n!
```

**Optimization: Memoization**

```python
# Naive: O(2^n)
def fib_naive(n):
    if n <= 1: return n
    return fib_naive(n-1) + fib_naive(n-2)

# With memoization: O(n)
def fib_memo(n, memo={}):
    if n in memo: return memo[n]
    if n <= 1: return n
    result = fib_memo(n-1, memo) + fib_memo(n-2, memo)
    memo[n] = result
    return result
```

---

### 4️⃣ Visualization

**Exponential Explosion:**

```
fib(6) calls:
  fib(5): 8 calls needed
  fib(4): 5 calls needed
  fib(3): 3 calls needed
  ...
  Total: 25 calls just to compute one number!

fib(50) would need 2^50 ≈ 10^15 calls (impossible)
```

**Memoization Cache:**

```
Computing fib(5) with memo:
  fib(5) not cached → compute
    fib(4) not cached → compute
      fib(3) not cached → compute
        fib(2) not cached → compute
          ...
        cache[2] = 1
      cache[3] = 2
    cache[4] = 3
  cache[5] = 5

Computing fib(6) with memo:
  fib(6) not cached → compute
    fib(5) IS cached → return 5 instantly!
    fib(4) IS cached → return 3 instantly!
  cache[6] = 8

Each new value computed once, reused as needed.
```

---

### 5️⃣ Critical Analysis

**Complexity:**

| Type | Recurrence | Complexity |
|------|-----------|-----------|
| Linear | T(n) = T(n-1) + 1 | O(n) |
| Multiple | T(n) = k·T(n-1) | O(k^n) |
| Divide conquer | T(n) = a·T(n/b) + f(n) | Master theorem |
| Tail recursive | Same as recursive | O(n) but reuses frames |

**Space:**

```
Without TCO: O(depth) call stack frames
With TCO: O(1) constant space (function doesn't consume stack)

With memoization: O(depth) call stack + O(subproblems) memory for cache
```

---

### 6️⃣ Real Systems

**Parsing:** Expression grammar is recursive (expr contains expr)
```
Expression → Term '+' Expression | Term
Term → Factor '*' Term | Factor
Factor → Number | '(' Expression ')'

Parse "2 + 3 * 4" recursively!
```

**Tree/Graph algorithms:** DFS naturally recursive
```
def dfs(node):
    visit(node)
    for child in node.children:
        dfs(child)  # Recursively visit children
```

---

### 7️⃣ Connections

Builds on: Day 3 (recursion basics)
Enables: Week 5+ (tree/graph algorithms), Week 11 (dynamic programming)

---

### 8️⃣ Mathematics

**Characteristic Equation Method:**

For T(n) = a₁·T(n-1) + a₂·T(n-2) + ... + aₖ·T(n-k):

Find roots of x^k = a₁·x^(k-1) + ... + aₖ

Then T(n) = c₁·r₁^n + c₂·r₂^n + ... (where rᵢ are roots)

**Golden Ratio in Fibonacci:**

T(n) = T(n-1) + T(n-2)

Characteristic equation: x² = x + 1
Roots: φ = (1+√5)/2 ≈ 1.618, ψ = (1-√5)/2 ≈ -0.618

T(n) ≈ φ^n / √5 = O(φ^n)

---

### 9️⃣ Design Intuition

**When to use tail recursion:**
- Simple counting/iteration (can use loop instead)
- Supported language: Scheme, some functional languages
- Not Python/Java (no TCO support)

**When to memoize:**
- Multiple recursive calls (k > 1)
- Overlapping subproblems (same inputs computed multiple times)
- Space available (memory vs CPU trade-off)

**Avoid:**
- Exponential recursion without memoization
- Tail recursion > 10,000 depth (TCO not guaranteed)

---

### 🔟 Knowledge Check

1. What's tail recursion and why is TCO useful?
2. Compare T(n) = T(n-1) vs T(n) = 2·T(n-1)
3. Why does fibonacci explode exponentially?
4. How does memoization reduce fib(50) from 10^15 to ~50 calls?
5. Derive T(n) = 3·T(n-1) + 1
6. What's mutual recursion and when is it useful?
7. When is iteration better than tail recursion?

### 1️⃣1️⃣ Hooks

**One-liner:** "Multiple recursion explodes exponentially; memoization fixes it."

**Memory aid:** "Fib without memo = 2^n (terrible). Fib with memo = n (great)."

---

## PART 2: QUICK SUMMARY

**Key Patterns:**
- Linear: T(n) = T(n-1) + O(1) = O(n)
- Multiple: T(n) = k·T(n-1) = O(k^n) 🚫
- Memoized: O(subproblems) = O(n) if n² subproblems
- Tail: Same complexity, better space (if TCO)

**Memoization Rules:**
- Store results of subproblems
- Return cached result if seen before
- Trade space for time

---

## PART 3: QUESTIONS & ANSWERS

**Q1:** Is factorial(1000) safe with recursion?
**A:** No, stack typically limits ~10K depth. Use iteration instead.

**Q2:** fib(40) with naive recursion?
**A:** ~300 million calls. With memoization: 40 calls. 10^6× difference!

**Q3:** Tail recursion example?
**A:** `def f(n, acc): if n<=0: return acc else: return f(n-1, acc+n)`

**Q4:** Can you memoize multiple recursion?
**A:** Yes! Store results of each unique (n) in dictionary. Turns exponential to polynomial.

**Q5:** When does mutual recursion occur?
**A:** Language parsing (is_statement calls is_expression calls is_statement)

**Q6:** Derive T(n) = 4·T(n/2) + n
**A:** Master theorem: a=4, b=2, d=1. log₂(4)=2 > 1. So T(n) = Θ(n²)

**Q7:** Is recursion slower than iteration?
**A:** Yes, function call overhead. But same Big-O. Use recursion for clarity on recursive problems.

---

## PART 4: README

**90-Minute Study:**
- Why (15 min): Multiple recursion and optimization
- What (15 min): Tail recursion, memoization
- How (15 min): Trace with memo
- Visualization (15 min): See exponential explosion, memo benefits
- Analysis (10 min): Complexity, space

**Key Skill:** Understand exponential growth and how memoization fixes it

**Hard Part:** Accepting that naive recursion is sometimes VERY bad

---

**Status:** ✅ Complete | **Next:** Day 5 - Space Complexity

