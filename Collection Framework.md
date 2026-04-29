## What is the Collection Framework?

The Java Collection Framework (JCF) is a set of interfaces, classes, and algorithms in java.util package. that provide ready-made data structures (like lists, sets, maps) and methods to manipulate them. Instead of writing your own linked lists or hash tables, you use JCF’s implementations.

## Why do we use it?

- Efficiency: Provides optimized data structures.
- Reusability: Standardized interfaces across APIs.
- Flexibility: Easy to switch implementations (e.g., ArrayList vs LinkedList).
- Convenience: Built-in algorithms (sorting, searching, shuffling).

## Types of Collections in Java
The framework is divided into four main categories:

| **Type**          | **Interface**       | **Examples (Classes)**                                   | **Key Use**                                                                 |
|-------------------|---------------------|----------------------------------------------------------|------------------------------------------------------------------------------|
| **List**          | List                | ArrayList, LinkedList, Vector                            | Ordered, allows duplicates, indexed access                                   |
| **Set**           | Set                 | HashSet, LinkedHashSet, TreeSet                          | No duplicates, unordered (except TreeSet which is sorted)                    |
| **Queue/Deque**   | Queue, Deque        | PriorityQueue, ArrayDeque, LinkedList                    | FIFO/LIFO ordering, supports priority-based retrieval                        |
| **Map**           | Map                 | HashMap, TreeMap, LinkedHashMap, Hashtable               | Key-value pairs, keys unique, values can repeat                              |
| **Concurrent**    | Concurrent Interfaces| ConcurrentHashMap, CopyOnWriteArrayList, ConcurrentLinkedQueue | Thread-safe collections for multi-threaded environments, avoid synchronization issues |

1. ArrayList Example (👉 Best for fast random access.) -> Dynamic Resizing
- ArrayList allows dynamic storage and retrieval of elements. Unlike regular arrays, its size can grow or shrink automatically as elements are added or removed. 
- Allows duplicates and null values.
- Not synchronized means not thread-safe. If multiple threads modify it at the same time, data corruption or unexpected behavior can occur. Since it’s not synchronized, the internal array may resize while another thread is writing, leading to race conditions or even ConcurrentModificationException.

```java
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        // Adding elements
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        // Accessing elements
        System.out.println("First element: " + list.get(0));

        // Iterating
        for (String fruit : list) {
            System.out.println(fruit);
        }
    }
}
```

2. LinkedList Example (👉 Best for frequent insertions/deletions.)

- Doubly-linked structure: Each node has references to both the previous and next node.
- It maintains insertion order (the order in which you add elements).
- Implements multiple interfaces: List, Deque, Queue, Iterable, Cloneable, Serializable.
- Allows null elements and duplicates.
- Not synchronized: Must be externally synchronized for multi-threaded use.

```java
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();

        // Adding elements
        list.add("Dog");
        list.add("Cat");
        list.add("Horse");

        // Adding at specific positions
        list.addFirst("Elephant");
        list.addLast("Tiger");

        // Iterating
        for (String animal : list) {
            System.out.println(animal);
        }
    }
}
```

3. Vector Example (👉 Thread-safe, but slower than ArrayList.)

- Dynamic resizing: Like ArrayList, it grows or shrinks automatically.
- Synchronized: All methods are synchronized, making it safe for concurrent access.
- Allows duplicates and null values.

```java
import java.util.Vector;

public class VectorDemo {
    public static void main(String[] args) {
        Vector<Integer> numbers = new Vector<>();

        // Adding elements
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);

        // Accessing elements
        System.out.println("Element at index 1: " + numbers.get(1));

        // Iterating
        for (int num : numbers) {
            System.out.println(num);
        }
    }
}
```

4. Stack Example (extends Vector / 👉 Best for LIFO operations (like undo/redo).)

```java
import java.util.Stack;

public class StackDemo {
    public static void main(String[] args) {
        Stack<String> stack = new Stack<>();

        // Push elements
        stack.push("First");
        stack.push("Second");
        stack.push("Third");

        // Pop element
        System.out.println("Popped: " + stack.pop());

        // Peek element
        System.out.println("Top element: " + stack.peek());
    }
}
```

## 🔹 Why Use the List Interface Directly?

✅ Key Difference

- Concrete class declaration → You tie your code to one implementation. Switching means changing variable types, imports, and possibly method signatures.
```java
ArrayList<String> fruits = new ArrayList<>();
```

