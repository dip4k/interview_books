# Week 2: Interview Q&A Reference

## 🎯 Arrays — 12 Q&A Pairs

**Q1: Why is array access O(1)?**
A: Direct addressing via arithmetic: address = base + index × element_size. Arithmetic is constant time, memory load is constant latency regardless of index.

**Q2: Why is insertion O(n)?**
A: Must shift all elements after insertion point one position right. Shifting n elements = n loads + n stores = O(n).

**Q3: What's the practical performance difference between array and list for sequential access?**
A: Arrays: 95% cache hit rate, 5ns per element. Lists: 5% cache hit rate, 200ns per element. **40-50x difference in practice!**

**Q4: Can you insert at the end of an array in O(1)?**
A: Static array: O(1) if space exists. Dynamic array: O(1) amortized (if you account for occasional resizing).

**Q5: How would you optimize repeated insertions at the beginning?**
A: Use circular buffer (deque) instead. O(1) insertion at both ends via pointer arithmetic, no shifting.

**Q6: What happens if you access arr[index] where index >= array.length?**
A: Undefined behavior in C/C++ (reads/writes garbage). RuntimeException in Java. IndexError in Python.

**Q7: Is array memory allocated contiguously?**
A: Yes. This is the defining property. Enables direct addressing and cache prefetching.

**Q8: How does cache prefetching work for arrays?**
A: CPU loads 64-byte cache line containing multiple elements. Sequential access hits prefetched data. Random access misses.

**Q9: Can you use an array for a problem requiring frequent middle deletions?**
A: Possible but inefficient (O(n) per delete). Use linked list instead if deletion heavy. Otherwise, use "swap-with-last" technique (O(1) amortized).

**Q10: What's the space complexity of an array?**
A: O(n) where n = number of elements. No overhead per element (unlike linked list which has pointer overhead).

**Q11: How do you find an element in an unsorted array?**
A: Linear search O(n). No better option without preprocessing (like sorting + binary search).

**Q12: Why might you choose an array over a hash table?**
A: Cache locality, simplicity, predictable performance, ordered access, less memory overhead.

---

## 🎯 Dynamic Arrays — 10 Q&A Pairs

**Q1: Why use exponential growth (2x) instead of linear growth (+k)?**
A: Exponential: O(log n) resizes, O(n) total cost. Linear: O(n/k) resizes, O(n²/k) total cost. Exponential is far better asymptotically.

**Q2: What's the amortized cost of appending n elements?**
A: Resizes at n=2,4,8,16,... Total copies: 1+2+4+...+2^(log n) ≈ 2n. Amortized per append: 2n/n = O(1).

**Q3: Does occasional O(n) pause matter for amortized O(1)?**
A: Depends on application. Amortized is good for average throughput. Real-time systems can't tolerate pauses → use preallocated arrays.

**Q4: What growth factor does C++ std::vector use?**
A: Typically 2x (doubling). Other libraries use 1.5x (slightly less waste).

**Q5: Why does Python use a more complex growth strategy?**
A: Aims to minimize memory waste while keeping amortized O(1). Starts small, grows adaptively.

**Q6: If capacity=100 and size=100, what happens when you append?**
A: Allocate new array (capacity=200). Copy 100 elements. Place new element. Total: ~300 memory operations.

**Q7: What's the typical memory waste for a dynamic array?**
A: Average 25% (capacity ranges from n to 2n, average 1.5n).

