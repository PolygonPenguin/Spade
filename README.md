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
4.  [Types and Primitives](#types-and-primitives-1)
    *   [Primitive Types and Wrapper Classes](#primitive-types-and-wrapper-classes)
    *   [Primitive/Wrapper Types](#primitivewrapper-types)
    *   [Collection Types](#collection-types-1)
5.  [Collections: Lists](#collections-lists-1)
    *   [List Creation](#list-creation-1)
    *   [List Operations](#list-operations-1)
6.  [Inline Tuple-like Structures (Sets)](#inline-tuple-like-structures-sets-1)
    *   [Set Syntax](#set-syntax-1)
    *   [Key Points (Rules for Sets)](#key-points-rules-for-sets-1)
    *   [Set Examples](#set-examples-1)
    *   [Accessing Set Elements](#accessing-set-elements-1)
    *   [Nested Sets](#nested-sets-2)
	*  [Class assignment](#class-assignment-1)
7.  [Optional Types (`optional`)](#optional-types-optional-2)
    *   [Purpose of `optional`](#purpose-of-optional-2)
    *   [Declaration and Usage](#declaration-and-usage-2)
    *   [Restrictions](#restrictions-2)
8.  [Constructors and Overloading](#constructors-and-overloading-1)
    *   [Constructors](#constructors-2)
    *   [Method Overloading](#method-overloading-2)
9.  [Operator Overloading](#operator-overloading-1)
    *    [Overloadable Operators](#overloadable-operators-3)
    *   [Example](#example-3)
10. [Memory Management](#memory-management-1)
11. [Additional Features](#additional-features-1)
    *   [Implicit Loop Index](#implicit-loop-index-1)
    *   [Null Safety](#null-safety-1)
    *   [Type Checking with `isInstance`](#type-checking-with-isinstance-2)
12. [Libraries](#libraries-1)
    *   [Creating Libraries](#creating-libraries-1)
    *   [Using Libraries](#using-libraries-1)
13. [Nested Classes](#nested-classes-1)
14. [Current Status & Future Plans](#current-status--future-plans-1)
15. [Contributing](#contributing-1)

---

## Overview

Spade combines object-oriented programming with modern features for safety and expressiveness. It aims for streamlined syntax. Spade prioritizes:

*   **Readability:** Clean syntax.
*   **Safety:** Strong typing and `optional` types.
*   **Cross-Platform Compatibility:** Compiles to C, Java, and JavaScript.
*   **Flexibility:** Inline tuple-like structures (Sets).

## Key Features

*   **Object-Oriented:** Classes, objects, inheritance, interfaces.
*   **Flexible Syntax:** Colons (`:`) or braces (`{ ... }`) for class bodies.
*   **Cross-Compilation:** Compiles to C, Java, and JavaScript.
*   **Automatic Memory Management:** Handles memory management.
*   **Optional Types:** `optional` for variables that might be unset.
*   **Strong Typing with Type Inference:** Strong type system (inference is WIP).
*   **Inline Tuple-like Structures (Sets):** Group values of different types.
*   **Rich Standard Library (Planned):** `Default` library provides core types.

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

Choose either `:` or `{ ... }`.

### File Organization

Each class in its own file (e.g., `MyClass.spade`).

## Types and Primitives

Spade is class-based. `Default` provides built-in types.

### Primitive Types and Wrapper Classes

Spade, like Java, has a distinction between *primitive types* and *wrapper classes*.

*   **Primitive Types:** These are the fundamental, low-level data types.  The *specific* primitive types available, and their sizes/representations, *may vary* depending on the compilation target (C, Java, or JavaScript).  For example, an integer might be represented as a 32-bit `int` in C, but a 64-bit `long` in Java.
*   **Wrapper Classes:**  Spade provides *wrapper classes* (like `Integer`, `String`, `Boolean`, etc.) that correspond to these primitive types.  These wrapper classes provide a *consistent* object-oriented interface, regardless of the underlying primitive type used by the target platform.  You should *always* use the wrapper classes in your Spade code.

This approach allows Spade to generate efficient code for each target platform while maintaining a consistent and predictable type system for the programmer.

### Primitive/Wrapper Types

*   **`String` (or `Str`):** Represents text as a sequence of UTF-8 characters.  Provides methods for string manipulation (concatenation, substring, etc.).
*   **`Integer` (or `Int`):** Represents whole numbers.  The underlying primitive type (and therefore the range of values) may vary depending on the compilation target (e.g., `int`, `long`, `BigInteger`).  The `Integer` class provides methods for arithmetic operations, comparisons, and conversions.
*   **`Boolean` (or `Bool`):** Represents a boolean value: `true` or `false`.  Provides methods for logical operations (and, or, not).
*   **`FloatingPoint` (or `Float`):** Represents numbers with decimal points (floating-point numbers).  The underlying primitive type (and therefore the precision) may vary (e.g., `float`, `double`).  The `FloatingPoint` class provides methods for arithmetic, comparisons, and rounding.
*   **`Rational` (or `Rat`):** Represents rational numbers (fractions) exactly, as a pair of `Integer` values (numerator and denominator).  Provides methods for arithmetic operations on fractions, simplifying fractions, and converting to/from `FloatingPoint`.
*   **`Character` (or `Char`):** Represents a single UTF-8 character.  Provides methods for getting character properties (uppercase, lowercase, digit, etc.) and converting to/from integer code points.  Can be created using an integer code point (e.g., `Char(65)`) or a character literal (e.g., `'A'`).
*   **`Void`:** Represents the absence of a value. Used as the return type of functions that don't return anything.  It's not a primitive type in the same way as the others, but it's a fundamental part of the type system.

### Collection Types

*   **`Array<T>`:** Fixed-size, homogeneous.
*   **`ArrayList<T>` (or `List<T>`):** Dynamically-sized, homogeneous.
*   **`LinkedList<T>`:** Linked list.

## Collections: Lists
### List Creation

```spade
// Direct initialization:
List<Int> numbers = [1, 2, 3];
List<String> names = ["Alice", "Bob"];

// Constructor (empty lists):
List<Float> measurements = new List<Float>();
```
### List Operations

```spade
List<String> fruits = ["apple", "banana"];

fruits.add("grape");
String first = fruits[0];
Int num = fruits.size();
for (String f : fruits) { print(f); }
fruits.remove(1);
Bool hasApple = fruits.contains("apple");
```

## Inline Tuple-like Structures (Sets)

Sets use `[]` for type declaration and initialization.  They group values of different types without a formal class.

### Set Syntax

*   **Type/Initialization:** `[Type1, Type2, ...] varName = [value1, value2, ...];`

### Key Points (Rules for Sets)

1.  **`[]` for Types and Literals:** `[]` for *both* type and literal.
2.  **Exact Type Match:** `[Type1, Type2, ...]` *exactly* describes `[value1, value2, ...]`.
3.  **No Required Keyword:** No keyword within the literal.
4.  **Nested Sets:** A set literal within another. Outer type includes *entire* inner type.
5.  **Indexing:** Starts from 0.
6.  **No Implicit Nesting:** Outer type *must* declare inner type.
7. **Class assignment**: you can assign a set literal to a class

### Set Examples

```spade
// Basic:
[Str, Int, Bool] myValues = ["Name", 30, true];
String name = myValues[0];
Int age = myValues[1];

// Nested:
[Str, [Int, Str], Bool] nested = ["outer", [123, "inner"], false];
String outer = nested[0];
[Int, Str] inner = nested[1];
Int val = inner[0];
Str label = inner[1];
Bool flag = nested[2];
Int val2 = nested[1][0]; // Chained
nested[1][0] = 5; // Can be modified

// Assigning to a Class Variable
Class myValues = [Int, Bool, String];
myValues i = [1, TRUE, "hi"];
```

## Optional Types (`optional`)

### Purpose of `optional`

`optional` for instance variables that might be unset.  Prevents null pointer exceptions.

### Declaration and Usage

```spade
class User uses Default:

String username;
optional Int age; // Starts unset

public User _construct_(String username) {
    username = username; // No 'self.' needed unless there's ambiguity
    return self;
}

public Void setAge(Int age) {
    age = age; // No 'self.' needed
}

public String getDetails() {
    String details = "User: " + username;
    if (hasValue(age)) { // Use hasValue()
        details += ", Age: " + age.toString();
    }
    return details;
}
```

*   **`optional Int age;`:** Declares `age` as optional.
*   **`hasValue(age)`:** *Must* use `hasValue()` to check. (`Default` library).
*   **Direct Assignment:** Assign directly.

### Restrictions

*   **Instance Variables Only:** Only for fields within a class.
*   **No Function Parameters:** Use overloading.

## Constructors and Overloading

### Constructors

Create/initialize objects. Same name as class, prefixed with `_construct_`. *Must* return `self`.

```spade
class MyClass uses Default:

String name;
Int value;

public MyClass _construct_(String name, Int value) {
    name = name;  // No 'self.' needed, no ambiguity
    value = value;
    return self;
}
```

### Method Overloading

Multiple methods (including constructors) with the *same name* but *different parameters*.

```spade
class MyClass uses Default:

public MyClass _construct_(String name) { ... } // Constructor 1
public MyClass _construct_(String name, Int val) { ... } // Constructor 2

public Void doSomething() { ... }
public Void doSomething(String msg) { ... } // Overloaded
```

Overloading is preferred over optional parameters.

## Operator Overloading

Define how operators (`+`, `-`, `==`, etc.) behave. Use special methods.

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

### Example

```spade
class MyNumber uses Default:

Int value;

public MyNumber _construct_(Int value) {
    value = value; // No 'self.' needed
    return self;
}

public MyNumber _add_(MyNumber other) {
    return new MyNumber(value + other.value); // No 'self.' needed
}

public Bool _equals_(Object other) {
    if (isInstance(other, MyNumber)) {
        MyNumber otherNum = other;  // Safe cast
        return value == otherNum.value; // No 'self.' needed
    }
    return false;
}
```

## Memory Management

*   **Automatic:** Garbage collection (Java/JS) or manual (C).
*   **Manual Control (Advanced):** Can be overridden (TBD).

## Additional Features

### Implicit Loop Index

`_index_` in `for` loops (starts from 0):

```spade
for (String name : ["Alice", "Bob"]) {
    print("Name " + (_index_ + 1) + ": " + name);
}
```

### Null Safety

`optional` prevents null pointer exceptions.

### Type Checking with `isInstance`

`Default` provides `isInstance(Object, Class)`:

```spade
if (isInstance(obj, MyClass)) {
    MyClass mc = obj;
}
```

## Libraries

Organize and reuse code.

### Creating Libraries

Library file starts with `library`:

```spade
// MyLibrary.spade
library MyLibrary uses Default:

public Int MY_CONSTANT = 42;

public Int add(Int a, Int b) {
    return a + b;
}
class MyClass{
    ...
}
```

*   **`library MyLibrary`:** Library name.
*   **`uses Default`:** Can import others.
*   **Public Members:** `public` members accessible.

### Using Libraries

```spade
// Main.spade
class Main uses Default, MyLibrary implements Runnable:

public static Void main() {
    Int sum = add(5, 3);
    print("Constant: " + MY_CONSTANT.toString());
}
```

*   **`uses Default, MyLibrary`:** Imports.
*   **Direct Access:** Access public members.

## Nested Classes

Classes *within* classes.

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
private class PrivateInnerClass {
        String innerString;
        public PrivateInnerClass _construct_() {
            innerString = "";
            return self;
        }
}
```

*   **`class InnerClass { ... }`:**  Inside `OuterClass`.
*   **Access:** Inner classes can access outer members.
*   **Visibility:** `public` or `private`.
*   **Library Usage:** Inherit `uses` from outer.
*   **Use in Libraries:** Common for encapsulation.

Create *public* inner instances:

```spade
OuterClass outer = new OuterClass();
OuterClass.InnerClass inner = new outer.InnerClass(42);
```

## Current Status & Future Plans

*   **Early Development:** Subject to change.
*   **Interpreter First:** Focus on interpreter.
*   **Compiler:**  C, Java, and JavaScript.
*   **Standard Library Expansion:** More features.