# 🎯 WEEKS 1-2: COMPREHENSIVE PRACTICAL PROBLEMS
## Real-World Scenarios, Analysis, and Deep Learning

---

## PART 1: WEEK 1 DEEP-DIVE PROBLEMS

### 🎯 PROBLEM SET 1: RECURSION & STACK OVERFLOW

#### Problem 1.1: Real-World Stack Overflow - File System Traversal

**Scenario:** You're writing a backup system that recursively traverses directories.

```
Directory structure:
C:\
├─ Users\        (depth 1)
│  ├─ John\      (depth 2)
│  │  ├─ Desktop\ (depth 3)
│  │  │  └─ Projects\ (depth 4)
│  │  │     └─ ... (continues)
│  ├─ Jane\      (depth 2)
│  ├─ Admin\     (depth 2)
├─ Windows\      (depth 1)
│  ├─ System32\  (depth 2)
│  │  └─ drivers\ (depth 3)
│  │     └─ ... (continues deeply)
└─ Program Files\ (depth 1)
   └─ ...
```

**Questions:**

A. **Maximum Safe Depth Calculation:**
   - Assume each frame is 24 bytes
   - Stack size on Windows: 1MB (smaller than Linux!)
   - Calculate: max_depth = 1MB / 24 bytes = ?
   
B. **Real Directory Depths:**
   - Typical Windows: max depth ≈ 30
   - Some weird setups: max depth ≈ 100+
   - Will 1MB stack handle this?
   
C. **The Problem:**
   ```
   def traverse_recursive(path):
       for item in os.listdir(path):
           full_path = os.path.join(path, item)
           if os.path.isdir(full_path):
               traverse_recursive(full_path)  # Recursive call
               # This adds frame to call stack
   ```
   
   If someone creates a directory 50 levels deep:
   - Stack frames needed: 50 (one per level)
   - Stack space: 50 × 24 = 1,200 bytes
   - Available: 1MB = 1,000,000 bytes
   - Safe? YES or NO?

D. **The Real Problem:**
   Now add these per-level operations:
   ```
   def traverse_recursive(path):
       files = os.listdir(path)        # 4KB buffer for file list
       metadata = []                    # 8KB list of metadata
       cache = {}                       # 16KB dictionary
       
       for item in files:
           full_path = os.path.join(path, item)
           if os.path.isdir(full_path):
               traverse_recursive(full_path)
   ```
   
   Now each frame is:
   - Base frame: 24 bytes
   - Local variables: ~28KB
   - Total per frame: ~28KB
   
   New calculation:
   - Stack size: 1MB = 1,000,000 bytes
   - Per frame: 28,000 bytes
   - Max depth: 1,000,000 / 28,000 = ?
   - Safe for depth 50? YES or NO?

E. **Your Solution:**
   How would you fix this to support arbitrary directory depth?
   - Option 1: Use iteration instead of recursion
   - Option 2: Use explicit stack (list)
   - Option 3: Increase stack size
   - Which is best for a production backup system?

---

**Solution 1.1:**

A. 1MB / 24 = 41,666 frames max

B. Windows has smaller stack than Linux!
   - Typical depth 30: Safe
   - Unusual depth 100+: Risky
   
C. 50 levels:
   - 50 × 24 = 1,200 bytes needed
   - Answer: YES, safe for frames alone

D. With local variables:
   - Max depth = 1,000,000 / 28,000 = 35 frames
   - Depth 50 needed, but only 35 safe
   - Answer: NO, will overflow!

E. **Best solution: Iterative with explicit stack**
   ```
   Use manual stack to avoid recursive depth:
   - Push paths to visit onto stack (linked list)
   - Pop and process each path
   - No function call depth limit!
   - Only limit is available heap memory (much larger)
   ```

---

#### Problem 1.2: Recursion Tree Analysis - Cache Implementation

**Scenario:** You're optimizing a caching system that needs to calculate dependency trees.

```python
# Calculate cache invalidation on update
# When one value changes, what else depends on it?

dependencies = {
    'user_data': ['profile_cache', 'timeline_cache'],
    'profile_cache': ['home_page_cache'],
    'timeline_cache': ['home_page_cache', 'notifications'],
    'home_page_cache': ['rendered_html'],
    'notifications': ['notification_list_html'],
    'rendered_html': [],
    'notification_list_html': []
}

def find_all_invalidations(key, dependencies):
    """Find everything that needs invalidation"""
    if key not in dependencies:
        return []
    
    result = [key]
    for dependent in dependencies[key]:
        result.extend(find_all_invalidations(dependent, dependencies))
    return result
```

