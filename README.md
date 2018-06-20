# cpp-shorthand
A WIP C++ shorthand language for fast prototyping. Spend less time with syntax and more with design.

# Data Types & Variable Declarations
In declarations, _Built-in_ data types (**int**, **float**, **const char \***, etc,) are denoted by _type specifier_ abbreviations. They are followed by a name, and optionally, a value to assign. Names of variables _may have spaces_, in which case they are concatenated in the conversion process. For example, here is a declaration of a float variable:
```
f default range 100
```
The exact conversion of this into C++ code depends on the context and conversion settings. For example, in a namespace context, this may be converted to:
```cpp
float g_flDefaultRange = 100;
```
While from inside a class/struct/union declaration, this may be converted to:
```cpp
float m_flDefaultRange = 100;
```
Pointer types are declared by appending a 'p' or multiple 'p's to the type specifier. Similarly, a **const** variable may be declared by appending a 'k' before or after the type specifier. An example conversion:
```
dkpkp multiplier list 0
```
```cpp
double const * const * g_ppMultiplierList = NULL;
```
A table of type specifiers is below. More declaration modifiers (sign, storage duration) are seen below that.

| C++ Type | CPPSH Shorthand |
| -------- | --------------- |
| int | i |
| long | l |
| float | f |
| double | d |
| void | v |
| char | ch |
| wchar | w |
| short | sh |
| long int | li |
| long long int | lli |
| short int | si |
| long double | ld |

Below are the shorthands for C++ qualifiers. Some of them aren't applicable to _variable_ declarations, yet they're here for completeness.

| C++ Qualifier | CPPSH Shorthand | Appended? | Notes |
|---------------|-----------------|-----------|-------|
| **signed** | sg              | No        | This non-appended because it is used less often and would otherwise conflict with 'si' for **short int**. |
| **unsigned** | u | Yes | Must prepend integer type specifier. Ex. "ush" => "unsigned short" |
| **const** | k               | Yes       | Appears separately at the end of the member function declaration to mark it as const.|
| **volatile**      | v               | Yes       | Distinguished from 'void' based on context. Appears at ends of member functions to mark them as const. |
| **mutable**       | m               | No        | Must precede type specifier.     |
| **static**        | s               | No        | Must precede type specifier.      |
| **extern**        | e               | No        | Must precede type specifier. Distinguished from 'enum' based on context. |
| **inline**        | in              | No        | Must precede type specifier of function return type. |
| **virtual**       | vir             | No        | Must precede return-type specifier and return-type qualifiers of member function declaration. |
| **override**      | ov              | No        | Must follow end of member function declaration. |

# Comments

# Namespaces

# Classes

# Pre-defined Functions

# Functions

# Structs, Unions

# Template Shorthand

# Mixins & Autocomposition

# Preprocessors

# C++ Literals

# Inheritance and Composition Trees

# Auto Documentation

# Exception-Assertion-Documentation Binding
