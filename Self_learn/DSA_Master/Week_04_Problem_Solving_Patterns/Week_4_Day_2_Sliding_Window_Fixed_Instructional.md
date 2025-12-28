# Week 4, Day 2: Sliding Window (Fixed Size)

## 🗓 Metadata
**Week:** 4 | **Day:** 2 of 5 | **Topic:** Fixed-Size Sliding Window  
**Category:** Problem-Solving Patterns | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-3 (arrays, time complexity), Day 1 (two pointers)  
**Time:** 120-150 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem
Processing contiguous subarrays repeatedly (rolling averages, network throughput sampling, image filtering). Naive approach recomputes sum for each window O(n*k). Sliding window maintains running state O(n).

### Design Problems Solved
- **Maximum sum of k consecutive elements**
- **Average temperature over k days** (rolling average)
- **Longest substring with k distinct characters** (variant)
- **Network packet statistics** (window-based metrics)
- **Image convolution** (fixed-size kernel)
- **Time-series smoothing** (moving average)
- **Duplicate detection within window**

### Real System Usage
- **Linux kernel network buffering:** TCP receive window slides through incoming packets, dropping oldest as new arrive
- **Database query optimization:** Window functions (ROW_NUMBER, RANK) use fixed-size sliding partition
- **Time-series databases (InfluxDB):** Aggregation over fixed time windows (1 min, 5 min, 1 hour)
- **Graphics antialiasing:** Kernel convolution uses fixed-size window sliding over pixels
- **Compression algorithms:** DEFLATE algorithm maintains 32KB window of previous data
- **Multimedia streaming:** Jitter buffer maintains fixed-size window of packets for timing compensation
- **Machine learning:** Mini-batch processing uses fixed-size window of samples

### Why Sliding Window Matters
**Reduces redundant computation from O(n*k) to O(n)** by maintaining aggregate state and updating incrementally. Eliminates need to resum/recompute for each window position.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy
Imagine **drawing a rectangular frame** over a scrolling filmstrip. The frame width is fixed (k frames). As you slide the frame forward, you lose one frame on the left and gain one on the right. You don't rescan all k frames each time—you just update by removing old and adding new.

### Key Invariants
1. **Window Size Invariant:** Window always contains exactly k elements (difference between right and left pointers)
2. **Sliding Invariant:** Pointers move forward only (never backward); window slides left-to-right
3. **State Invariant:** Aggregate value (sum, max, etc.) always reflects current window elements
4. **Increment Invariant:** When both pointers advance by 1, window slides by 1 position

### Visual Representation

```
Fixed-Size Sliding Window (k=3):

Array:    [1, 3, 2, 6, -1, 4, 1, 8]
           ^^^                          Window at position 0: sum=6
         left=0, right=2

Array:    [1, 3, 2, 6, -1, 4, 1, 8]
              ^^^                       Window at position 1: sum=11
            left=1, right=3

Array:    [1, 3, 2, 6, -1, 4, 1, 8]
                 ^^^                    Window at position 2: sum=8
               left=2, right=4

Array:    [1, 3, 2, 6, -1, 4, 1, 8]
                    ^^^                 Window at position 3: sum=5
                  left=3, right=5

Window slides forward: remove leftmost, add rightmost
Aggregate updates O(1) by: new_sum = old_sum - arr[left-1] + arr[right]
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### State Definition
- **window_sum:** Aggregate of current k elements
- **left:** Start index of window (inclusive)
- **right:** End index of window (inclusive)
- **result:** Best value found so far (max sum, min average, etc.)

### Operation 1: Maximum Sum of k Consecutive Elements

```
Algorithm: Find maximum sum in fixed-size window

Initialize:
  window_sum ← 0
  max_sum ← 0
  
Step 1: Build initial window (first k elements)
  for i = 0 to k-1:
    window_sum += array[i]
  max_sum = window_sum

Step 2: Slide window forward
  left ← 0
  right ← k
  
  While right < array.length:
    // Remove leftmost element from previous window
    window_sum -= array[left]
    
    // Add new rightmost element
    window_sum += array[right]
    
    // Update max if needed
    max_sum = max(max_sum, window_sum)
    
    left++
    right++

