+++
date = '2026-08-19T11:47:14+05:30'
draft = false
title = 'Chapter 1 Intro'
categories = ["java"]
tags = ["java"]
+++

### Exception Handling
#### Checked and Unchecked Exceptions
1. Checked - code calls a method that throws a checked exception, code detects an error and throws a checked exception
2. Unchecked - code error like IndexOutOfBoundsException, internal error in JVM or runtime
Checked exceptions must be specified with method declaration.
Overriding function in the overloading class cannot have more checked exceptions or different checked exceptions than the overridden method in the base class. It can have no checked exceptions (even if the overridden method has exceptions).

#### Finally
```java
try {
  return Integer.parseInt(s);
}
finally {
  return 0;
}
```
Beware of returns with try-finally. In the above code, if the try block doesn't throw an error, finally will swallow the return and 0 will be returned instead of the parsed value. If try throws an error, finally will swallow the exception and the caller method will not receive an exception.
Finally is supposed to handle cleanup. Don't put code that changes the control flow.

### Logging
Configuration
Localisation
Handlers
Filters
Formatters

### Generics 
Type erasure 
Bridge methods 

#### Restrictions
- Generic classes can't be instantiated with primitive types
```java
var p1 = new Pair<double>(); // error
var p1 = new Pair<Double>(); // no error
```
- Can't do type check in runtime
- Can't have arrays of generic class objects
```java
var p1 = new Pair<string>[10]; // error
var p2 = (Pair<string>[])new Pair<?>[10]; // no error
```