**Questions:**

A. **Draw the recursion tree** for `find_all_invalidations('user_data')`
   - Show each node (function call)
   - Show return values

B. **Count function calls:**
   - Total calls made?
   - Any duplicates? (overlapping subproblems)

C. **Is this code problematic?**
   - Time complexity: O(n), O(n²), or O(2^n)?
   - Could this cause stack overflow?

D. **How would memoization help?**
   - What would you cache?
   - Would it reduce calls significantly?

E. **Is there a better approach?**
   - Could you solve this iteratively?
   - Could you solve it without recursion?

---

**Solution 1.2:**

A. **Recursion tree:**
```
find_all_invalidations('user_data')
├─ 'user_data'
├─ find_all_invalidations('profile_cache')
│  ├─ 'profile_cache'
│  └─ find_all_invalidations('home_page_cache')
│     ├─ 'home_page_cache'
│     └─ find_all_invalidations('rendered_html')
│        └─ 'rendered_html'
└─ find_all_invalidations('timeline_cache')
   ├─ 'timeline_cache'
   ├─ find_all_invalidations('home_page_cache')
   │  └─ [duplicated work!]
   └─ find_all_invalidations('notifications')
      ├─ 'notifications'
      └─ find_all_invalidations('notification_list_html')
         └─ 'notification_list_html'
```

B. **Function calls:**
   - Total: ~15 calls
   - Duplicate: `find_all_invalidations('home_page_cache')` called twice!
   - Overlapping subproblems exist!

C. **Complexity:**
   - O(n) in best case (DAG, no duplicates)
   - But O(2^n) in worst case (if cycles or many overlaps)
   - Stack overflow unlikely (max depth ≈ 5)

D. **With memoization:**
   - Cache results of `find_all_invalidations(key)`
   - First call computes: 'home_page_cache' → ['rendered_html']
   - Second call returns cached result
   - Speedup: 2-4x (eliminates duplicate work)

E. **Better approach:**
   - Use BFS with explicit queue (iterative)
   - No recursion, no depth risk
   - Still finds all dependencies
   - Cleaner and faster

---

### 🎯 PROBLEM SET 2: BIG O ANALYSIS IN PRODUCTION

#### Problem 2.1: Trading System Performance Disaster

**Scenario:** Your trading system processes price updates and needs to find "hot stocks" (those with >10% price change).

**Initial Implementation:**

```python
def find_hot_stocks(prices_today, prices_yesterday, threshold=0.10):
    """Find all stocks with >10% price change"""
    hot_stocks = []
    
    for stock_today in prices_today:  # 5,000 stocks
        for stock_yesterday in prices_yesterday:  # 5,000 stocks
            if stock_today['symbol'] == stock_yesterday['symbol']:
                change = (stock_today['price'] - stock_yesterday['price']) / stock_yesterday['price']
                if abs(change) >= threshold:
                    hot_stocks.append(stock_today)
                break
    
    return hot_stocks
```

**Questions:**

A. **Time complexity analysis:**
   - Worst case: O(?)?
   - For 5,000 stocks: ? comparisons

B. **Real performance:**
   - Assume 1 comparison = 1 microsecond
   - Worst case time: ? seconds
   - Is this acceptable for a real-time trading system?

C. **Optimization 1: Use a hash table**
   ```python
   def find_hot_stocks_v2(prices_today, prices_yesterday, threshold=0.10):
       yesterday_dict = {s['symbol']: s for s in prices_yesterday}  # O(n)
       hot_stocks = []
       
       for stock_today in prices_today:  # O(n)
           if stock_today['symbol'] in yesterday_dict:  # O(1)
               # Calculate change
       
       return hot_stocks
   ```
   
   New time complexity: O(?)?
   New time for 5,000 stocks: ? seconds

D. **Optimization 2: Pre-sorted data**
   If both arrays are sorted by symbol, could you use O(n) solution?
   How?

E. **At scale (100,000 stocks):**
   - Original: ? seconds
   - With hash table: ? seconds
   - Speedup: ? times faster

