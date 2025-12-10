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

# Java Collection Conversion  

# Java Collection Conversion Cheatsheet (2025+)

| # | From → To | Fastest & Cleanest One-Liner (2025+) | Notes / Real-World Use |
|---|-----------|----------------------------------------|-------------------------|
| 1 | List<E> → Set<E> | `new HashSet<>(list)` | Fastest way to remove duplicates |
| 2 | List<E> → LinkedHashSet<E> | `new LinkedHashSet<>(list)` | Maintain insertion order + deduplication |
| 3 | List<E> → E[] | `list.toArray(E[]::new)` | Type-safe array conversion |
| 4 | List<E> → int[] (if List<Integer>) | `list.stream().mapToInt(Integer::intValue).toArray()` | Used when API requires primitives |
| 5 | Set<E> → List<E> | `List.copyOf(set)` *(immutable)* or `new ArrayList<>(set)` *(mutable)* | Very common conversion |
| 6 | Set<E> → E[] | `set.toArray(E[]::new)` | Convert collection to array |
| 7 | Integer[] → List<Integer> | `List.of(arr)` *(immutable)* or `new ArrayList<>(Arrays.asList(arr))` | `List.of()` best for constants |
| 8 | Integer[] → Set<Integer> | `Set.of(arr)` *(immutable)* or `new HashSet<>(Arrays.asList(arr))` | `Set.of()` fails if duplicates exist |
| 9 | Integer[] → int[] | `Arrays.stream(arr).mapToInt(Integer::intValue).toArray()` | Unboxing conversion |
| 10 | int[] → List<Integer> | `Arrays.stream(arr).boxed().toList()` | Useful for JPA `IN` conditions |
| 11 | int[] → Integer[] | `Arrays.stream(arr).boxed().toArray(Integer[]::new)` | Needed for wrapper-based APIs |
| 12 | int[] → Set<Integer> | `Arrays.stream(arr).boxed().collect(Collectors.toSet())` | Dedup primitive array |
| 13 | String[] → List<String> | `List.of(arr)` or `Arrays.asList(arr)` | Same rules as Integer[] |
| 14 | List<Integer> → Integer[] | `list.toArray(Integer[]::new)` | Type-safe conversion |
| 15 | Set<Integer> → int[] | `set.stream().mapToInt(Integer::intValue).toArray()` | Rare conversion |
| 16 | int[] → LinkedHashSet<Integer> | `Arrays.stream(arr).boxed().collect(Collectors.toCollection(LinkedHashSet::new))` | Dedup + keep sorted insertion order |
| 17 | List<E> → Immutable List<E> | `List.copyOf(list)` | Best for returning safe objects |
| 18 | Set<E> → Immutable Set<E> | `Set.copyOf(set)` | Prevent external modification |
| 19 | Any Collection → Empty if null | `Optional.ofNullable(c).stream().flatMap(Collection::stream).toList()` | Defensive null-safety pattern |