- Interface declaration → You tie your code to the contract (List). Switching only requires changing the new ArrayList<>(); part to new LinkedList<>();. All your method calls remain valid because they belong to the List interface.
```java
List<String> fruits = new ArrayList<>();
```

```java
import java.util.List;
import java.util.ArrayList;
import java.util.LinkedList;

public class InterfaceDemo {
    public static void main(String[] args) {
        // Variable type is List (interface)
        List<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");

        System.out.println(fruits.get(0));

        // Later, if you want LinkedList instead:
        fruits = new LinkedList<>(); // only change the right-hand side
        fruits.add("Mango");
        fruits.add("Orange");

        // Same code still works because both ArrayList and LinkedList implement List
        for (String f : fruits) {
            System.out.println(f);
        }
    }
}
```

## Other Collection Frameworks Details with Example:

1. Set

- HashSet:
1. Implements Set interface → Ensures uniqueness of elements.
2. Backed by HashMap → Uses hashing for fast lookups.
3. No ordering guarantee → Iteration order is not fixed and may change.
4. Allows null → Only one null element is permitted.
5. Not synchronized → Must be wrapped with Collections.synchronizedSet() for thread safety.

- LinkedHashSet: is a special type of Set that combines the features of a HashSet with a linked list to maintain insertion order.
1. Implements Set interface → Stores unique elements only.
2. Maintains insertion order → Unlike HashSet, iteration order is predictable.
3. Backed by LinkedHashMap → Uses hashing for fast lookups and a linked list for order.
4. Allows one null element.
5.  Not synchronized → Needs external synchronization for multi-threaded use.

- TreeSet: TreeSet is a collection that stores unique elements in a sorted order using a self-balancing binary search tree.
1. Implements NavigableSet and SortedSet → Ensures elements are unique and sorted.
2. Ordering → Maintains elements in ascending order by default, or by a custom Comparator.
3. No duplicates allowed → Each element must be unique.
4. Allows null? → Only if the set is empty and no comparator is used; otherwise throws NullPointerException.
5. Not synchronized → Needs external synchronization for multi-threaded use.


```java
import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.TreeSet;

public class SetDemo {
    public static void main(String[] args) {
        // HashSet: fast, no order
        HashSet<String> hashSet = new HashSet<>();
        hashSet.add("Apple");
        hashSet.add("Banana");
        hashSet.add("Apple"); // duplicate ignored
        System.out.println("HashSet: " + hashSet);

        // LinkedHashSet: maintains insertion order
        LinkedHashSet<String> linkedSet = new LinkedHashSet<>();
        linkedSet.add("Dog");
        linkedSet.add("Cat");
        linkedSet.add("Horse");
        System.out.println("LinkedHashSet: " + linkedSet);

        // TreeSet: sorted order
        TreeSet<String> treeSet = new TreeSet<>();
        treeSet.add("Zebra");
        treeSet.add("Lion");
        treeSet.add("Elephant");
        System.out.println("TreeSet: " + treeSet);
    }
}
```
👉 Use Set when you need unique elements.

- HashSet → fastest, no order.
- LinkedHashSet → preserves insertion order.
- TreeSet → keeps elements sorted.

2. Queue / Deque

```java
import java.util.PriorityQueue;
import java.util.ArrayDeque;
import java.util.LinkedList;

public class QueueDemo {
    public static void main(String[] args) {
        // PriorityQueue: elements ordered by priority (natural order by default)
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        pq.add(30);
        pq.add(10);
        pq.add(20);
        System.out.println("PriorityQueue: " + pq.poll()); // smallest element first

        // ArrayDeque: fast double-ended queue
        ArrayDeque<String> deque = new ArrayDeque<>();
        deque.addFirst("First");
        deque.addLast("Last");
        System.out.println("ArrayDeque: " + deque);

        // LinkedList as Queue
        LinkedList<String> queue = new LinkedList<>();
        queue.offer("Task1");
        queue.offer("Task2");
        System.out.println("LinkedList Queue: " + queue.poll()); // FIFO
    }
}
```

👉 Use Queue/Deque when you need FIFO/LIFO ordering or priority-based retrieval.

- PriorityQueue → tasks sorted by priority.
- ArrayDeque → efficient stack/queue replacement.
- LinkedList → flexible queue with fast insertions.

3. Map