---

**Solution 2.1:**

A. **Time complexity:**
   - Nested loops: O(n²)
   - 5,000 × 5,000 = 25,000,000 comparisons

B. **Real performance:**
   - 25 million microseconds = 25 seconds!
   - UNACCEPTABLE! Trading needs <100ms!

C. **With hash table:**
   - O(n) to build dictionary
   - O(n) to check each stock
   - Total: O(2n) = O(n)
   - 5,000 stocks: 10,000 operations = 10 milliseconds
   - ACCEPTABLE!

D. **Two-pointer approach (if sorted):**
   ```
   i = 0 (today)
   j = 0 (yesterday)
   
   while i < len(today) and j < len(yesterday):
       if today[i] == yesterday[j]:
           check change
           i += 1
           j += 1
       elif today[i] < yesterday[j]:
           i += 1
       else:
           j += 1
   
   Time: O(n), no hash table needed
   ```

E. **At 100,000 stocks:**
   - Original: 100,000² = 10 billion comparisons = 10,000 seconds (!!)
   - With hash table: 200,000 = 0.2 seconds
   - Speedup: 50,000x faster!

---

#### Problem 2.2: Web Crawler Performance Analysis

**Scenario:** Your web crawler visits websites and extracts data.

```python
def crawl_website(urls, depth=0, visited=None):
    """Recursively crawl website"""
    if visited is None:
        visited = []
    
    if depth > 5:  # Max depth 5
        return
    
    for url in urls:  # 10 URLs per page
        if url not in visited:
            visited.append(url)  # O(n) search!
            page = fetch(url)
            links = extract_links(page)
            crawl_website(links, depth+1, visited)
```

**Questions:**

A. **Time complexity of `url not in visited`:**
   - visited is a list
   - Searching a list: O(?)?
   
B. **How many URLs crawled (depth 5, 10 links per page)?**
   - Level 0: 10
   - Level 1: 10 × 10 = 100
   - Level 2: 10 × 100 = 1,000
   - ...
   - Total: 10 + 100 + 1,000 + 10,000 + 100,000 + 1,000,000 = 1,111,110 URLs

C. **Total time complexity:**
   - For each URL: check if in visited list: O(n)
   - n = number of URLs (grows to 1.1 million)
   - Average n during crawl: 500,000
   - Total: 1.1 million × O(500,000) = ?

D. **Fix: Use a set instead of list**
   ```python
   visited = set()  # Instead of []
   
   if url not in visited:  # Now O(1)!
       visited.add(url)
   ```
   
   New complexity: 1.1 million × O(1) = O(1.1 million)

E. **Performance impact:**
   - List version: ~550 billion operations
   - Set version: 1.1 million operations
   - Speedup: 500,000x faster!

---

**Solution 2.2:**

A. `url not in visited` on a list: O(n) (linear search)

B. Total URLs: 1,111,110 (geometric series)

C. **Worst time complexity:**
   - Average visited size: 500,000
   - Total: 1.1M URLs × O(500K) = O(550 billion) operations!

D. With set: O(1) per lookup

E. **Real speedup:**
   - List: 550 seconds (way too slow!)
   - Set: 1.1 seconds (acceptable)
   - 500x speedup!

---

### 🎯 PROBLEM SET 3: SPACE COMPLEXITY IN MOBILE

#### Problem 3.1: Mobile App Memory Crisis

**Scenario:** Your mobile app loads user feed (1,000 posts) using recursion.

```python
def load_feed_recursive(page=0):
    """Load feed recursively, one page at a time"""
    
    if page >= total_pages:
        return []
    
    # Load one page of posts (100 posts)
    posts = api_call(f"/posts?page={page}")  # Returns 100 posts
    
    # Each post:
    # - text: 1KB
    # - images: 50KB (compressed)
    # - metadata: 1KB
    # Total per post: ~52KB
    
    all_posts = posts + load_feed_recursive(page + 1)
    return all_posts
```

**Questions:**

A. **Stack depth:**
   - 10 pages total
   - Each recursive call = 1 frame
   - Max depth = ?

B. **Per-frame memory:**
   - Frame overhead: 24 bytes
   - Posts variable: 100 × 52KB = 5.2MB
   - Total per frame: ~5.2MB

