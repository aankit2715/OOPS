# Java Exceptions:  
In Java, an Exception is an event that occurs during program execution and disrupts the normal flow of a program. Exceptions are objects that inherit from the Throwable class.

- Java Exception Hierarchy:
```java
Object
 └── Throwable
      ├── Error
      │    ├── OutOfMemoryError
      │    ├── StackOverflowError
      │    └── VirtualMachineError
      │
      └── Exception
           ├── Checked Exceptions
           │    ├── IOException
           │    ├── SQLException
           │    ├── FileNotFoundException
           │    ├── ClassNotFoundException
           │    └── InterruptedException
           │
           └── RuntimeException (Unchecked)
                ├── NullPointerException
                ├── ArithmeticException
                ├── ArrayIndexOutOfBoundsException
                ├── NumberFormatException
                ├── ClassCastException
                ├── IllegalArgumentException
                └── IllegalStateException
```

**1. Checked Exceptions:**  
Checked exceptions are checked by the compiler at compile time.  
If a method can throw a checked exception, you must either:  
    - Handle it using try-catch
    - Declare it using throws  

Ex: 
```java
import java.io.*;

public class Main {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("abc.txt");
        } catch (FileNotFoundException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

- **1: Common Checked Exceptions (Compile time):**  

1. IOException:  
Occurs when input/output operation fails.
```java
Ex: FileReader file = new FileReader("test.txt");
```  

**Possible reasons:** 
    - File access issue
    - Network issue
    - Device failure

2. FileNotFoundException:  
Occurs when file does not exist.  
```java
Ex: FileReader file = new FileReader("missing.txt");
```  

3. SQLException:  
Occurs during database operations.  
```java
Ex: Connection con = DriverManager.getConnection(url);
```

**Possible causes:**  
    - Incorrect SQL query
    - Database unavailable
    - Invalid credentials  

4. ClassNotFoundException:  
Occurs when JVM cannot find specified class.  
```java
Ex: Class.forName("com.mysql.jdbc.Driver");
```

5. InterruptedException:  
Occurs when a thread is interrupted while sleeping or waiting.  

6. ParseException:  
Occurs when parsing date or text fails.  
Ex: 
```java
SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
sdf.parse("invalid-date");
```

- **2: Common Unchecked Exceptions (Runtime Exceptions)**  
Runtime exceptions occur during execution. Compiler does not force handling. They are subclasses of RuntimeException.  

1. NullPointerException (NPE):  
Most common exception. Occurs when calling methods on a null reference.  
Ex:
```java
String str = null;
System.out.println(str.length());
```

2. ArithmeticException:  
Occurs during illegal arithmetic operations.  
Ex: 
```java
int result = 10 / 0;
```  

3. ArrayIndexOutOfBoundsException:  
Occurs when accessing invalid array index.  
Ex:
```java
int[] arr = {1,2,3};
System.out.println(arr[5]);
```  

4. StringIndexOutOfBoundsException:  
Occurs when accessing invalid string index.  
Ex:
```java
String s = "Java";
char c = s.charAt(10);
```

5. NumberFormatException:  
Occurs when converting invalid string to number.  
Ex:
```java
int num = Integer.parseInt("ABC");
```

6. ClassCastException:  
Occurs when object type conversion is invalid.  
Ex:
```java
Object obj = "Java";
Integer i = (Integer)obj;
```

7. IllegalArgumentException:  
Thrown when a method receives unsuitable argument.  
Ex:
```java
Thread t = new Thread();
t.setPriority(20);
Priority should be between 1 and 10.
```

8. UnsupportedOperationException:  
Operation is not supported.  
Ex:
```java
List<Integer> list = Arrays.asList(1,2,3);
list.add(4);
```

9. ConcurrentModificationException:  
Occurs when collection is modified during iteration.  
Ex:
```java
ArrayList<String> list = new ArrayList<>();
list.add("A");
list.add("B");
for(String s : list){
    list.remove(s);
}
```

- **3: Errors**  
Errors indicate serious problems that applications generally should not handle. They are subclasses of Error.  

1. OutOfMemoryError:  
JVM runs out of memory.  
Ex:
```java
List<int[]> list = new ArrayList<>();

while(true){
    list.add(new int[1000000]);
}
```  

2. StackOverflowError:  
Occurs because of infinite recursion.  
Ex:
```java
public static void test() {
    test();
}
```

3. VirtualMachineError:  
Thrown when JVM resources are exhausted.  


# Exception Handling Keywords:

- **try:**  
Defines risky code block.  
Ex:
```java
try {
    int a = 10/0;
}
```
- **catch:**  
Handles exception.  
Ex:
```java
catch(Exception e){
    System.out.println(e.getMessage());
}
```

- **finally:**  
Always executes.  
Ex:
```java
try{
    System.out.println("Try");
}
finally{
    System.out.println("Finally");
}
```  

- **throw:**  
Used to explicitly throw exception.  
Ex:
```java
throw new ArithmeticException("Custom error");
```

- **throws:**  
Declares exception in method signature.  
Ex:
```java
public void readFile() throws IOException {
}
```

# Custom Exception:  
You can create your own exception by extending Exception.  
Ex:
```java
class InvalidAgeException extends Exception {

    public InvalidAgeException(String message) {
        super(message);
    }
}

Usage:
public class Main {

    static void validateAge(int age)
            throws InvalidAgeException {

        if(age < 18)
            throw new InvalidAgeException(
                "Age must be 18 or above");

        System.out.println("Eligible");
    }

    public static void main(String[] args) {

        try {
            validateAge(16);
        }
        catch(InvalidAgeException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

# Multiple Catch Blocks:

```java
try {
    int arr[] = new int[5];
    arr[10] = 50;
}
catch(ArrayIndexOutOfBoundsException e){
    System.out.println("Array Error");
}
catch(Exception e){
    System.out.println("General Error");
}
```

# Try-With-Resources (Java 7+):  
Absolutely. Try-With-Resources is one of the most important features introduced in Java 7 to automatically close resources like files, database connections, streams, sockets, etc.  
 
- Problem Before Try-With-Resources  
Ex: Suppose you're reading a file.  
```java
FileReader fr = null;

try {
    fr = new FileReader("data.txt");

    // Read file
}
catch (IOException e) {
    e.printStackTrace();
}
finally {
    try {
        if(fr != null) {
            fr.close();   // Must manually close
        }
    } catch(IOException e) {
        e.printStackTrace();
    }
}
```  

**Issues:**  
    - Too much boilerplate code.
    - Easy to forget close().
    - Resource leak if not closed.
    - Nested try-catch becomes messy.


- Solution: Try-With-Resources, Java automatically closes resources after use.
```java
try(FileReader fr = new FileReader("data.txt")) {

    // Read file

} catch(IOException e) {
    e.printStackTrace();
}
```

No finally block required. Java automatically executes:  
fr.close();

- Multiple Resources  
You can declare multiple resources inside one try block.  
Ex:
```java
try(
    FileReader fr =
        new FileReader("input.txt"); // To open file

    BufferedReader br =
        new BufferedReader(fr); // To read file
) {

    System.out.println(br.readLine());

}
catch(IOException e) {
    e.printStackTrace();
}
```

- Resource Closing Order:  
Resources are closed in reverse order.  
Ex:
```java
try(
    Resource1 r1 = new Resource1();
    Resource2 r2 = new Resource2();
) {
    System.out.println("Working");
}

Closing sequence:
r2.close()
r1.close()
```