return max_sum

Time: O(n) — traverse array once
Space: O(1) — constant variables only
```

**Key Insight:** Build window once O(k), then slide n-k times O(1) each. Total O(k + (n-k)) = O(n).

### Operation 2: Rolling Average Computation

```
Algorithm: Compute rolling average over k samples

Initialize:
  window_sum ← sum of first k elements
  result ← []

For each position from 0 to n-k:
  current_average = window_sum / k
  result.append(current_average)
  
  // Slide window forward
  if position < n - k:
    window_sum = window_sum - array[position] + array[position + k]

return result

Time: O(n) — one pass through array
Space: O(n-k+1) — store results (output space)
```

**Key Insight:** Average changes by only k-th multiplication. Update is: remove old element weight, add new element weight.

### Operation 3: First Sliding Window Maximum

```
Algorithm: Find maximum element in each k-size window

Initialize:
  result ← []
  window = deque() // stores indices of useful elements

For i = 0 to n-1:
  // Remove indices outside current window
  While window not empty and window[0] <= i - k:
    window.removeLeft()
  
  // Remove smaller elements (they can't be max)
  While window not empty and array[window[-1]] <= array[i]:
    window.removeRight()
  
  // Add current element
  window.append(i)
  
  // If window is complete, record maximum
  if i >= k - 1:
    result.append(array[window[0]])  // Front of deque is max

return result

Time: O(n) — each element added/removed once
Space: O(k) — deque stores at most k elements
```

**Key Insight:** Deque maintains decreasing order, enabling O(1) max lookup.

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example 1: Maximum Sum in Window of 3

**Problem:** Find max sum of any 3 consecutive elements in [1, 3, 2, 6, -1, 4, 1, 8]

```
Array:  [1, 3, 2, 6, -1, 4, 1, 8]
k = 3

Step 1: Build initial window [1, 3, 2]
sum = 1 + 3 + 2 = 6
max_sum = 6

Step 2: Slide to [3, 2, 6]
sum = 6 - 1 + 6 = 11
max_sum = 11

Step 3: Slide to [2, 6, -1]
sum = 11 - 3 + (-1) = 7
max_sum = 11

Step 4: Slide to [6, -1, 4]
sum = 7 - 2 + 4 = 9
max_sum = 11

Step 5: Slide to [-1, 4, 1]
sum = 9 - 6 + 1 = 4
max_sum = 11

Step 6: Slide to [4, 1, 8]
sum = 4 - (-1) + 8 = 13
max_sum = 13

Answer: 13 (from subarray [4, 1, 8])
Windows checked: 6 (out of C(8,3) = 56 possible without sliding window!)
```

**Why efficient:** Checked 6 windows in O(8) time. Brute force would be O(8³) = O(512) worst case.

---

### Example 2: Rolling Average Temperature

**Problem:** Compute 3-day rolling average for [70, 72, 68, 75, 71]

```
Temps:  [70, 72, 68, 75, 71]
k = 3

Initial window: [70, 72, 68]
sum = 210
average = 210/3 = 70.0

Slide to [72, 68, 75]
sum = 210 - 70 + 75 = 215
average = 215/3 = 71.67

Slide to [68, 75, 71]
sum = 215 - 72 + 71 = 214
average = 214/3 = 71.33

Output: [70.0, 71.67, 71.33]
(3 days of rolling average from 5-day period)
```

**Why useful:** Smooths out daily noise to show trend.

---

### Example 3: Sliding Window Maximum (Using Deque)

**Problem:** Find max in each 3-element window of [3, 3, 5, 1, 5]

```
Array:  [3, 3, 5, 1, 5]
k = 3

i=0: Window not complete
deque: add index 0
deque: [0]

i=1: Window not complete
arr[1]=3, deque[-1]=3, they're equal, so don't remove
deque: add index 1
deque: [0, 1]

i=2: Window complete [3, 3, 5]
i >= k-1, so we process
arr[2]=5 > arr[1]=3, remove index 1
arr[2]=5 > arr[0]=3, remove index 0
deque: add index 2
deque: [2]
max = arr[2] = 5, result = [5]

