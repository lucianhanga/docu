## Concepts
---

**C++20 concepts** can be used to constrain the types passed to a function template and prevent the compiler from attempting to instantiate the template.

**Concepts** specify template requirements explicitly in code. They enable the compiler to determine that a **type** is not compatible with a **template** before instantiating it.

**Concepts** also enable you to overload **function templates** with the same signature based on each function template’s requirements.


### Templated lambdas

```c++
[](auto total, auto value) {return total + value * value;}
```
Force the lambda to require the **same type** for both by using a **templated lambda**:

```c++
[]<typename T>(T total, T value) {return total + value * value;}
```
The C++ standard provides 74 predefined concepts, and you can create custom concepts. Each defines a **type’s requirements** or a **relationship between types**. Concepts can be applied to any parameter of any template and to any use of `auto`.

When you call a function, the compiler uses its overload-resolution rules and a technique called **argument-dependent lookup (ADL)** to locate all the function definitions that might satisfy the function call. Together, these are known as the **overload set**. This process often includes instantiating function templates based on a function call’s argument types. The compiler then chooses the best match from the overload set. An unconstrained function template does not explicitly specify any requirements. 


###  Constrained Function Template with a C++20 Concepts `requires` Clause

C++20 **concepts** enable you to specify constraints. Each is a compile-time predicate expression that evaluates to `true` or `false`. The compiler uses constraints to check type requirements before instantiating templates. 

```c++
template<typename T>
requires std::integral<T> || std::floating_point<T>
T multiply(T first, T second) {
    return first * second;
};

int main() {
    cout << multiply(10, 20) << endl;
    cout << multiply(10.5, 20.4) << endl;
    return 0;
}
```

`std::integral<T>` indicates that `T` can be any integer data type.
`std::floating_point<T>` indicates that `T` can be any floating-point data type.

### Type Traits

A fundamental type like `int` using the type trait `std::is_fundamental` vs. a `class` type using the type trait `std::is_class`.

- The **concept** `std::integral` is implemented in terms of the **type trait** `std::is_integral`,
- The **concept** `std::floating_point` is implemented in terms of the **type trait** `std::is_floating_point` and
- The **concept** `std::destructible` is implemented in terms of the **type trait** `std::is_nothrow_destructible`.

```c++
#include<type_traits>

cout << boolalpha << is_integral<int>::value << endl;
cout << boolalpha << is_integral_v<int> << endl;
```

### Custom Concept

A concept begins with a:
- `template` header 
- followed by the C++20 keyword `concept`,
- the concept name (`Numeric`),
- an equal sign (`=`) and
- the constraint expression `(std::integral<T> || std::floating_point<T>)`.

```c++
template<typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;
```

**Concepts** with **multiple template parameters** also can specify **relationships** between types. For example, if a template has two type parameters, you can use the predefined concept `std::same_as` to ensure two type arguments have the same type.

```c++
template<typename T, typename U>
    requires std::same_as<T, U>
    // rest of template definition
```

### `requires` Clause Following the `template` Header

```c++
template<typename T>
   requires Numeric<T>
T multiply(T first, T second) {
    return first * second;
}
```

### `requires` Clause Following a Function Template’s Signature

```c++
template<typename T>
T multiply(T first, T second) requires Numeric<T> {
   return first * second;
}
```

- A member function defined in a class template’s body does not have a template header, so you must use a trailing `requires` clause.

- To use a function template’s parameter names in a constraint, you must use a trailing `requires` clause, so the parameter names are in scope before the compiler evaluates the `requires` clause.

### Concept as a Type in the `template` Header

```c++
template<typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;

template<Numeric T>
Number multiply(T first, T second) {return first * second;}
```

When you have a single concept-constrained type parameter, the C++ Core Guidelines recommend using the concept name in place of `typename` in the `template` header. Doing so simplifies the template definition by eliminating the `required` clause.


### Using Concepts in Abbreviated Function Templates

**Abbreviated function templates** with the parameters declared `auto` so the compiler can infer the function’s parameter types. Anywhere you can use `auto` in your code, you can precede it with a **concept** name to constrain the allowed types.

- abbreviated function template parameter lists,
- `auto` specified as a function’s return type,
- `auto` local-variable definitions that infer a variable’s type from an initializer
- generic `lambda` expressions.

The key difference between this **abbreviated function template** and the constrained multiply function templates is that the compiler treats each `auto` as a separate **template type parameter**. Thus, first and second can have different data types, e.g. which passes an `int` and a `double`.

```c++
// Numeric concept aggregates std::integral and std::floating_point
template < typename T>
concept Numeric = std::integral<T> || std::floating_point<T>;

// abbreviated function template with constrained auto
auto multiply(Numeric auto first, Numeric auto second) {
    return first * second;
}

int main() {
    cout << multiply(10, 20) << endl;
    cout << multiply(10.4, 20) << endl;
    return 0;
}
```

## *requires* expreisons

```c++
requires {
    requirement-definitions
}
```
or 
```c++
requires(params) {
    requirement-definitions which uses params
}
```

compiler is using he parameters to check if they statisfy the requirements in the `requires` braces.

There are four requirement types:

- simple
- type
- compound
- nested

### Simple Requirements

checks if the expresion is valid
e.g.

if any of the simple requirements between brackets does not compile then the type is not a `range`.
```c++
template <class T> 
concept range = 
    requires (T& t) {
        std::rages::begin(t);
        std::ranges::end(t);
    };
```

another example specifies operator expresions

```c++
template<typename T>
concept ArithmeticType = 
    requires (T a, T b) {
        a + b;
        a - b;
        a * b;
        a / b;
        a += b;
        a *= b;
        a -= b;
        a /= b;
    };
```

### Type Requirements

```c++
template<typename T>
concept HasValueType = 
    requires (T& t) {
        typename T::value_type;
    };
```

If the type `T` does not have a nested `value_type` then the expresion would evaluate to `false`.

### Compound Requirements

allows to specify an expresion that also has requirements on the result.

```c++
    { expresion } -> return-type-requirement
```


```c++
template<typename T>
concept incr = 
    requires (I i) {
        { i++ } -> same_as<I>;
    };
```

### Ad-Hoc Constraints

```c++
template<typename T>
   requires requires(const T& t) {
      std::ranges::begin(t);
      std::ranges::end(t);
  }
void printRange(const T& range) {
  for (const auto& item : range) {
     std::cout << item << " ";
  }
}
```

The **first** `requires` introduces the **requires clause**.
The **second** `requires` introduces the **requires expression**.

### Testing c++20 concepts with `static_assert`

`concepts` produce a compile-time `bool` value which can be tested **at compile time** with `static_assert`. 

