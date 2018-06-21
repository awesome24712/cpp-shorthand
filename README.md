# cpp-shorthand
A WIP C++ shorthand language for fast prototyping. Spend less time with syntax and more with design. Below is an example conversion from shorthand into separate header, implementation and testing files.

```
n Shapes
c Rectangle
/-Global list of rectangles
e ppRectangle Rectangles 0
c Rectangle : Shape
  /-Member Variables
  i width
  i height
  :build -d width=0 height=0
    /width >= 0
    /height >= 0
  /-Member Functions
  i diagonal() k
  i64 area() k f ov
  i perimeter() k
:tests Rectangle
```
Generated files are below:
**Rectangle.h**
```cpp
//-----------------------------------------------------------
// Globally defined copyright message goes here...
// Copyright Whoever Whenever
// Other licenses...
//-----------------------------------------------------------
// @file Rectangle.h
// @author cheltypes
// @date June 21 2018
//-----------------------------------------------------------
#ifndef SHAPES_RECTANGLE_H
#define SHAPES_RECTANGLE_H

#include "../Shape.h"

namespace Shapes {
  class Rectangle;
  
  //----------------------------------------------------------
  // Global list of rectangles
  //----------------------------------------------------------
  extern Rectangle** g_ppRectangles;
  
  /**
   * @brief
   * @inherit Rectangle class inherits from Shape class.
   * @author cheltypes
   * @date June 32 2018
   */
  class Rectangle : public Shape {
  public:
    //--------------------------------------------------------
    // Member Variables
    //--------------------------------------------------------
    int m_iWidth;
    int m_iHeight;
    
    //--------------------------------------------------------
    // Constuctors
    //--------------------------------------------------------
    /**
     * @brief Builds a Rectangle given width, height
     * @param _width - value for m_iWidth
     * @param _height - value for m_iHeight
     * @requires _width >= 0, _height >= 0
     */
    Rectangle(int _width = 0, int _height = 0);
    
    //--------------------------------------------------------
    // Member Functions
    //--------------------------------------------------------
    /**
     * @brief
     * @return
     */
    int diagonal() const;
    
    /**
     * @brief
     * @return
     */
    int64 area() const final override;
    
    /**
     * @brief
     * @return
     */
    int perimeter() const;
  };
}

#endif //SHAPES_RECTANGLE_H
```
**Rectangle.cpp**
```cpp

//-----------------------------------------------------------
// Globally defined copyright message goes here...
// Copyright Whoever Whenever
// Other licenses...
//-----------------------------------------------------------
// @file Rectangle.cpp
// @author cheltypes
// @date June 21 2018
//-----------------------------------------------------------

#include "Rectangle.h"

namespace Shapes {

  
  //----------------------------------------------------------
  // Global list of rectangles
  //----------------------------------------------------------
  Rectangle** g_ppRectangles = NULL;
  
  /**
   * @brief Builds a Rectangle given width, height
   * @param _width - value for m_iWidth    
   * @param _height - value for m_iHeight
   * @requires _width >= 0, _height >= 0
   */
  Rectangle::Rectangle(int _width, int _height) {
    assert(_width >= 0);
    assert(_height >= 0);
    m_iWidth = _width;
    m_iHeight = _height;
  }
  
  /**
   * @brief
   * @return
   */
  int Rectangle::diagonal() const {
  
  }
    
  /**
   * @brief
   * @return
   */
  int64 Rectangle::area() const {
  
  }
    
  /**
   * @brief
   * @return
   */
  int Rectangle::perimeter() const {
  
  }
}
```
**Test_Rectangle.cpp**
```cpp
//-----------------------------------------------------------
// Globally defined copyright message goes here...
// Copyright Whoever Whenever
// Other licenses...
//-----------------------------------------------------------
// @file Rectangle.cpp
// @author cheltypes
// @date June 21 2018
//-----------------------------------------------------------

#include "Rectangle.h"
#include "CTestPlan.h"

using namespace Shapes;

TEST_PLAN("Shapes::Rectangle");

/**
 * @brief
 */
TEST(RectangleConstructor) {

}

/**
 * @brief
 */
TEST(RectangleDiagonal) {

}

/**
 * @brief
 */
TEST(RectangleArea) {

}

/**
 * @brief
 */
TEST(RectanglePerimeter) {

}

```

# Data Types & Variable Declarations
In declarations, _built-in_ data types (**int**, **float**, **const char \***, etc,) are denoted by _type specifier_ abbreviations. They are followed by a name, and optionally, a value to assign. Names of variables _may have spaces_, in which case they are concatenated in the conversion process. For example, here is a declaration of a float variable:
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
| bool | b |
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
| current_type** | c |

** Wherever 'c' appears from inside a class/union/struct definition, it refers to the above class/struct/union type. For example, if one is declaring a function in some struct **SomeNamespace::SomeClass::SomeStruct**, then a type specifier of 'cp' would be converted to SomeStruct* . Outside of a class/union/struct definiton, 'c' is used to declare and define classes. See the 'Classes' section for more.

Below are the shorthands for C++ qualifiers. Some of them aren't applicable to _variable_ declarations, yet they're here for completeness.

