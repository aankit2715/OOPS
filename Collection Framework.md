## What is the Collection Framework?

The Java Collection Framework (JCF) is a set of interfaces, classes, and algorithms in java.util package. that provide ready-made data structures (like lists, sets, maps) and methods to manipulate them. Instead of writing your own linked lists or hash tables, you use JCF’s implementations.

## Why do we use it?

- Efficiency: Provides optimized data structures.
- Reusability: Standardized interfaces across APIs.
- Flexibility: Easy to switch implementations (e.g., ArrayList vs LinkedList).
- Convenience: Built-in algorithms (sorting, searching, shuffling).

## Types of Collections
The framework is divided into four main categories:

classDiagram
    class List {
        +Ordered
        +Allows duplicates
        +Index-based access
        Examples: ArrayList, LinkedList, Vector
    }

    class Set {
        +No duplicates
        +May be ordered/sorted
        Examples: HashSet, TreeSet, LinkedHashSet
    }

    class Queue {
        +FIFO order
        +Insertion/removal at ends
        Examples: PriorityQueue, ArrayDeque, LinkedList
    }

    class Map {
        +Key-value pairs
        +Keys unique
        Examples: HashMap, TreeMap, LinkedHashMap, ConcurrentHashMap
    }

    class ConcurrentCollections {
        +Thread-safe
        +Optimized for concurrency
        Examples: ConcurrentHashMap, CopyOnWriteArrayList
    }

    %% Relationships
    Collection <|-- List
    Collection <|-- Set
    Collection <|-- Queue
    Collection <|-- Map
    Collection <|-- ConcurrentCollections


