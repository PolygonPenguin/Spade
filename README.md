# Spade

[![Status](https://img.shields.io/badge/status-very%20early%20stages-red.svg)](https://shields.io/)

Spade is a modern, object-oriented programming language designed for clarity, flexibility, and cross-platform compatibility.  It's in **very early stages of development**, but aims to compile to C, Java, and JavaScript.

---

## Table of Contents

1.  [Overview](#overview)
2.  [Key Features](#key-features)
3.  [Class Structure](#class-structure)
    *   [Class Header](#class-header)
    *   [Class Body](#class-body)
    *   [File Organization](#file-organization)
4.  [Types and Primitives](#types-and-primitives)
    *   [Primitive Types and Wrapper Classes](#primitive-types-and-wrapper-classes)
    *   [Primitive/Wrapper Types](#primitivewrapper-types)
    *   [Collection Types](#collection-types)
5.  [Collections: Lists](#collections-lists)
    *   [List Creation](#list-creation)
    *   [List Operations](#list-operations)
6.  [Inline Tuple-like Structures (Sets)](#inline-tuple-like-structures-sets)
    *   [Set Syntax](#set-syntax)
    *   [Key Points (Rules for Sets)](#key-points-rules-for-sets)
    *   [Set Examples](#set-examples)
    *   [Accessing Set Elements](#accessing-set-elements)
    *   [Nested Sets](#nested-sets)
    *   [Class Assignment](#class-assignment)
7.  [Optional Types (`optional`)](#optional-types-optional)
    *   [Purpose of `optional`](#purpose-of-optional)
    *   [Declaration and Usage](#declaration-and-usage)
    *   [Restrictions](#restrictions)
8.  [Constructors and Overloading](#constructors-and-overloading)
    *   [Constructors](#constructors)
    *   [Method Overloading](#method-overloading)
9.  [Operator Overloading](#operator-overloading)
    *   [Overloadable Operators](#overloadable-operators)
    *   [Example](#operator-example)
10. [Lambdas and Functional Programming](#lambdas-and-functional-programming)
    *   [Lambda Syntax](#lambda-syntax)
    *   [Functions as Parameters](#functions-as-parameters)
    *   [Examples](#lambda-examples)
11. [Inheritance and Polymorphism](#inheritance-and-polymorphism)
    *   [Extending Classes](#extending-classes)
    *   [Polymorphism](#polymorphism-in-spade)
    *   [Abstract Classes and Methods](#abstract-classes-and-methods)
12. [Memory Management](#memory-management)
13. [Additional Features](#additional-features)
    *   [Implicit Loop Index](#implicit-loop-index)
    *   [Null Safety](#null-safety)
    *   [Type Checking with `isInstance`](#type-checking-with-isinstance)
14. [Libraries](#libraries)
    *   [Creating Libraries](#creating-libraries)
    *   [Using Libraries](#using-libraries)
15. [Nested Classes](#nested-classes)
16. [Current Status & Future Plans](#current-status--future-plans)
17. [Contributing](#contributing)

---

## Overview

Spade combines object-oriented programming with modern features for safety and expressiveness. It aims for streamlined syntax. Spade prioritizes:

*   **Readability:** Clean syntax.
*   **Safety:** Strong typing and `optional` types.
*   **Cross-Platform Compatibility:** Compiles to C, Java, and JavaScript.
*   **Flexibility:** Inline tuple-like structures (Sets).

## Key Features

*   **Object-Oriented:** Classes, objects, inheritance, polymorphism, interfaces.
*   **Flexible Syntax:** Colons (`:`) or braces (`{ ... }`) for class bodies.
*   **Cross-Compilation:** Compiles to C, Java, and JavaScript.
*   **Automatic Memory Management:** Handles memory management.
*   **Optional Types:** `optional` for variables that might be unset.
*   **Strong Typing with Type Inference:** Strong type system (inference is WIP).
*   **Inline Tuple-like Structures (Sets):** Group values of different types.
*   **Rich Standard Library (Planned):** `Default` library provides core types.
*   **Lambdas and Functional Programming:** Supports lambda expressions and passing functions as parameters.

## Class Structure

### Class Header

```spade
class MyClass uses Default, Math implements MyInterface:
```

*   **`class MyClass`:** Class name.
*   **`uses Default, Math`:** Imports libraries.
*   **`implements MyInterface`:** Implements interfaces.

### Class Body

```spade
class MyClass uses Default:

    String myString; // Instance variable
    Int myInt;

    public Void myMethod(String input) {
        print("Hello, " + input);
    }
```

```spade
class MyClass uses Default {
    String myString;

    public Void myMethod(String input) {
        print("Hello, " + input);
    }
} // Closing brace required
```

Choose either `:` or `{ ... }`.  Consistency is recommended within a project.

### File Organization

Each class should be in its own file (e.g., `MyClass.spade`).

## Types and Primitives

Spade is a class-based language.  The `Default` library provides built-in types.

### Primitive Types and Wrapper Classes

Spade, like Java, distinguishes between *primitive types* and *wrapper classes*.

*   **Primitive Types:**  Fundamental, low-level data types. The *specific* primitive types, their sizes, and representations *may vary* depending on the compilation target (C, Java, or JavaScript).  For example, an integer might be a 32-bit `int` in C, but a 64-bit `long` in Java.
*   **Wrapper Classes:** Spade provides *wrapper classes* (like `Integer`, `String`, `Boolean`, etc.) corresponding to these primitive types. These classes provide a *consistent* object-oriented interface, regardless of the underlying primitive type.  You should *always* use the wrapper classes in your Spade code.

This approach allows efficient code generation for each target while maintaining a consistent and predictable type system.

### Primitive/Wrapper Types

*   **`String` (or `Str`):** Text as UTF-8 characters. Methods for string manipulation.
*   **`Integer` (or `Int`):** Whole numbers. The underlying primitive type (and range) may vary (e.g., `int`, `long`, `BigInteger`). Methods for arithmetic, comparisons, and conversions.
*   **`Boolean` (or `Bool`):** `true` or `false`. Methods for logical operations (and, or, not).
*   **`FloatingPoint` (or `Float`):** Numbers with decimal points. Precision may vary (e.g., `float`, `double`). Methods for arithmetic, comparisons, and rounding.
*   **`Rational` (or `Rat`):** Rational numbers (fractions) represented exactly as a pair of `Integer` values (numerator and denominator). Methods for arithmetic on fractions, simplification, and conversion to/from `FloatingPoint`.
*   **`Character` (or `Char`):** A single UTF-8 character. Methods for character properties (uppercase, lowercase, digit, etc.) and conversion to/from integer code points. Created using an integer code point (e.g., `Char(65)`) or a character literal (e.g., `'A'`).
*   **`Void`:** The absence of a value.  Used as the return type of functions that don't return anything.

### Collection Types

*   **`Array<T>`:** Fixed-size, homogeneous collections.
*   **`ArrayList<T>` (or `List<T>`):** Dynamically-sized, homogeneous collections.
*   **`LinkedList<T>`:** Linked list implementation.  Provides efficient insertion and removal at arbitrary positions.

## Collections: Lists

### List Creation

```spade
// Direct initialization:
List<Int> numbers = [1, 2, 3];
List<String> names = ["Alice", "Bob", "Charlie"];

// Constructor (empty lists):
List<Float> measurements = new List<Float>();
```

### List Operations

```spade
List<String> fruits = ["apple", "banana"];

fruits.add("grape");               // Add an element
String first = fruits[0];        // Access by index
Int numFruits = fruits.size();     // Get the size
for (String f in fruits) {      // Iterate
    print(f);
}
fruits.remove(1);                 // Remove by index
Bool hasApple = fruits.contains("apple"); // Check for element
```

## Inline Tuple-like Structures (Sets)

Sets use `[]` for *both* type declaration and initialization. They group values of different types without a formal class definition.

### Set Syntax

*   **Type/Initialization:** `[Type1, Type2, ...] varName = [value1, value2, ...];`

### Key Points (Rules for Sets)

1.  **`[]` for Types and Literals:** Use `[]` for *both* the type declaration and the literal value.
2.  **Exact Type Match:** The type declaration `[Type1, Type2, ...]` must *exactly* describe the literal `[value1, value2, ...]`.
3.  **No Required Keyword:**  There's no special keyword inside the set literal.
4.  **Nested Sets:** You can have a set literal within another set literal. The outer set's type declaration must include the *entire* inner set's type.
5.  **Indexing:** Indexing starts from 0.
6.  **No Implicit Nesting:** The outer set's type *must* explicitly declare the inner set's type.
7.  **Class Assignment:** You can assign a set literal to a class variable.

### Set Examples

```spade
// Basic set:
[Str, Int, Bool] myValues = ["Name", 30, true];
String name = myValues[0];
Int age = myValues[1];

// Nested set:
[Str, [Int, Str], Bool] nested = ["outer", [123, "inner"], false];
String outerStr = nested[0];
[Int, Str] innerSet = nested[1];
Int innerVal = innerSet[0];
Str innerLabel = innerSet[1];
Bool flag = nested[2];
Int val2 = nested[1][0]; // Chained indexing
nested[1][0] = 5;       // Sets can be modified

// Assigning a set to a class variable:
Class myValuesClass = [Int, Bool, String];
myValuesClass myInstance = [1, true, "hello"];
```

### Accessing Set Elements

Use square bracket notation with zero-based indexing: `mySet[index]`.

### Nested Sets

Nested sets are fully supported, as shown in the examples above.

### Class Assignment

As demonstrated, you can assign set literals to class-typed variables.

## Optional Types (`optional`)

### Purpose of `optional`

The `optional` keyword is used for *instance variables* that might be unset. If you don't use the optional keyword, that variable **has** to be set in **all** constructors or you will get an error

### Declaration and Usage

```spade
class User uses Default:
String username; // 'username' HAS to be set in the constructor
optional Int age; // 'age' doesn't have to be set in the constructor

public User _construct_(String username) {
    username = username;
    return(self);
}

public Void setAge(Int age) {
    age = age;  // Direct assignment to optional
}

public String getDetails() {
    String details = "User: " + username;
    hasValue(age) {  // *Must* use hasValue() to check
        details += ", Age: " + age.toString();
    }
    return(details);
}
```

*   **`optional Int age;`:** Declares `age` as an optional integer.  It starts with no value.
*   **`hasValue(age)`:** You *must* use the `hasValue()` function (provided by the `Default` library) to check if an optional variable has a value before accessing it. If it has a value it will run that code normally, if it doesn't, it skips that chunk of code.
*   **Direct Assignment:**  You can assign values directly to an optional variable.

### Restrictions

*   **Instance Variables Only:**  `optional` can only be used for fields (instance variables) within a class.
*   **No Function Parameters:** `optional` is *not* allowed for function parameters. Use method overloading instead (see below).

## Constructors and Overloading

### Constructors

Constructors are special methods used to create and initialize objects.  They have the same name as the class, prefixed with `_construct_`. Constructors *must* return `self`.

```spade
class MyClass uses Default:
String name;
Int value;

public MyClass _construct_(String name, Int value) {
    self.name = name;
    self.value = value;
    return(self);
}
```

### Method Overloading

Method overloading allows you to define multiple methods (including constructors) with the *same name* but *different parameter lists*.  This is the preferred way to handle optional parameters in Spade.

```spade
class MyClass uses Default:

public MyClass _construct_(String name) {
    this(name, 0); // Calls the other constructor
    return(self);
}
public MyClass _construct_(String name, Int val) {
    name = name;
    value = val;
    return(self);
}

public Void doSomething() {
    print("Doing something...");
}
public Void doSomething(String message) { // Overloaded method
    print("Doing something: " + message);
}
```

Overloading provides flexibility and avoids the need for `optional` parameters.

## Operator Overloading

Operator overloading allows you to define how operators (like `+`, `-`, `==`, etc.) behave with objects of your custom classes.  You do this by defining special methods in your class.

### Overloadable Operators

*   **`+`:** `_add_`
*   **`-`:** `_subtract_`
*   **`*`:** `_multiply_`
*   **`/`:** `_divide_`
*   **`==`:** `_equals_`
*   **`!=`:** `_notEquals_`
*   **`<`:** `_lessThan_`
*   **`>`:** `_greaterThan_`
*   **`<=`:** `_lessThanOrEqual_`
*   **`>=`:** `_greaterThanOrEqual_`
### Operator Example

```spade
class MyNumber uses Default {
    Int value;

    public MyNumber _construct_(Int value) {
        value = value;
        return(self);
    }

    public MyNumber _add_(MyNumber other) {
        return(new MyNumber(value + other.value));
    }

    public Bool _equals_(Object other) {
        if (isInstance(other, MyNumber)) {
            MyNumber otherNum = other; // Safe cast
            return(value == otherNum.value);
        }
        return(false);
    }
}
```

## Lambdas and Functional Programming

Spade supports lambda expressions (anonymous functions) and passing functions as parameters.

### Lambda Syntax

```spade
(parameter1Type parameter1Name, parameter2Type parameter2Name, ...) {
  // Lambda body - code to be executed
  return(result);
}
```

Single-expression lambda (implicit return):

```spade
(Int a, Int b){a + b};
```

### Functions as Parameters

```spade
// Function definition
ReturnType functionName(Param1Type param1, Param2Type param2) {
    // function Body
}

// Function taking another function as a parameter
ReturnType2 outerFunction(Param3Type a, ReturnType functionName(Param1Type, Param2Type)){
    //do something
}
```

### Lambda Examples

```spade
class Main uses Default:

public static Void main() {
    // Lambda assigned to a variable:
    myAdder = (Int a, Int b) a + b;
    Int result = myAdder(5, 3);
    print(result.toString()); // Output: 8

    // Passing a lambda directly to a function:
    Int result2 = operate(10, 4, (Int x, Int y) x - y);
    print(result2.toString()); // Output: 6

    // Function as a parameter:
    Int result3 = applyAndSum(2, 3, square);
    print(result3.toString()); // Output: 13

    // Example using List and a lambda to filter:
    List<Int> numbers = [1, 2, 3, 4, 5, 6];
    List<Int> evens = filterList(numbers, (Int n) n % 2 == 0);
    print(evens.toString());  // Output: [2, 4, 6]
}

// Function taking a lambda as a parameter:
public static Int operate(Int a, Int b, Int functionToApply(Int, Int)) {
    return(functionToApply(a, b));
}

// Function passed as a parameter:
public static Int square(Int n) {
    return(n * n);
}

public static Int applyAndSum(Int a, Int b, Int toApply(Int)) {
    return(toApply(a) + toApply(b));
}

// Function to filter a list using a lambda:
public static List<Int> filterList(List<Int> list, Bool predicate(Int)) {
    List<Int> result = new List<Int>();
    for (Int item in list) {
        if (predicate(item)) {
            result.add(item);
        }
    }
    return(result);
}
```

*   **Type Inference (WIP):** Full type inference is a work in progress. Spade can often infer a lambda's return type if it's a single expression. Parameter types currently need to be specified.
*   **Closures:** Lambdas in Spade are *closures*. They can "capture" variables from the surrounding scope. This captured state is preserved even if the surrounding scope goes away.
*   **Naming Convention:** To indicate a parameter that uses a function, use the format `ReturnType functionName(param1Type, param2Type,...)`.
* **Function Definitions:** Function can be defined in class as usual and in the `Default` library.
## Inheritance and Polymorphism

Spade supports inheritance (creating new classes that inherit from existing ones) and polymorphism (treating objects of different classes as objects of a common type).

### Extending Classes

Use the `extends` keyword:

```spade
class Animal uses Default {
    String name;

    public Animal _construct_(String name) {
        self.name = name;
        return(self);
    }

    public String makeSound() {
        return("Generic animal sound");
    }
}

class Dog extends Animal {
    String breed;

    public Dog _construct_(String name, String breed) {
        super(name); // Call superclass (Animal) constructor
        breed = breed;
        return(self);
    }

    // Overriding a method
    public String makeSound() {
        return("Woof!");
    }
}

class Cat extends Animal {
    Int lives;

    public Cat _construct_(String name, Int lives) {
        super(name); // Call superclass (Animal) constructor
        self.lives = lives;
        return(self);
    }

     // Overriding a method
    public String makeSound() {
        return("Meow!");
    }
}
```

*   **`class Dog extends Animal`**: `Dog` inherits from `Animal`.
*   **`super(name);`**:  Calls the base class (`Animal`) constructor.  *Required* if the base class has a constructor with parameters. Must be the first statement in the derived class constructor.
*   **`makeSound()` (in `Dog`):** *Overrides* the `makeSound()` method from `Animal`.

### Polymorphism in Spade

```spade
class Main uses Default:
public static Void main():

Animal myAnimal = new Dog("Buddy", "Golden Retriever");
print(myAnimal.makeSound()); // Output: Woof! (Dog's makeSound is called)

Animal myOtherAnimal = new Cat("Whiskers", 9);
print(myOtherAnimal.makeSound()); // Output: Meow! (Cat's makeSound is called)
```

*   **`Animal myAnimal = new Dog(...)`**: A `Dog` object can be assigned to an `Animal` variable because `Dog` *is an* `Animal`.
*   **`myAnimal.makeSound()`**: Even though `myAnimal` is declared as `Animal`, the *actual* object is a `Dog`, so `Dog`'s `makeSound` is executed (dynamic dispatch).

### Abstract Classes and Methods

*Frameworks* cannot be instantiated directly but serve as templates.  They can have *abstract methods*, which have no implementation and *must* be overridden by derived classes or they can have *concrete methods* that are inherited by derived classes and can be overridden

```spade
framework Shape uses Default {  // 'framework' keyword instead of class
    public Float getArea(); // Abstract method - no body

    public String getDescription() { // Concrete method
        return("This is a shape.");
    }
}

class Circle uses Default, Math implements Shape {
    Float radius;

    public Circle _construct_(Float radius) {
        radius = radius;
        return self;
    }

    // MUST override getArea()
    public Float getArea() {
        return PI * pow(radius, 2);
    }
}

class Rectangle extends Shape {
    Float width;
    Float height;

    public Rectangle _construct_(Float width, Float height) {
        width = width;
        height = height;
        return self;
    }
     // MUST override getArea()
    public Float getArea() {
        return width * height;
    }
}
```

*   **`framework Shape`**: Defines an abstract class.
*   **`public Float getArea();`**: Declares an abstract method. No implementation.
*   **`Circle implements Shape`**: `Circle` *must* provide an implementation for `getArea()`.

## Memory Management

*   **Automatic:** Spade uses garbage collection (for Java and JavaScript targets) or manual memory management (for the C target).  The specifics of the C implementation are still under development.
*   **Manual Control (Advanced):**  Advanced users may have options for overriding the default memory management behavior (details TBD).

## Additional Features

### Implicit Loop Index

The `_index_` variable is available within `for` loops, starting from 0:

```spade
for (String name in new Array<String>(["Alice", "Bob"])) {
    print("Name " + (_index_ + 1).toString() + ": " + name);
}
```

### Null Safety

`optional` types help prevent null pointer exceptions.

### Type Checking with `isInstance`

The `Default` library provides `isInstance(Object, Class)` for type checking:

```spade
if (isInstance(obj, MyClass)) {
    MyClass mc = obj; // Safe cast after type check
}
```

## Libraries

Libraries organize and reuse code.

### Creating Libraries

A library file starts with the `library` keyword:

```spade
// MyLibrary.spade
library MyLibrary uses Default:

public Int MY_CONSTANT = 42;

public Int add(Int a, Int b) {
    return a + b;
}

class MyUtilityClass {
    // ...
}
```

*   **`library MyLibrary`:**  The library's name.
*   **`uses Default`:** Libraries can import other libraries.
*   **`public` Members:** Only `public` members are accessible from outside the library.

### Using Libraries

```spade
// Main.spade
class Main uses Default, MyLibrary implements Runnable:
public static Void main():

Int sum = add(5, 3);  // Accessing MyLibrary.add
print("Constant: " + MY_CONSTANT.toString()); // Accessing MyLibrary.MY_CONSTANT

```

*   **`uses Default, MyLibrary`:**  Imports the necessary libraries.
*   **Direct Access:** Access public members of the imported library directly.

## Nested Classes

Classes can be defined *within* other classes:

```spade
class OuterClass uses Default:

String outerString;

class InnerClass { // Nested class
    Int innerInt;
    public InnerClass _construct_(Int innerInt){
        innerInt = innerInt;
        return self;
    }
}

private class PrivateInnerClass { // Private nested class
    String innerString;
    public PrivateInnerClass _construct_(){
        innerString = "";
        return self;
    }
}
```

*   **`class InnerClass { ... }`:** Defines a class nested inside `OuterClass`.
*   **Access:** Inner classes can access members of the outer class.
*   **Visibility:**  Nested classes can be `public` or `private`.
*   **Library Usage:** Nested classes inherit the `uses` declarations from their outer class.
*   **Use in Libraries:** Nested classes are commonly used for encapsulation and organization within libraries.

Create instances of *public* inner classes like this:

```spade
OuterClass outer = new OuterClass();
OuterClass.InnerClass inner = new outer.InnerClass(42);
```

## Current Status & Future Plans

*   **Very Early Development:** The language is in the very early stages of development and is subject to significant changes.
*   **Interpreter First:** The initial focus is on building a working interpreter.
*   **Compiler:**  Compilers targeting C, Java, and JavaScript are planned.
*   **Standard Library Expansion:**  The standard library will be expanded with more features and utilities.