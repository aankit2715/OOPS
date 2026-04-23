## What is the Collection Framework?

The Java Collection Framework (JCF) is a set of interfaces, classes, and algorithms in java.util package. that provide ready-made data structures (like lists, sets, maps) and methods to manipulate them. Instead of writing your own linked lists or hash tables, you use JCF’s implementations.

## Why do we use it?

- Efficiency: Provides optimized data structures.
- Reusability: Standardized interfaces across APIs.
- Flexibility: Easy to switch implementations (e.g., ArrayList vs LinkedList).
- Convenience: Built-in algorithms (sorting, searching, shuffling).

## Types of Collections in Java
The framework is divided into four main categories:

| **Type**       | **Interface**       | **Examples (Classes)**                     | **Key Use**                                                   |
|----------------|---------------------|--------------------------------------------|---------------------------------------------------------------|
| **List**       | List                | ArrayList, LinkedList, Vector              | Ordered, allows duplicates, indexed access                     |
| **Set**        | Set                 | HashSet, LinkedHashSet, TreeSet            | No duplicates, unordered (except TreeSet which is sorted)      |
| **Queue/Deque**| Queue, Deque        | PriorityQueue, ArrayDeque, LinkedList      | FIFO/LIFO ordering, supports priority-based retrieval          |
| **Map**        | Map                 | HashMap, TreeMap, LinkedHashMap, Hashtable | Key-value pairs, keys unique, values can repeat                |
