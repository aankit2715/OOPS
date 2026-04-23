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

1. ArrayList Example (👉 Best for fast random access.)

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
- CopyOnWriteArrayList → safe alternative to ArrayList for read-heavy workloads.
- ConcurrentLinkedQueue → safe queue for concurrent producers/consumers.

## ✅ Summary: When to Use Which

- List → Ordered, allows duplicates. Use when you need indexed access.
- Set → Unique elements. Use when duplicates are not allowed.
- Queue/Deque → FIFO/LIFO or priority-based tasks. Use for scheduling, buffering.
- Map → Key-value pairs. Use when you need fast lookups by key.
- Concurrent Collections → Use in multi-threaded apps to avoid synchronization issues.

## iterator

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

- Intermediate operations (return another Stream, can be chained):
* filter() → keep only elements that match a condition.
* map() → transform each element.
* sorted() → sort elements.
* distinct() → remove duplicates.

- Terminal operations (end the pipeline, produce a result):
* forEach() → loop through and perform an action.
* collect() → gather results into a collection.
* reduce() → combine elements into a single result (like sum).

- Optional short-circuiting operations:
* findFirst(), anyMatch(), allMatch() → stop early when condition is met.

- 🔹 Example: Salaries with Streams

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




 