i=3: Window [3, 5, 1]
index 0 (arr[0]=3) now outside window (i - k = 0), remove it
deque: [2]
arr[3]=1 < arr[2]=5, don't remove
deque: add index 3
deque: [2, 3]
max = arr[2] = 5, result = [5, 5]

i=4: Window [5, 1, 5]
index 1 outside window, check: 1 <= 4 - 3 = 1, yes remove it
deque: [2, 3]
arr[4]=5 == arr[3]=1? No. arr[4]=5 > arr[3]=1, remove 3
arr[4]=5 >= arr[2]=5? Yes, remove 2
deque: add index 4
deque: [4]
max = arr[4] = 5, result = [5, 5, 5]

Answer: [5, 5, 5]
```

**Why deque works:** Maintains candidates in decreasing order. Front element is always current max.

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Operation | Time | Space | Conditions |
|-----------|------|-------|-----------|
| **Max sum (simple)** | O(n) | O(1) | Build once, slide n-k |
| **Rolling average** | O(n) | O(output) | Same as max sum |
| **Sliding window max** | O(n) | O(k) | Deque maintains O(1) max |
| **With preprocessing** | O(n) | O(n) | Store all window values |

### Real Memory Behavior
- **Cache efficiency:** Sequential access (right++) maintains cache locality
- **Memory bandwidth:** Updates to window state use single variable (sum), minimal memory traffic
- **Deque overhead:** Even though deque is O(k), constant k makes it O(1) practical overhead
- **Early termination:** No early exit possible (must slide entire array), always O(n)

### Edge Cases & Failure Modes

1. **k larger than array:** Window never completes
   - ❌ **Risk:** Return empty result (no valid windows)
   - ✅ **Solution:** Check n < k upfront, handle gracefully

2. **k equals 1:** Window is single element
   - ❌ **Risk:** Special case crashes (off-by-one)
   - ✅ **Solution:** Works correctly naturally (max of single element is itself)

3. **Negative numbers:** Affect max/min logic
   - ❌ **Risk:** Initialize max_sum incorrectly (should be INT_MIN not 0)
   - ✅ **Solution:** Handle negative sums explicitly

4. **Floating-point precision:** Rolling average accumulates error
   - ❌ **Risk:** Round-off errors accumulate over large n
   - ✅ **Solution:** Use Kahan summation for high precision

5. **Window is entire array:** No sliding happens
   - ❌ **Risk:** Loop doesn't execute (left never moves)
   - ✅ **Solution:** Works naturally (just computes single window aggregate)

---

## 6️⃣ REAL SYSTEM INTEGRATION

### System 1: TCP Receive Window (Linux Networking)
TCP uses sliding window for flow control:
```
Receive buffer size = 64KB (fixed window)
As data arrives, right pointer moves forward
As application reads, left pointer moves forward
Window "slides" through packet stream
```
Prevents buffer overflow by limiting in-flight data.

### System 2: Time-Series Aggregation (InfluxDB/Prometheus)
Fixed-size time windows aggregate metrics:
```
Window: last 5 minutes
As new data point arrives after 5 min, drop oldest
Compute: sum, avg, max, min within window
Update every 1 second (slide window)
```
Enables real-time metrics without storing everything.

### System 3: Video Codec Compression (H.264)
Motion estimation uses fixed-size search window:
```
Frame buffer: 16x16 pixel window (macroblock)
Search window: +/-64 pixels around block
Find best match in previous frame within window
Use offset as motion vector (compression)
```
Reduces redundancy in consecutive frames.

### System 4: String Matching (DEFLATE/Zlib)
Compression maintains 32KB window of previous data:
```
Sliding window of 32KB
Search for repeated patterns within window
Emit: (distance to match, length of match)
Slide window forward as data processed
```
Enables compression without storing entire file.

### System 5: Kubernetes Rolling Updates
Pod rolling window ensures gradual replacement:
```
MaxSurge = 1 new pod
MaxUnavailable = 1 old pod
At any time: window contains mix of old/new versions
As new pods ready, slide: remove old, add new
Window slides through all replicas
```
Maintains availability during updates.

### System 6: Stock Market Bollinger Bands
Technical analysis uses fixed-period moving average:
```
Window: last 20 trading days
Compute mean and standard deviation within window
Bands: mean ± 2×std_dev
Update daily as new price arrives, oldest drops out
```
Identifies overbought/oversold conditions.

### System 7: Network Quality of Service (QoS)
Leaky bucket algorithm uses fixed-size window:
```
Token bucket (window): capacity C tokens
Refill rate: r tokens per second
Packet requires token(s) from bucket
Bucket size window regulates traffic rate
```
Prevents network congestion through rate limiting.

---

## 7️⃣ CONCEPT CROSSOVERS

### Builds On
- **Week 1 Complexity:** O(n) vs O(nk) reduction (two-pointer pattern foundation)
- **Week 2 Arrays:** Index-based element access (left/right pointers)
- **Day 1 Two Pointers:** Sequential element processing (similar mental model)
- **Prefix Sums (Day 4):** Range query foundation (window queries)

### Built Upon By
- **Week 11 DP:** State transitions use window sliding (DP recurrence)
- **Segment Trees:** Range query on fixed intervals
- **Monotonic Deque:** Advanced window problems (with deque data structure)
- **Week 8 Specialized:** Suffix arrays use window of subsequences

### Used In Algorithms
- **Merge K Sorted Lists:** Sliding window to find min across k lists
- **Minimum Window Substring:** Variable sliding (extends to Week 4 Day 3)
- **Trapping Rainwater:** Window with prefix/suffix maximums
- **Bitwise Operations:** Rolling bitmask (XOR of k elements)

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

### Theorem 1: Sliding Window Optimality
**Claim:** Sliding window reduces O(nk) to O(n) for fixed window.

**Proof:**
- Naive: For each of n windows, compute sum of k elements = O(nk)
- Sliding: Build first window O(k), then n-1 slides with O(1) update = O(k + n-1) = O(n)
- Speedup factor: nk / n = k (linear in window size)
- For large n, k constant: speedup is k×

### Theorem 2: Deque Maximum Maintenance
**Claim:** Deque maintains current window maximum in O(1) amortized time.

**Invariant:** Deque stores indices in strictly decreasing order of values.

**Proof:**
- When adding element: remove all smaller elements from back, add new
- Property: front element always has max value in deque
- Amortized: each element added once and removed at most once = O(n) total
- Per operation: amortized O(1)

### Theorem 3: Window Sliding Correctness
**Claim:** Sliding window covers all contiguous k-subarrays exactly once.

**Proof:**
- Window positions: [0, k-1], [1, k], [2, k+1], ..., [n-k, n-1]
- Number of positions: n - k + 1
- Each subarray appears exactly once
- No subarray appears twice (pointers move forward only)
- Total windows = n - k + 1 (correct)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

### When to Use Fixed Sliding Window

✅ **Use when:**
- **Window size is fixed/known** (k is given constant)
- **Processing contiguous subsequences** (not arbitrary subsets)
- **Time-critical** (need O(n) not O(nk))
- **Aggregate over window** (sum, avg, max, etc.)
- **Rolling computation needed** (moving average, Bollinger bands)

✅ **Examples:**
- Maximum sum of k consecutive elements
- Rolling average over k days
- First sliding window maximum
- Contains duplicate (window size k)

### When Use Alternative

❌ **Use variable sliding window instead when:**
- Window size unknown (need to find optimal window)
- Constraint is on window contents (unique chars, etc.) not size
- Target is property of elements, not fixed count

❌ **Use prefix sums instead when:**
- Only querying ranges, not processing sequentially
- Multiple independent range queries (precompute)

❌ **Use segment tree instead when:**
- Need range queries AND updates
- Complex aggregate function (not just sum)

### Decision Framework

```
Processing subarrays?
├─ YES: Is window size FIXED?
│   ├─ YES: Use fixed sliding window
│   └─ NO: Use variable sliding window (Day 3)
└─ NO: Different approach needed
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1: Why does building initial window O(k) not hurt overall O(n) complexity?**
- Hint: What's the big-O complexity of k + (n-k) iterations?
- Deep: How does constant factor affect asymptotic analysis?