- HashMap: HashMap is a collection that stores key–value pairs using hashing. It allows fast access to values based on their keys.
1. Implements Map interface → Stores data as key–value pairs.
2. Unique keys → Each key can map to only one value.
3. Allows one null key and multiple null values.
4. No ordering guarantee → Keys and values are not stored in insertion or sorted order.
5. Not synchronized → Must be wrapped with Collections.synchronizedMap() for thread safety.

- LinkedHashMap: 
1. Order preservation: Iteration order is predictable (insertion order by default).
2. Performance: Similar to HashMap → O(1) average for put, get, remove.
3. Nulls allowed: One null key and multiple null values.
4. Access-order mode: If constructed with accessOrder = true, it maintains order based on last access (useful for LRU caches).
5. Not synchronized: Like HashMap, it’s not thread-safe unless wrapped.

- TreeMap:
1. Sorted order: Keys are always sorted (ascending by default).
2. Performance:
    - put, get, remove → O(log n) because of tree operations.
    - Slower than HashMap (which is O(1) average), but provides ordering.
3. Nulls:
    - Does not allow null keys (throws NullPointerException).
    - Allows multiple null values.

```java
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.TreeMap;
import java.util.Hashtable;

public class MapDemo {
    public static void main(String[] args) {
        // HashMap: fast, no order
        HashMap<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Apple", 100);
        hashMap.put("Banana", 200);
        System.out.println("HashMap: " + hashMap);

        // LinkedHashMap: maintains insertion order
        LinkedHashMap<String, Integer> linkedMap = new LinkedHashMap<>();
        linkedMap.put("Dog", 1);
        linkedMap.put("Cat", 2);
        System.out.println("LinkedHashMap: " + linkedMap);

        // TreeMap: sorted by keys
        TreeMap<String, Integer> treeMap = new TreeMap<>();
        treeMap.put("Zebra", 10);
        treeMap.put("Lion", 20);
        System.out.println("TreeMap: " + treeMap);

        // Hashtable: legacy, synchronized
        Hashtable<String, Integer> table = new Hashtable<>();
        table.put("Key1", 111);
        table.put("Key2", 222);
        System.out.println("Hashtable: " + table);
    }
}
```

👉 Use Map when you need key-value pairs.

- HashMap → fastest, no order.
- LinkedHashMap → preserves insertion order.
- TreeMap → sorted by keys.
- Hashtable → legacy, thread-safe.

4. Concurrent Collections

```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.CopyOnWriteArrayList;
import java.util.concurrent.ConcurrentLinkedQueue;

public class ConcurrentDemo {
    public static void main(String[] args) {
        // ConcurrentHashMap: thread-safe map
        ConcurrentHashMap<String, Integer> concurrentMap = new ConcurrentHashMap<>();
        concurrentMap.put("A", 1);
        concurrentMap.put("B", 2);
        System.out.println("ConcurrentHashMap: " + concurrentMap);

        // CopyOnWriteArrayList: thread-safe list, good for read-heavy scenarios
        CopyOnWriteArrayList<String> cowList = new CopyOnWriteArrayList<>();
        cowList.add("Alpha");
        cowList.add("Beta");
        System.out.println("CopyOnWriteArrayList: " + cowList);

        // ConcurrentLinkedQueue: non-blocking queue
        ConcurrentLinkedQueue<String> clq = new ConcurrentLinkedQueue<>();
        clq.add("Task1");
        clq.add("Task2");
        System.out.println("ConcurrentLinkedQueue: " + clq.poll());
    }
}
```
👉 Use Concurrent Collections in multi-threaded environments.

- ConcurrentHashMap → safe alternative to HashMap.
    - Splits the map into segments/buckets.
    - Only locks the bucket being modified, not the entire map → much faster than synchronizing the whole map.
    - Iterators are fail-safe (they don’t throw exceptions if the map changes during iteration, but may not reflect the latest updates immediately).
    
- CopyOnWriteArrayList → safe alternative to ArrayList for read-heavy workloads.
- ConcurrentLinkedQueue → safe queue for concurrent producers/consumers.

## ✅ Summary: When to Use Which

- List → Ordered, allows duplicates. Use when you need indexed access.
- Set → Unique elements. Use when duplicates are not allowed.
- Queue/Deque → FIFO/LIFO or priority-based tasks. Use for scheduling, buffering.
- Map → Key-value pairs. Use when you need fast lookups by key.
- Concurrent Collections → Use in multi-threaded apps to avoid synchronization issues.