C. **Total stack memory:**
   - Depth: 10
   - Memory per frame: 5.2MB
   - Total: 10 × 5.2MB = 52MB
   - iPhone memory: 512MB
   - Percentage used: 52/512 = 10%
   - Safe? YES or NO?

D. **The problem:**
   - Each frame has its own local copy of `posts`
   - When frame returns, new copy created in parent
   - At deepest level: ALL 10 frames exist simultaneously!

E. **The crisis:**
   What if users scroll to page 100 (1,000 pages)?
   - Stack memory: 100 × 5.2MB = 520MB!
   - Available: 512MB
   - Result: CRASH!

F. **Better approach:**
   How would you load 1,000 pages of posts?
   - Option 1: Iterative loading (no recursion)
   - Option 2: Lazy loading (load on demand)
   - Option 3: Pagination with limited memory
   - Which is best for mobile?

---

**Solution 3.1:**

A. Stack depth: 10 frames

B. Per-frame: ~5.2MB (posts array stored locally)

C. Total: 52MB = 10% of iPhone memory
   Safe for 10 pages

D. Issue: Each frame keeps its copy of posts in memory
   All copies exist simultaneously (not released until function returns)

E. At 100 pages:
   - Stack memory: 520MB > 512MB available
   - Result: Stack overflow crash!

F. **Best approach: Iterative with pagination**
   ```python
   def load_feed_iterative():
       all_posts = []
       page = 0
       while page < total_pages:
           posts = api_call(f"/posts?page={page}")
           all_posts.extend(posts)
           page += 1
       return all_posts
   
   Stack depth: 1 (constant)
   Memory: Only current page in memory = 5.2MB
   Total for 1000 pages: Still only 5.2MB!
   ```

---

## PART 2: WEEK 2 DEEP-DIVE PROBLEMS

### 🎯 PROBLEM SET 4: CACHE LOCALITY IN REAL SYSTEMS

#### Problem 4.1: Image Processing Performance (Cache Matters!)

**Scenario:** Processing a 10,000 × 10,000 pixel image.

```python
# Approach 1: Row-major (sequential, cache-friendly)
def process_image_row_major(image):
    """Process image going through rows"""
    total = 0
    for row in range(10000):
        for col in range(10000):
            pixel = image[row][col]
            total += pixel
    return total

# Approach 2: Column-major (jumpy, cache-unfriendly)
def process_image_column_major(image):
    """Process image going through columns"""
    total = 0
    for col in range(10000):
        for row in range(10000):
            pixel = image[row][col]  # Jump 40KB each time!
            total += pixel
    return total
```

**Questions:**

A. **Time complexity:**
   - Both: O(?)?
   - Same complexity, but which is faster?

B. **Cache line analysis:**
   - Cache line size: 64 bytes
   - Integer size: 8 bytes
   - One cache line holds: 8 integers
   - One row has: 10,000 integers

C. **Row-major access pattern:**
   ```
   image[0][0], image[0][1], image[0][2], ...
   ↑
   Sequential in memory!
   
   Load cache line at 0x1000:
   Contains: image[0][0..7]
   
   Next access image[0][1]: HIT! Already in cache
   Next access image[0][2]: HIT! Already in cache
   ...
   Next access image[0][8]: MISS, load new cache line
   ```
   
   Cache hit rate: 7/8 = 87.5%

D. **Column-major access pattern:**
   ```
   image[0][0], image[1][0], image[2][0], ...
   ↑
   Each is 40KB away in memory!
   
   Load cache line at 0x1000 (contains image[0][0])
   Next access image[1][0]: MISS! 40KB away, different cache line
   Next access image[2][0]: MISS! Another cache line
   ```
   
   Cache hit rate: Almost 0%

E. **Real performance:**
   - Row-major: 87.5% cache hits
     - Hits: 100M × 4ns = 400ms
     - Misses: 12.5M × 100ns = 1,250ms
     - Total: 1,650ms
   
   - Column-major: ~0% cache hits
     - All misses: 100M × 100ns = 10,000ms
     
   - Speedup: 10,000 / 1,650 ≈ **6x faster** with better cache locality!

---

**Solution 4.1:**

A. Both O(n²) where n=10,000
   But row-major is 6x faster due to cache!