**Q2: If window size changes during problem, can we use fixed sliding window?**
- Hint: What assumption about pointers breaks?
- Deep: How would algorithm need to change?

**Q3: Why store indices in deque instead of values for window maximum?**
- Hint: What happens when window slides? Can we just shift values?
- Deep: How do indices enable removing elements outside window?

**Q4: Is fixed sliding window always better than recomputing each window?**
- Hint: What if k is very large and window operation expensive?
- Deep: When would recomputation be preferable?

**Q5: Can we use sliding window on 2D arrays?**
- Hint: How would window slide? What's the movement pattern?
- Deep: How does complexity scale with 2D window size?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Fixed sliding window transforms O(nk) to O(n) by maintaining running aggregate: remove left element, add right element, slide forward.**

**Mnemonic:** **FRAME** (window frame of fixed size slides forward) or **FILMSTRIP** (moving frame on scrolling film)

**Geometric Cue:** Rectangular frame of fixed width sliding across a number line. Width never changes, only position.

### 5 Cognitive Lenses

| **Computational** | Aggregate stored in single variable (O(1) update). Deque uses O(k) space but enables O(1) operations via index-based removal. Cache-friendly: sequential pointer movement. |
| **Psychological** | Counterintuitive: never recompute window sum (update is remove + add). Mental model: "don't rescan what you already know." |
| **Design Trade-off** | Fixed window: simple, O(n) guaranteed. Variable window: complex logic, handles more problems. Choose based on problem constraint. |
| **AI/ML Analogy** | Batch processing: fixed batch size k processes data in chunks. Mini-batch sliding window = moving through epochs. |
| **Historical Context** | Used since UNIX pipe design (~1970s) for streaming data. Formalized in algorithms via "sliding window" term ~2000s in competitive programming. |