| C++ Qualifier | CPPSH Shorthand | Appended? | Notes |
|---------------|-----------------|-----------|-------|
| **signed** | sg              | No        | This non-appended because it is used less often and would otherwise conflict with 'si' for **short int**. |
| **unsigned** | u | Yes | Must prepend integer type specifier. Ex. "ush" => "unsigned short" |
| **const** | k               | Yes       | Appears separately at the end of the member function declaration to mark it as const.|
| **volatile**      | v               | Yes       | Distinguished from **void** based on context. Appears at ends of member functions to mark them as volatile. |
| **mutable**       | m               | No        | Must precede type specifier.     |
| **static**        | s               | No        | Must precede type specifier.      |
| **extern**        | e               | No        | Must precede type specifier. Distinguished from 'enum' based on context. |
| **inline**        | in              | No        | Must precede type specifier of function return type. |
| **virtual**       | vir             | No        | Must precede return-type specifier and return-type qualifiers of member function declaration. |
| **override**      | ov              | No        | Must follow end of member function declaration. |
| **final**         | f              | No        | Distinguished from **float** based on context. |

# Comments
Vanilla C++ comments are preserved. There location relative to shorthanded declarations is preserved, yet they will appear in multiple files if a declaration beneath them is located in multiple files.

CPPSH introduces new comment formats for the purposes of generating comments. Also, comment blocks are automatically generated for file header, class definitions, function declarations, etc. Below is a table of the new comment formats, and an example beneath that. All new comment formats start with these symbols and continue until the end of the line.

| Comment Delimeter | Explanation |
|-------------------|-------------|
| /-                | Begins a comment block wrapped in //------------ . See the example. |
| /                 | Used to generate JavaDoc-style /** blocks. Place them before class, struct, etc declarations. Place them indented _after_ function declarations to specify requires clauses and assert statements.
| /.                | These comments are ignored and do not appear in generated files. |


```
/. This comment is completely ignored.
/- Here I can describe some kind of special purpose.
/- It's also split into multiple lines by reusing the /- at the beginning.

/ This namespace is for cool stuff.
n cool stuff

/ The best class ever.
c best stuff
  / Gets the best stuff
  c get() k
  / Set the best stuff
  in v set(kcp stuff) k
    / stuff
  //traditional C++ comment
```

```cpp

//------------------------------------------------------------------------
// Globally defined copyright message goes here...
// Copyright Whoever Whenever
// Other licenses...
//------------------------------------------------------------------------
// @file Example.h
// @author cheltypes
// @date June 21 2018
//------------------------------------------------------------------------

#ifndef COOLSTUFF_BESTSTUFF_H
#define COOLSTUFF_BESTSTUFF_H

//------------------------------------------------------------------------
// Here I can describe some kind of special purpose.
// It's also split into multiple lines by reusing the /- at the beginning.
//------------------------------------------------------------------------

//------------------------------------------------------------------------
// This namespace is for cool stuff
//------------------------------------------------------------------------
namespace CoolStuff {

  /**
   * @brief The best class every
   * @inherit Rectangle class inherits from Shape class.
   * @author cheltypes
   * @date June 32 2018
   */
  class BestStuff {
    
    /**
     * Gets the best stuff
     * @return
     */
    BestStuff get() const;
    
    /**
     * Set the best stuff
     * @param stuff
     * @requires stuff != NULL 
     */
    inline void set(const BestStuff* stuff) {
      assert(stuff);
      
    }
    
  };
}
#endif //COOLSTUFF_BESTSTUFF_H
```
An Example.cpp would also be generated, with duplicate comments where appropriate.

# Namespaces
A **namespace** delcaration is done by with 'n' followed by a name. The name may have spaces, in which case it is concatenated at conversion time. Following declarations are automatically interpretted as being a part of the **namespace** _without_ indentation. See the example below. Auto-generated licensing information and include guards are omitted for brevity. 

```
n cool stuff
c foo
  i bar
v foobar()
```
```cpp
namespace CoolStuff {

  /**
   * @brief 
   * @author cheltypes
   * @date June 32 2018
   */
  class Foo {
    int m_iBar;
  };
  
  /**
   * @brief
   */
  void foobar();
}
```
A similarly formatted and commented cpp file is also generated.

# Classes
Class definitions begin with 'c' . See the example above for a simple case.
'c' can also be used to refer to the type of the class/struct/union type defined above a declaration. This is distinguished from defining a subclass based on context. See the example below. Auto-generated comments are omitted for brevity.
```
c Rectangle : Shape
  public:
  // I am a subclass
  c Area
    v foo()
    
  // I am a member function
  c square() k
```
```cpp
class Rectangle : public Shape {
public:
  //I am a subclass
  class Area {
    void foo()
  };
  
  //I am a member function
  Rectangle square() const;
};
```
Inheritance and publicity specifier are just as in C++, except that the default visibility of parent classes is **public**.

# Pre-defined Functions
There are several CPPSH functions for generating C++ code. With these functions, multiple function declarations and definitions can be shorthanded into single lines. All of these functions begin with a colon.

| CPPSH Function | Explanation |
|----------------|-------------|
| :build _member1, member2..._ | Declares and implements a constructor where _member1_, _member2_, etc. are the names of member variables. |
| :buildsuper | Declares, partially implements, and documents constructors which call parent class constructors.
| :gset _member_ | Declares a _private_ member variable named _member_, and with the previous publicity declares, implements and documents functions _GetMember() const_ and _SetMember(const member_t&)_ |

# Functions

# Structs, Unions

# Template Shorthand

# Mixins & Autocomposition

# Preprocessors

# C++ Literals

# Inheritance and Composition Trees

# Auto Documentation

# Exception-Assertion-Documentation Binding
