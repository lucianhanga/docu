### Operators overloading 

- operators are not implicitelly defined for new types/classes.
- they have to be overloaded using the `operator` keyword
- most of the available operators can be overloaded for new classes
- they MUST be non-`static` members 
- they can be also as non-members of the class

operators which **cannot** be overloaded:

. (dot) member selection operator
.* pointer-to-member operator 
:: scope resolution operator
?: conditional operator until C++20 

**by default** overloaded operators:

= assignment operator : bitwise copy of the members 
& address operator 
, comma operator : evaluates the operation from left and then right and returns the last evaluated expresion value

() [] -> = operators **must** be overloaded as member functions. They don't work as non-member functions.

### `new` and `delete` operators

c++ Core Guidelines recomends not to use these operators directly.


```C++
Time* timePtr{new Time{}};
// or 
Time* timePtr = new Time{};
// release the mem
delete timePtr; // first calls the destructor for objects

// alloc with new an array of fundamental types
int* intArray{ new int[10]{} };
// release an dynamic allocated array
delete[] intArray;
intArray = nullptr;
```

`range base for loops` do not work on the dynamically allocated arrays because the compliler needs to know at the compile time the size of the array. Work arround use `span`