B. Cache line: 64 bytes = 8 integers
   One row: 10,000 integers = 1,250 cache lines

C. Row-major: Sequential = 87.5% hit rate

D. Column-major: Jumpy (40KB apart) = ~0% hit rate

E. **Real speedup: 6x** - This is why memory layout matters!

---

#### Problem 4.2: Dynamic Array Growth Analysis

**Scenario:** Building a real-time analytics dashboard that logs events.

```python
events = []

# Incoming events: 1 event per millisecond
for i in range(1_000_000):
    event = create_event()
    events.append(event)  # What happens here?
```

**Questions:**

A. **Without doubling (naive allocation):**
   ```python
   capacity = 1
   for i in range(1_000_000):
       if len(events) == capacity:
           capacity += 1  # Add 1 element at a time
           reallocate()
   ```
   
   - How many reallocations? 1 million times!
   - How many copies? 1+2+3+...+1M = 500 billion copies!
   - Time per reallocation (assume 1 copy = 1 nanosecond):
     - Total: 500 billion ns = 500 seconds!

B. **With 2x doubling:**
   ```python
   capacity = 1
   for i in range(1_000_000):
       if len(events) == capacity:
           capacity *= 2  # Double capacity
           reallocate()
   ```
   
   - How many reallocations? log₂(1M) ≈ 20
   - How many copies? 1+2+4+8+...+512K = ~1M copies
   - Time: 1M ns = 1 millisecond!

C. **With 1.5x growth:**
   ```python
   capacity = 1
   for i in range(1_000_000):
       if len(events) == capacity:
           capacity = int(capacity * 1.5)  # 1.5x growth
           reallocate()
   ```
   
   - How many reallocations? log₁.₅(1M) ≈ 41
   - How many copies? Still O(n) = ~2M copies
   - Time: 2 milliseconds
   - Memory waste: ~33% (vs 50% for 2x)

D. **At real-time speed (1 event/ms):**
   - Naive: 500 seconds of copying = TOTALLY UNUSABLE
   - 2x doubling: 1 millisecond of copying = INVISIBLE
   - 1.5x: 2 milliseconds of copying = ACCEPTABLE

E. **When to choose which:**
   - Memory tight (embedded): 1.5x growth
   - Real-time requirement: 2x doubling
   - Unknown size: Don't pre-allocate
   - Fixed size known: Just allocate once

---

**Solution 4.2:**

A. Naive (add 1):
   - Reallocations: 1M
   - Copies: 500B
   - Time: 500 seconds (TERRIBLE!)

B. 2x doubling:
   - Reallocations: 20
   - Copies: 1M
   - Time: 1 millisecond (GREAT!)
   - Memory waste: 50%

C. 1.5x growth:
   - Reallocations: 41
   - Copies: 2M
   - Time: 2 milliseconds (GOOD!)
   - Memory waste: 33%

D. At real-time scale: 2x is invisible, naive is catastrophic

E. **Choice summary:**
   - Real-time or high-speed: 2x doubling (ignore memory waste)
   - Memory-constrained: 1.5x growth
   - Unknown growth: 2x is safer

---

### 🎯 PROBLEM SET 5: LINKED LIST VS ARRAY TRADE-OFFS

#### Problem 5.1: LRU Cache Implementation

**Scenario:** Implement cache for hot data (like browser).

**Design options:**

**Option A: Array + Linear Search**
```python
cache = []  # List of (key, value) tuples

def get(key):
    for i, (k, v) in enumerate(cache):  # O(n) search
        if k == key:
            # Move to front (most recently used)
            cache.pop(i)  # O(n) removal
            cache.insert(0, (k, v))  # O(n) insertion
            return v
    return None

def put(key, value):
    # Check if exists
    for i, (k, v) in enumerate(cache):
        if k == key:
            cache.pop(i)
            cache.insert(0, (k, v))
            return
    
    # Add new
    cache.insert(0, (k, value))
    if len(cache) > capacity:
        cache.pop()  # O(n) removal from end
```

