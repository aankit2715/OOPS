## What is the Collection Framework?

The Java Collection Framework (JCF) is a set of interfaces, classes, and algorithms in java.util package. that provide ready-made data structures (like lists, sets, maps) and methods to manipulate them. Instead of writing your own linked lists or hash tables, you use JCF’s implementations.

## Why do we use it?

- Efficiency: Provides optimized data structures.
- Reusability: Standardized interfaces across APIs.
- Flexibility: Easy to switch implementations (e.g., ArrayList vs LinkedList).
- Convenience: Built-in algorithms (sorting, searching, shuffling).

## Types of Collections
The framework is divided into four main categories:

# Types of Collections in Java

| **Type**                | **Interface**                        | **Examples**                                      | **Key Features**                                   |
|--------------------------|--------------------------------------|--------------------------------------------------|---------------------------------------------------|
| **List**                 | `List`                               | `ArrayList`, `LinkedList`, `Vector`              | Ordered, allows duplicates, index-based access    |
| **Set**                  | `Set`, `SortedSet`, `NavigableSet`   | `HashSet`, `TreeSet`, `LinkedHashSet`            | No duplicates, may be ordered/sorted              |
| **Queue**                | `Queue`, `Deque`, `BlockingQueue`    | `PriorityQueue`, `ArrayDeque`, `LinkedList`      | FIFO order, supports insertion/removal at ends    |
| **Map**                  | `Map`, `SortedMap`, `NavigableMap`   | `HashMap`, `TreeMap`, `LinkedHashMap`, `ConcurrentHashMap` | Key-value pairs, keys unique                      |
| **Concurrent Collections** | `ConcurrentMap`, `BlockingQueue`   | `ConcurrentHashMap`, `CopyOnWriteArrayList`      | Thread-safe, optimized for concurrency            |
