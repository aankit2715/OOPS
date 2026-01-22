##Java Basics:

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}

#public static void main(String[] args): 
This is the entry point.

#public: 
Access modifier, means it can be accessed from anywhere.

#static: 
It can be run without creating an object of the class.
Example:

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

#void: 
It does not return any value.
 
#String[] args: 
Command line arguments. We can pass inputs to the program when running it from the command line.

Example:

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