**Option B: Linked List + HashMap**
```python
# Doubly linked list node
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

cache_map = {}  # HashMap for O(1) access
head = Node(0, 0)
tail = Node(0, 0)
head.next = tail
tail.prev = head

def get(key):
    if key not in cache_map:
        return None
    
    node = cache_map[key]
    # Move to front (most recently used)
    self.remove(node)  # O(1)
    self.add_to_front(node)  # O(1)
    return node.value

def remove(node):
    prev_node = node.prev
    next_node = node.next
    prev_node.next = next_node
    next_node.prev = prev_node

def add_to_front(node):
    node.next = head.next
    node.prev = head
    head.next.prev = node
    head.next = node
```

**Questions:**

A. **Time complexity for get():**
   - Option A: O(?)
   - Option B: O(?)

B. **Time complexity for put():**
   - Option A: O(?)
   - Option B: O(?)

C. **Time complexity for eviction (capacity exceeded):**
   - Option A: O(?)
   - Option B: O(?)

D. **For 1,000 cache accesses with 100 capacity:**
   - Option A: Total work?
   - Option B: Total work?
   - Speedup factor?

E. **Memory overhead:**
   - Option A: Just the data
   - Option B: data + 3 pointers per node
   - Which is worth it?

---

**Solution 5.1:**

A. **get():**
   - Option A: O(n) - linear search
   - Option B: O(1) - hashmap lookup

B. **put():**
   - Option A: O(n) - move to front requires O(n) ops
   - Option B: O(1) - all operations are O(1)

C. **Eviction:**
   - Option A: O(n) - remove from end
   - Option B: O(1) - just unlink node

D. **1,000 accesses:**
   - Option A: 1,000 × O(100) = O(100,000)
   - Option B: 1,000 × O(1) = O(1,000)
   - Speedup: 100x

E. **Memory trade-off:**
   - Option A: No overhead
   - Option B: 3 pointers × 8 bytes = 24 bytes per entry
   - For 100 entries: 2.4KB overhead
   - **100x speed for 2.4KB = WORTH IT!**

---

#### Problem 5.2: Streaming Data Processing

**Scenario:** Process streaming data (stock ticks) and calculate moving average.

```
Ticks arrive: 10, 20, 15, 25, 30, ...
Window size: 5
```

**Option A: Use Array**
```python
window = []

for tick in stream:
    window.append(tick)  # O(1) amortized
    if len(window) > 5:
        window.pop(0)  # O(n) - shift all elements!
    
    # Calculate average
    avg = sum(window) / len(window)
    print(f"Moving average: {avg}")
```

**Option B: Use Linked List**
```python
from collections import deque

window = deque(maxlen=5)  # Special double-ended queue

for tick in stream:
    window.append(tick)  # O(1)
    if len(window) == 5:
        window.popleft()  # O(1) - just unlink first node!
    
    # Calculate average
    avg = sum(window) / len(window)
    print(f"Moving average: {avg}")
```

**Questions:**

A. **Operation complexity:**
   - Array append: O(?)
   - Array popleft: O(?)
   - Deque append: O(?)
   - Deque popleft: O(?)

B. **For 1 million ticks:**
   - Array: 1M appends + 999,995 poplefts = ?
   - Deque: 1M appends + 999,995 poplefts = ?

C. **With large window (size 1000):**
   - Array popleft: shift 1000 elements = O(1000)
   - Deque popleft: unlink 1 node = O(1)
   - Per tick difference: 1000x slower with array

D. **Real-world consideration:**
   - Stock ticks: 5-10 million per day
   - Window sizes: 5-1000
   - Which would you choose?

---

**Solution 5.2:**

A. **Complexity:**
   - Array append: O(1) amortized
   - Array popleft: O(n) - must shift!
   - Deque append: O(1)
   - Deque popleft: O(1)

B. **1 million ticks:**
   - Array: 1M × O(1) + 999,995 × O(5) = O(1M + 5M) = O(6M)
   - Deque: 1M × O(1) + 999,995 × O(1) = O(2M)
   - Speedup: 3x with deque

C. **Large window (1000):**
   - Array: 999,995 × O(1000) = O(1 billion) operations!
   - Deque: 999,995 × O(1) = O(1M) operations
   - Speedup: **1000x**!

D. **Real-world choice:** Deque/linked list for streaming data
   - Large windows make array prohibitively slow
   - Linked list's O(1) operations shine

---

### 🎯 PROBLEM SET 6: BINARY SEARCH DEEP-DIVE

#### Problem 6.1: Finding Boundaries in Sorted Data