**Q8: Can you shrink a dynamic array to save memory?**
A: Yes, but rarely. Shrinking on deletion requires careful choice (don't shrink on every delete, or you get O(n²) behavior).

**Q9: Is std::vector or ArrayList always the right choice?**
A: For dynamic sequences, yes ~95% of time. Use deque for front insertion, list for heavy middle operations (rare).

**Q10: How does a growth factor of 1.5x compare to 2x?**
A: 1.5x: more frequent resizes (log_1.5(n) ≈ log_2(n) × 1.7), less memory waste. 2x: fewer resizes, more waste. 1.5x is often better in practice.

---

## 🎯 Linked Lists — 10 Q&A Pairs

**Q1: When should you use a linked list?**
A: Rarely. Only: (1) Undo/redo systems, (2) Memory allocators, (3) LRU caches (with hash map). 99% use arrays/vectors.

**Q2: Why is linked list access O(n)?**
A: Must follow n pointers from head. Each dereference = memory access = potential cache miss.

**Q3: Why is linked list insertion O(1) while array insertion is O(n)?**
A: List insertion: just relink pointers (O(1)). Array insertion: must shift all elements after position (O(n)).

**Q4: Why is linked list cache-unfriendly?**
A: Pointers scattered throughout memory. Each pointer dereference = memory load = potential cache miss (95% miss rate typically).

**Q5: How much memory overhead does a linked list have?**
A: One pointer per node (8 bytes on 64-bit). For small integers (4 bytes), overhead is 200%! For large data, overhead is small.

**Q6: Can you binary search a linked list?**
A: No. Requires random access. Only works on arrays (or skip lists, but rare).

**Q7: How do you efficiently delete from a linked list?**
A: If you have pointer to previous node: O(1) relink. If you only have target node: O(1) if you swap value, O(n) if you need actual deletion from chain.

**Q8: What's the difference between singly and doubly-linked list?**
A: Doubly: extra prev pointer, O(1) backward traversal, uses more memory. Singly: saves pointer, but can't traverse backward.

**Q9: Why is a circular buffer (deque) better for queue than linked list?**
A: Deque: O(1) enqueue/dequeue, cache-friendly, less memory. List: O(1) ops, but 50x slower due to cache.

**Q10: Would you ever use a linked list for a problem allowing dynamic array?**
A: No. Use array/vector instead. Better cache, simpler, standard, no pointer overhead.

---

## 🎯 Stacks — 8 Q&A Pairs

**Q1: What does LIFO mean?**
A: Last-In-First-Out. Last element pushed is first element popped.

**Q2: What's the real-world use of a stack?**
A: Function call stack (return addresses), undo/redo, expression parsing, DFS traversal.

**Q3: Why is push/pop O(1)?**
A: Both just update a single pointer (top index) and read/write one element. No shifting needed.

**Q4: Can you implement a stack using a linked list?**
A: Yes, push = insert at head (O(1)), pop = remove from head (O(1)). But use array instead (cache better).

**Q5: What happens if you pop from an empty stack?**
A: Exception (in most languages). Undefined behavior in C (depending on implementation).

**Q6: How would you implement a stack?**
A: Use array + top pointer. top initialized to -1. Push: buffer[++top] = x. Pop: return buffer[top--].

**Q7: What's the space complexity of a stack?**
A: O(n) where n = maximum depth of stack at any point.

**Q8: Could you use a queue for undo functionality?**
A: No. Undo should pop most recent action (LIFO). Queue would be FIFO (wrong order).

---

## 🎯 Queues — 8 Q&A Pairs

**Q1: What does FIFO mean?**
A: First-In-First-Out. First element enqueued is first element dequeued.

**Q2: What's the real-world use of a queue?**
A: Task scheduling, printer queue, BFS traversal, asynchronous task processing.

**Q3: Why is enqueue/dequeue O(1)?**
A: Both update pointers (front/rear) and read/write one element. No shifting needed.

**Q4: How do you implement a queue without shifting?**
A: Use circular buffer. Maintain front and rear pointers. Use modulo arithmetic: rear = (rear + 1) % capacity.

**Q5: What's the difference between a regular array queue and circular buffer?**
A: Regular: shifting required on dequeue (O(n)). Circular: no shifting, just pointer updates (O(1)).

**Q6: Can you implement a queue using two stacks?**
A: Yes. Stack1 for enqueue, Stack2 for dequeue. Dequeue = pop from Stack2 (or pop Stack1 and push to Stack2).

**Q7: What happens if you dequeue from an empty queue?**
A: Exception (in most languages). Check size before dequeuing.

**Q8: Why would you use a queue instead of a linked list for FIFO?**
A: Array-based queue (circular buffer) is faster: cache-friendly, less overhead. Same O(1) operations, but 50x faster.

---

## 🎯 Binary Search — 10 Q&A Pairs

**Q1: What's the time complexity of binary search?**
A: O(log n). Halve search space each iteration. After log₂(n) iterations, one element remains.

**Q2: What's the critical precondition for binary search?**
A: **Array MUST be sorted.** Unsorted array breaks algorithm (you'll skip target).

**Q3: What's the formula for middle index?**
A: mid = (left + right) / 2. Alternative: mid = left + (right - left) / 2 (avoids integer overflow for very large arrays).

**Q4: How many comparisons for binary search on 1 million elements?**
A: log₂(1,000,000) ≈ 20 comparisons. vs Linear search: 1,000,000 comparisons.

**Q5: Can you binary search a linked list?**
A: No. Linked list doesn't support O(1) random access. Need array (or skip list, but rare).

**Q6: What if the target is not in the array?**
A: Return -1 (or left/right pointer if you want insertion position).

**Q7: How do you avoid integer overflow in mid calculation?**
A: Use mid = left + (right - left) / 2 instead of mid = (left + right) / 2.

**Q8: What's the difference between binary search and ternary search?**
A: Ternary search divides into 3 parts. Still O(log₃(n)). Binary is simpler and equally good.

**Q9: Can you use binary search on partially sorted array?**
A: Depends. Basic binary search no. Modified versions exist for rotated/partially sorted (Week 4 problem).

**Q10: What's the space complexity of binary search?**
A: Iterative: O(1). Recursive: O(log n) (call stack).

---

## 🎯 Cross-Cutting Questions — 10 Q&A Pairs

**Q1: When would you choose array vs vector vs list?**
A: Array for fixed size (rare). Vector for unknown size (95% of cases). List for undo/redo, allocators, LRU cache (rare).

**Q2: How does cache behavior differ between array and list?**
A: Arrays: prefetching works (sequential), 95% hit rate. Lists: random memory, 5% hit rate. 40-50x performance difference.

**Q3: What's the biggest misconception about linked lists?**
A: "O(1) insertion makes them good for dynamic data." Reality: Finding position is O(n)! Total cost often O(n).

**Q4: Can you implement a set using an array?**
A: Yes (unsorted array), but inefficient for search (O(n)). Use hash set instead (O(1) average).

**Q5: Why does amortized analysis matter?**
A: Worst-case (O(n) resize) isn't representative. Amortized (O(1) average) shows typical behavior.

**Q6: What's the relationship between stacks, queues, and deques?**
A: Deque = Double-Ended Queue. Push/pop both ends O(1). Stack = deque with one end disabled. Queue = deque with specific order (FIFO).

**Q7: How would you optimize insertion at the front of an array?**
A: Use deque (double-ended queue). O(1) insertion at front. Or reverse thinking if possible.

**Q8: When should you worry about cache performance?**
A: Large data (n > 10,000). Tight loops. Performance-critical code. Most interviews: consider but don't obsess.

**Q9: What's the relationship between binary search and sorted arrays?**
A: Binary search requires sorted input. Sorting = O(n log n) preprocessing, then O(log n) searches.

**Q10: Why do you think Week 2 structures appear in Week 3-4?**
A: Sorting uses arrays. Hashing uses arrays + chaining (lists). Patterns build on these fundamentals. Week 2 is foundation for everything.

---

## ✅ Interview Readiness Checklist

After Week 2, you should confidently answer:
- [ ] 12 array questions
- [ ] 10 dynamic array questions
- [ ] 10 linked list questions
- [ ] 8 stack questions
- [ ] 8 queue questions
- [ ] 10 binary search questions
- [ ] 10 cross-cutting questions

**Total: 68 Q&A pairs mastered**

**If you can answer 90% confidently → ready for Week 3 interviews**

