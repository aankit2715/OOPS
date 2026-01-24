# Java Basics:
 
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}

## public static void main(String[] args): 
This is the entry point.

## public: 
Access modifier, means it can be accessed from anywhere.

## static: 
It can be run without creating an object of the class.
Example:
```java
class MathUtils {

    // Instance method (not static)
    int square(int x) {
        return x * x;
    }

    // Static method 
    static int squareRoot(int x) { 
        return ; 
    }
}


public class Main {

    public static void main(String[] args) {

        // Calling static method without creating object
        int result1 = MathUtils.squareRoot(5);

        // ❌ This will NOT work:
        int result2 = MathUtils.square(5);

        // ✅ Correct way: create an object first
        MathUtils utils = new MathUtils();
        int result3 = utils.square(5);

        System.out.println("Square: " + result);
    }
}
```

## void: 
It does not return any value.
 
## String[] args: 
Command line arguments. We can pass inputs to the program when running it from the command line.

Example:
```java
public class CommandLineExample {

    public static void main(String[] args) {

        // Check if arguments are provided
        if (args.length > 0) {

            System.out.println("Arguments passed:");

            for (int i = 0; i < args.length; i++) {

                System.out.println("args[" + i + "]: " + args[i]);
            }
        } else {

            System.out.println("No arguments passed!");
        }
    }
}
```

## String:
Strings are objects in Java, not primitives. They store text.

Immutable: Once created, a String object cannot be changed. Modifying it creates a new object.

## String Declarations in Java

1. String Literal
```java
    String s1 = "Hello";   
```
- Stored in the String pool.
- Reused if another literal "Hello" is declared.

2. Using new Keyword
```java
    String s2 = new String("Hello");
```
- Creates a new object in heap memory, even if "Hello" already exists in the pool.

3. String from char[]
```java
    char[] chars = {'J', 'a', 'v', 'a'};
    String s5 = new String(chars);
```
- Converts a character array into a String.

4. String from byte[]
```java
    byte[] bytes = {65, 66, 67}; // ASCII values for A, B, C
    String s6 = new String(bytes);
```
- Converts byte array into a String ("ABC").

5. StringBuilder / StringBuffer (Mutable)
```java
    StringBuilder sb = new StringBuilder("Hello");
    sb.append(" World");
    System.out.println(sb.toString()); // "Hello World"
```
- Unlike String, these are mutable (can be changed without creating new objects).

6. String to Char Array
```java
    String str = "World";
    char[] arr3 = str.toCharArray();
```

## Scanner class vs BufferedReader class

- For input, we use the Scanner class or BufferedReader class.

| Aspect              | Scanner Class (`java.util`)                          | BufferedReader Class (`java.io`)                  |
|---------------------|------------------------------------------------------|--------------------------------------------------|
| Ease of Use         | Provides built-in methods like `nextInt()`, `nextDouble()`, `nextLine()` for parsing input directly. | Only reads text as strings; you must manually parse into other types. |
| Performance         | Slower due to parsing overhead and tokenization.     | Faster because it uses efficient buffering.       |
| Buffer Size         | Smaller buffer.                                      | Larger buffer → better performance for bulk input.|
| Thread Safety       | Not thread-safe.                                     | Thread-safe.                                     |
| Use Case            | Best for simple console input where you know the data type (e.g., reading numbers, words). | Best for reading large text files or streams efficiently. |
| Package             | `java.util`                                          | `java.io`                                        |

- Example with Scanner:
```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int num = sc.nextInt();
        System.out.println("You entered: " + num);
    }
}
```

- Example with BufferedReader:
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class BufferedReaderExample {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.out.print("Enter a line: ");
        String line = br.readLine();
        System.out.println("You entered: " + line);
    }
}
```

## Professional Recommendation

- Use Scanner → for small programs, console input, and when parsing different data types is needed  quickly.

- Use BufferedReader → for performance-critical applications, reading large files, or when working with streams.

## Type Casting

- Type casting is the process of converting a value from one data type to another. In Java, there are two main types of casting:

1. Implicit Casting (Widening Conversion)

- Occurs automatically when a smaller data type is assigned to a larger data type.  
- Example: converting int to double.

```java
int myInt = 9;
double myDouble = myInt; // Implicit casting: int → double
System.out.println(myDouble); // Output: 9.0
```

2. Explicit Casting (Narrowing Conversion)

- Must be done manually by the programmer using parentheses. Used when converting a larger data type to a smaller one.
- May cause data loss (e.g., fractional part is discarded when converting double to int).

```java
double myDouble = 9.78;
int myInt = (int) myDouble; // Explicit casting: double → int
System.out.println(myInt); // Output: 9 (fraction lost)
```



