# Java Collection Types Comparison

| Collection Type | Ordered? | Allows Duplicates? | Allows Nulls? | Performance Notes | Best Real-World Use Case |
|-----------------|----------|--------------------|---------------|------------------|---------------------------|
| **ArrayList** | Yes (index-based) | Yes | Yes | Fast `get()` and iteration, slower inserts/removals (middle) | Default go-to list for most cases |
| **LinkedList** | Yes | Yes | Yes | Fast insert/remove at ends, slow `get()` due to traversal | Queue, frequent insert/remove operations |
| **HashSet** | No | No | Yes (1 null) | O(1) average for add/lookup | Removing duplicates, fast membership lookup |
| **LinkedHashSet** | Yes (insertion-order) | No | Yes | Slightly slower than HashSet | Unique data while preserving order |
| **TreeSet** | Yes (sorted) | No | No (unless custom comparator) | O(log n), slower than HashSet | Sorted and unique elements (ranking, leaderboard) |
| **CopyOnWriteArrayList** | Yes | Yes | Yes | Very slow writes, excellent concurrency for reads | Listener registry, event subscribers in multithreaded apps |
| **HashMap** | No | Keys: No duplicate, Values: Yes | 1 null key allowed | O(1) lookup | Fast key-value storage |
| **LinkedHashMap** | Yes (insertion order) | Keys: No duplicate | 1 null key allowed | Slight overhead vs HashMap | Caches, predictable iteration |
| **TreeMap** | Sorted (by key) | Keys: No duplicate | No for null keys | O(log n) | Sorted lookup and navigation |
| **ConcurrentHashMap** | No | Keys: No duplicate | Nulls NOT allowed | Thread-safe and fast under concurrency | High-performance concurrent caching |
| **PriorityQueue** | Partially ordered (heap-based) | Yes | No | Fast insert (`O(log n)`), fast `peek()` | Scheduling, job execution order |
| **ArrayDeque** | Yes | Yes | No | Faster than LinkedList for stack/queue ops | Stack/Queue replacement |
| **Vector** (legacy) | Yes | Yes | Yes | Thread-safe but slower | Avoid unless required by legacy code |
| **Stack** (legacy) | Yes (LIFO) | Yes | Yes | Uses Vector (slow) | Deprecated—use `ArrayDeque` instead |