---

## Supplementary Outcomes

### Practice Problems (8+)

1. **Maximum Average Subarray I** (LeetCode 643)
   - Find k-length subarray with max average
   - Return the maximum average
   - [Easy] 15 min

2. **Number of Sub-arrays of Size K with Average Greater than or Equal to Threshold** (LeetCode 1343)
   - Count k-length subarrays with average ≥ threshold
   - [Medium] 20 min

3. **Maximum Consecutive Sum** (LeetCode variant)
   - Max sum of any k consecutive elements
   - Return both sum and subarray
   - [Easy] 15 min

4. **Sliding Window Maximum** (LeetCode 239)
   - Find max in each k-size window
   - Use deque for O(n) solution
   - [Hard] 30 min

5. **Contains Duplicate II** (LeetCode 219)
   - Detect duplicate within k indices
   - k-size window with hash set
   - [Easy] 20 min

6. **Grumpy Bookstore Owner** (LeetCode 1052)
   - Maximize satisfied customers using k-minute window
   - Track who's satisfied normally vs with help
   - [Medium] 25 min

7. **Subarrays with K Different Integers** (LeetCode 992)
   - Count subarrays with exactly k distinct integers
   - Variant of variable sliding window
   - [Hard] 35 min

8. **Moving Average from Data Stream** (LeetCode 346)
   - Implement stream class computing moving average
   - Fixed-size window on streaming data
   - [Easy] 20 min

### Interview Q&A Highlights

**Q: What's the difference between fixed and variable sliding window?**
A: Fixed: window size k is constant, pointer movement synchronized. Variable: window size changes to satisfy constraint (next day's material).

**Q: Why use deque instead of simple max tracking?**
A: Simple tracking only remembers current max. Deque remembers all candidates in decreasing order, enabling O(1) removal when element leaves window.

**Q: Can sliding window work on unsorted arrays?**
A: Yes, uniquely from two-pointers. Sliding window doesn't exploit sorting—works on any array.

### Common Misconceptions

- ❌ **"Sliding window only for sorted arrays"** → ✅ Works on any array (doesn't need sorting)
- ❌ **"Must build complete first window"** → ✅ Can iterate from position 0, check when i >= k-1
- ❌ **"Deque is required for all sliding windows"** → ✅ Only needed when you need max/min (simple sum doesn't need it)

---

**Status:** ✅ Complete  
**Confidence Check:** Can you compute rolling average from scratch? Can you implement sliding window maximum?  
**Next:** Move to Day 3 (Variable Sliding Window) for dynamic window sizing