**Scenario:** E-commerce search for products with prices in a range.

```
Sorted prices: [10, 12, 15, 15, 15, 15, 20, 25, 30]
               [0   1   2   3   4   5   6   7   8]

Question: Find all products with price = 15
Answer: indices 2, 3, 4, 5 (range [2, 5])
```

**Questions:**

A. **Using standard binary search:**
   ```python
   def binary_search(arr, target):
       left, right = 0, len(arr) - 1
       while left <= right:
           mid = (left + right) // 2
           if arr[mid] == target:
               return mid  # Found, but which occurrence?
           elif arr[mid] < target:
               left = mid + 1
           else:
               right = mid - 1
       return -1
   ```
   
   Finding price 15 returns index 3 (one occurrence).
   But there are 4! How do you find all?

B. **Finding first occurrence:**
   ```python
   def find_first(arr, target):
       left, right = 0, len(arr) - 1
       result = -1
       while left <= right:
           mid = (left + right) // 2
           if arr[mid] == target:
               result = mid
               right = mid - 1  # Keep searching left
           elif arr[mid] < target:
               left = mid + 1
           else:
               right = mid - 1
       return result
   ```
   
   Finding first 15 returns index 2.
   Time: O(log n)

C. **Finding last occurrence:**
   Similar to above but search right when found.
   Finding last 15 returns index 5.
   Time: O(log n)

D. **Total products in range:**
   - First index: 2
   - Last index: 5
   - Count: 5 - 2 + 1 = 4 products

E. **At scale (10 million products):**
   - Standard binary search: O(log n) = 23 comparisons
   - Linear scan for all: O(n) = 10M comparisons
   - Using boundaries: 2 × O(log n) = 46 comparisons
   - Speedup: 216,000x faster!

---

**Solution 6.1:**

A. Standard binary search finds one, but need all occurrences

B. **Find first:**
   - When found, continue searching left
   - Track result
   - Returns leftmost index
   - Time: O(log n)

C. **Find last:**
   - When found, continue searching right
   - Returns rightmost index
   - Time: O(log n)

D. **Count:** last - first + 1 = 4

E. **Speedup:** 216,000x with boundary approach!
   - Invaluable for large datasets

---

#### Problem 6.2: Rotated Array Search

**Scenario:** You have a sorted array that's been rotated.

```
Original:  [1, 3, 4, 5, 7, 8, 9]
Rotated 3: [5, 7, 8, 9, 1, 3, 4]
           └─ rotation point
```

**Questions:**

A. **Can standard binary search find value 3?**
   - The array is NOT globally sorted
   - Binary search relies on sorted invariant
   - What happens if you try?

B. **Insight: Two sorted halves**
   - Left half: [5, 7, 8, 9] - sorted
   - Right half: [1, 3, 4] - sorted
   - Rotation point between them

C. **Modified binary search:**
   ```python
   def search_rotated(arr, target):
       left, right = 0, len(arr) - 1
       
       while left <= right:
           mid = (left + right) // 2
           if arr[mid] == target:
               return mid
           
           # Check which half is sorted
           if arr[left] <= arr[mid]:  # Left half sorted
               if arr[left] <= target < arr[mid]:
                   right = mid - 1  # Search left
               else:
                   left = mid + 1   # Search right
           else:  # Right half sorted
               if arr[mid] < target <= arr[right]:
                   left = mid + 1   # Search right
               else:
                   right = mid - 1  # Search left
       
       return -1
   ```
   
   Time: O(log n) even though array is rotated!

D. **Why this works:**
   - At each step, one half is always sorted
   - Compare target to sorted half's boundaries
   - Know which half to search
   - Still O(log n)!

E. **Comparison:**
   - Linear search: O(n)
   - Rotated binary search: O(log n)
   - Speedup: 50,000x for 1M elements!

---

**Solution 6.2:**

A. Standard binary search breaks because invariant violated

B. Insight: One half is always sorted after rotation

C. **Modified binary search:**
   - Check which half is sorted
   - Compare target to sorted half's range
   - Search appropriate half
   - Still O(log n)!

D. Why: One sorted half always available to guide search

E. **Speedup:** 50,000x vs linear!

---

## PART 3: SYNTHESIS PROBLEMS (Week 1 + 2 Combined)

