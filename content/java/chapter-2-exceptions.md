+++
date = '2026-08-21T00:07:08+05:30'
draft = false
title = 'Chapter 2 Exceptions'
categories = ["java"]
tags = ["java"]
+++

# Java Exceptions

## Checked/Unchecked
Check out this example code.
*(Ignore two classes in same file for now)*

```java
import java.util.Scanner;

public class Calculator {

    int a;
    
    void setNum(String s) throws NumberFormatException {
        a = Integer.parseInt(s);
    }

    public int getNum() {
        return a;
    }

}

public class Main {

    public static void main(String[] args) {
        Calculator calculator = new Calculator();
        Scanner scanner = new Scanner(System.in);
        try {
            calculator.setNum(scanner.next());
            int a = calculator.getNum();
            int b = Integer.parseInt(scanner.next());
            System.out.println(a/b);
        }
        catch (ArithmeticException e) {
            System.out.println("Error. Cannot divide by 0.");
        }
        catch (NumberFormatException e) {
            System.out.println("Please enter valid integers only.");
        }
        finally {
            System.out.println("End of program");
            scanner.close();
        }
    }
}
```

There are two types of exceptions in Java.
### 1. Checked Exceptions
   * Developer knows that the code may throw this error and adds provision for handling it.
   * These exceptions are derived from java.lang.Exception class, except RuntimeException and Error.
   * (Eg. - NumberFormatException in above code)
### 2. Unchecked Exceptions
   * These exceptions the not specified in method signature.
   * These exceptions are derived from java.lang.RuntimeException or java.lang.Error.
   * Eg. - ArithmeticException in above code

## Careful with **finally**
Check out this example:

```java
import java.util.InputMismatchException; 
import java.util.Scanner;

public class Calculator {
    int a;
    
    void setNum(String s) throws NumberFormatException {
        a = Integer.parseInt(s);
    }

    public int getNum() {
        return a;
    }

    public int parse(String s) {
        try {
            return Integer.parseInt(s);
        }
        catch (NumberFormatException e) {
            System.out.println("Please enter valid integers only.");
            return -1;
        }
        finally {
            System.out.println("End of program");
            return 0;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter a number:");
        int n = calculator.parse(scanner.next());
        System.out.println(n);
    }
}
```
In the above code, the final result will always be 0. Because **finally** will swallow other returns.
Use **finally** strictly for only cleanup and nothing else.