## Iterator

- Use for-each loop when you just need to read values.
- Use Iterator when you need to remove or modify elements while traversing, or when working with collections where index access isn’t available (like Set).

```java
import java.util.ArrayList;
import java.util.Iterator;

public class IteratorDemo {
    public static void main(String[] args) {
        ArrayList<Integer> salary = new ArrayList<>();
        salary.add(1000);
        salary.add(2000);
        salary.add(3000);
        salary.add(4000);

        Iterator<Integer> it = salary.iterator();
        while (it.hasNext()) {
            Integer s = it.next();
            if (s < 3000) {
                it.remove(); // safely remove while iterating
            }
        }

        System.out.println("Remaining salaries: " + salary);
    }
}
```

## Streams:
Streams were introduced in Java 8 (2014). Before that, you only had loops (for, while, Iterator) to process collections. Streams brought a functional programming style to Java, making collection processing more concise, expressive, and powerful.

Streams don’t store data; they just provide a pipeline to process it.

## 🔹 Key Operations
Streams have three main categories of operations:

-- Intermediate operations (return another Stream, can be chained):
* filter() → keep only elements that match a condition.
* map() → transform each element.
* sorted() → sort elements.
* distinct() → remove duplicates.

-- Terminal operations (end the pipeline, produce a result):
* forEach() → loop through and perform an action.
* collect() → gather results into a collection.
* reduce() → combine elements into a single result (like sum).

-- Optional short-circuiting operations:
* findFirst(), anyMatch(), allMatch() → stop early when condition is met.

 🔹 Example: Salaries with Streams

```java
import java.util.*;
import java.util.stream.*;

public class StreamDemo {
    public static void main(String[] args) {
        List<Integer> salary = Arrays.asList(1000, 2000, 3000, 4000);

        // Print all salaries
        salary.stream()
              .forEach(s -> System.out.println("Salary: " + s));

        // Filter: print only salaries > 2000
        salary.stream()
              .filter(s -> s > 2000)
              .forEach(s -> System.out.println("High Salary: " + s));

        // Map: increase each salary by 10%
        salary.stream()
              .map(s -> s * 110 / 100)
              .forEach(s -> System.out.println("Increased Salary: " + s));

        // Reduce: calculate total salary
        int total = salary.stream()
                          .reduce(0, (sum, s) -> sum + s);
        System.out.println("Total Salary: " + total);
    }
}
```


## Java 8 features: Streams, lambdas, Optional, functional interfaces

1. Streams
    - A Stream is a pipeline to process collections in a functional style.
    - Supports operations like filter, map, reduce, collect.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// Pipeline: filter → map → collect
List<String> result = names.stream()
                           .filter(n -> n.length() > 3)   // keep names longer than 3
                           .map(String::toUpperCase)      // convert to uppercase
                           .sorted()                      // sort alphabetically
                           .toList();                     // collect into list

System.out.println(result);
Output:
[ALICE, CHARLIE, DAVID]
```

2. Lambdas
    - A lambda expression is a concise way to represent an anonymous function.
    - Syntax: (parameters) -> expression.

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4);

// Traditional anonymous class
nums.forEach(new java.util.function.Consumer<Integer>() {
    public void accept(Integer n) {
        System.out.println(n * 2);
    }
});

// Lambda equivalent
nums.forEach(n -> System.out.println(n * 2));
```

3. Optional
    - Optional is a container object to avoid null checks and NullPointerException.
    - Provides methods like isPresent(), orElse(), ifPresent().

```java
Optional<String> name = Optional.ofNullable(null);

// Safe handling
if (name.isPresent()) {
    System.out.println("Name: " + name.get());
} else {
    System.out.println("No name provided");
}

// Cleaner way
name.ifPresent(n -> System.out.println("Name: " + n));
System.out.println(name.orElse("Default Name"));
```

4. Functional Interfaces
    - An interface with exactly one abstract method.
    - Examples: Runnable, Callable, Comparator, Function, Predicate.
    - Annotated with @FunctionalInterface.

```java
@FunctionalInterface
interface Greeting {
    void sayHello(String name);
}

public class Demo {
    public static void main(String[] args) {
        Greeting g = (n) -> System.out.println("Hello, " + n);
        g.sayHello("Alice");
    }
}
```
 





 