### 🎯 PROBLEM SET 7: SYSTEM DESIGN CHALLENGES

#### Problem 7.1: Design High-Performance URL Shortener

```
Requirements:
- Generate short IDs for long URLs
- Store millions of URLs
- Retrieve original URL in <100ms
- 1,000 requests per second
```

**Design Decisions:**

A. **Data structure for URL storage:**
   - Option 1: Array
   - Option 2: Linked list
   - Option 3: Hash table
   - Which and why?

B. **Finding "hot" URLs:**
   - Some URLs accessed millions of times
   - Need to track access frequency
   - Use array of access counts?
   - Time to find most accessed: O(?)?

C. **Caching recently accessed:**
   - Keep top 1,000 URLs in fast cache
   - Need O(1) access and O(1) insertion
   - What data structure?

D. **Performance at scale:**
   - 1,000 requests/sec × 86,400 sec/day = 86 million/day
   - At this rate, how long to fill 1 million cache slots?
   - How long to fill 1 million hash table?

E. **Real-world complexity:**
   - URLs expire (need to remove old ones)
   - Still need O(1) access and O(1) deletion
   - Which data structure handles this best?

---

**Solution 7.1:**

A. **Hash table is best**
   - O(1) lookup
   - O(1) insertion
   - O(1) deletion

B. **Array of access counts:**
   - Finding max: O(n) linear scan
   - With hash table: still need to scan
   - Better: Use heap for tracking top 1000

C. **Fast cache:**
   - Doubly-linked list + hash map (LRU cache)
   - Like Problem 5.1
   - O(1) access and insertion

D. **Fill rate:**
   - 86M URLs/day for 1M slots = ~12 days

E. **Data structure:**
   - Hash table + doubly linked list
   - Hash for O(1) access
   - Linked for O(1) insertion/deletion
   - Combined: Best of both worlds!

---

## PART 4: PRACTICE ASSESSMENT

### Self-Assessment Checklist

**Week 1 Mastery:**
- [ ] Can calculate stack overflow risk (8MB / frame size)
- [ ] Can count recursion tree nodes and identify overlaps
- [ ] Can analyze Big O for nested loops (n², n log n, etc.)
- [ ] Can explain amortized analysis in simple terms
- [ ] Can identify when memoization helps (overlapping subproblems)

**Week 2 Mastery:**
- [ ] Can explain why cache locality matters (25x difference)
- [ ] Can calculate optimal array growth factor
- [ ] Can trace through linked list insertion/deletion
- [ ] Can implement monotonic stack conceptually
- [ ] Can explain why binary search is 33B times faster

**Combined Mastery:**
- [ ] Can choose right data structure for a problem
- [ ] Can estimate performance before coding
- [ ] Can identify performance bottlenecks
- [ ] Can explain real-world trade-offs
- [ ] Can solve real system design problems

---

## PART 5: CHALLENGE PROBLEMS

### 🎯 CHALLENGE 1: Stock Market Volatility

**Problem:**
Process 1 million stock ticks. For each tick, calculate:
1. Price change from previous tick
2. Moving average (last 20 ticks)
3. All-time high
4. Volatility (standard deviation of last 100 ticks)

Questions:
- Which data structure for each calculation?
- Time complexity per tick?
- Can you do this in <1ms per tick?

---

### 🎯 CHALLENGE 2: Social Network Recommendation

**Problem:**
Given 100 million users, find:
- Top 10 most-followed users
- Mutual friends between two users
- All friends of a friend not already connected
- Shortest path between two users

Questions:
- Which data structures?
- Time complexity for each operation?
- How to optimize at scale?

---

### 🎯 CHALLENGE 3: Real-Time Analytics Dashboard

**Problem:**
Process 100K events per second. Maintain:
- Count by event type (1000 types)
- Top 100 events
- Events in last 1 hour window
- Percentile calculations (95th, 99th)

Questions:
- How to handle streaming?
- How to efficiently maintain windows?
- How to calculate percentiles?

---

**SOLUTIONS PROVIDED ON REQUEST**

---

**Total Problems:** 30+ real-world scenarios
**Difficulty:** Beginner to Advanced
**Topics:** All Week 1-2 concepts
**Time to complete:** 20-30 hours
**Learning value:** Extremely high

These problems force you to apply concepts to real systems, not just academic examples!
