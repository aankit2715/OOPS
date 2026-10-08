
# String:  
Unlike primitive data types (int, char, double), String is a class from the java.lang package.  
Ex: String str = "Hello";  
Here:  
- String → Class name
- str → Reference variable
- "Hello" → String object

# Ways to Create String Objects:  

- **Method 1: Using String Literal**    
Ex:
```java
String s1 = "Java";
String s2 = "Java";
```  
Here, Java is a string literal like int x = 10; here, 10 is a int literal.  

**Memory Behavior**  
Java stores literals in a special memory area called the String Constant Pool (SCP). And it is maintained by the JVM to store String literals efficiently.  

**Reason:**  
Strings are immutable. If multiple variables contain the same text, Java can safely share one object instead of creating multiple copies.  

# Where is SCP stored?

- Before Java 7, String Pool was stored in: PermGen (Permanent Generation), which was a special JVM memory area.  
- Java 7 and later (including Java 8, 11, 17, 21): The String Pool is stored inside the Heap Memory.  

That's why s1==s2 return true. As both contains reference of same object.  

- **Method 2: Using new Keyword**  
Ex:
```java
String s1 = new String("Java");
String s2 = new String("Java");
```  

This creates:  
- One object in String Pool (if not present).  
- One object in Heap.  

So Here, s1==s2 return false, As refernces are different because s1, s2 pointing to different objects.  
Ex:
```java
String s1 = "Java";
String s2 = "Java";
String s3 = new String("Java");

String Pool
 └── "Java"

Heap
 └── String object ("Java") 
```   
So, here s1 and s2 point to pool object. s3 points to heap object.

# Why String is Immutable?  
A String object cannot be modified after creation.  

Ex: 1
```java
String s = "Java";
s.concat(" Programming");
System.out.println(s);

output: Java
```  
The original string remains unchanged.  

- If you want modification:
Ex: 2
```java
s = s.concat(" Programming");
System.out.println(s);

output: Java Programming
```  

# Advantages of Immutability:

- **Security**    
Used in:  
1. Database URLs
2. Network connections
3. File paths  
They cannot be changed accidentally.  

- **Thread Safety**  
Multiple threads can safely access String objects.  


# Comparing Strings:

- **Using == Operator:**  
Ex: 1
```java
String s1 = "Java";
String s2 = "Java";
System.out.println(s1 == s2);

Output: true
```  
Ex: 2
```java
String s1 = new String("Java");
String s2 = new String("Java");
System.out.println(s1 == s2);

Output:false
```  

- **Using equals():**  
Ex:
```java
String s1 = new String("Java");
String s2 = new String("Java");
System.out.println(s1.equals(s2));

Output: true (Here we comparing strings not refernces)
```




 
