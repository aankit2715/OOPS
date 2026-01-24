## Encapsulation

Encapsulation is one of the four pillars of Object-Oriented Programming (OOP).
It means wrapping data (variables/fields) and methods (functions) together into a single unit (class), and controlling access to that data using access modifiers.

In simple words:

    - Hide the internal details of how data is stored.
    - Expose only necessary operations through methods (getters/setters).
    - Prevent direct modification of fields from outside the class.

    ```java
    class Student {
    // Private fields (data hidden)
    private String name;
    private int age;

    // Public getter method (controlled access)
    public String getName() {
        return name;
    }

    // Public setter method (controlled access)
    public void setName(String name) {
        this.name = name;
    }

    // Getter for age
    public int getAge() {
        return age;
    }

    // Setter for age with validation
    public void setAge(int age) {
        if(age > 0) {
            this.age = age;
        } else {
            System.out.println("Age must be positive!");
        }
    }
}

public class EncapsulationExample {
    public static void main(String[] args) {
        Student s1 = new Student();

        // Accessing data via methods (not directly)
        s1.setName("Alice");
        s1.setAge(20);

        System.out.println("Name: " + s1.getName());
        System.out.println("Age: " + s1.getAge());

        // Trying invalid age
        s1.setAge(-5); // Will show validation message
    }
}
```

# 🎯 Summary

- Encapsulation = Data + Methods together in a class + Controlled access.
- It’s used for data hiding, security, maintainability, and flexibility.
- Achieved in Java by:
    - Making fields private.
    - Providing public getters and setters.