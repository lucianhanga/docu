
### virual & override

if the `getFunc()` would not have existed, because of the `override` keyword, the compile would give an error.

```c++

class Base {
    virtual int getFunc() const;
};

class Derived : public Base {
    int getFunc() const override;
};

```

### virtual destructors

Do not call `virtual` functions in constructors and destructors because polymorphism is not taken in cosideration. The type used which function to call is the type where the constructor/destructor is defined and not the type of the object which is currently constructed/destructed.


If a class has at least a `virtual` function then the `distructor` should be also declared as `virutal`.

```c++
virtual ~Base() {
    // ...
};
```

or if you want to get the deaulft one generated:

```c++
virtual ~Base() = default; //C++11
```

A non-virtual destructor signifies that `deleting` an instance of derived via a base pointer will not work. For example:
```c++
class Base {};
class Derived : public Base {};

Base* b = new Derived;
delete b; // Does not call Derived's destructor!
```

### final

`final` method, no more further virutalization possible.

```c++
class MyClass {
    int myMethod() final;
};
```

`final` class, no other class can be derived from it.

```c++
class MyBaseClass final {
};

class MyDerivedClass final : public BaseClass  {
};
```


### Abstract (Base) Classes & Concrete Classes 

```c++
int virtual myPureVirtualMethod() const = 0;
```

a `Pure Abstract Base Class` with all the methods pure virtual is called an `Interface`.


### Polymorfic behaviour

Refer to a object of a derived class through a pointer/reference to a the base class.

The private virtual functions from a base class can be overriden in the derived class.


### Non-Virtual Interface (NVI) Idiom

- Make `interfaces` non-virtual
- Make `virtual` functions `private`
  Only if a derived classes need to invoke he base class virtual function make the virtual function `protected`.
- A base-class destructor must be either `public virtual` or `protected` and non-virtual.


### Program to an Interface and not an Implementaion

Try to avoid big hyerarchies. Because the derived object inherit the base cases implemnetation and relay on them and changing one base class may break the derived ones.
Also is hard to bebug big hierarchies.

### Composition and Dependency Injection

The `functionalityX` is **not** implemented in the class/class hierarchy but rather the instance `has a pointer` to an `object` which provides the `functionalityX`.  This pointer can be changed to another object which provides `functionalityY` and so so. So there is no need in creating specialized/derived classes which implement functionalityX and functionality`.

C++ GuideLines recomends inheriting from `Interface` rather then Base Classes with implementations. 

### Runtime Polymorphism with `std::variant` and `std::visit`
(Duck Typing)

`If it walks like a duck and it quacks like a duck, then it must be a duck"—to determine whether an object can be used for a particular purpose.`

```c++
#include <iostream>
#include <format>
#include <variant>
#include <string>
#include <vector>

using namespace std;

class LinearDistribution {
public:
    explicit LinearDistribution(int val) : m_value { val } {};
    string duckFunction() const { return "LinearDistribution calculation ... "; };
private:
    int m_value;
};

class GausianDistribution {
public:
    explicit GausianDistribution(int radius) : m_radius{ radius } {};
    string duckFunction() const { return "GausianDistribution calculation ... "; };
private:
    int m_radius;
};

class RandomDistribution {
public:
    explicit RandomDistribution(int seed) : m_seed{ seed }, m_intermediate_hash { 0 } {};
    string duckFunction() const { return "RandomDistribution calculation ... "; };
private:
    int m_seed;
    int m_intermediate_hash;
};

using DistributionType = std::variant< LinearDistribution, GausianDistribution, RandomDistribution>;

int main() {
    vector<DistributionType> modes{ LinearDistribution(120) , GausianDistribution(33), LinearDistribution(10), RandomDistribution(78) };
    auto duckIt = [](const auto &  d) { return d.duckFunction(); };
    for (const auto & mode : modes) {
        cout << std::visit(duckIt, mode) << endl;
    }
}

```

### Multiple Inheritance

- Recomended in the first place `single inheritance` or `composition`
- Recomended multimple inheritance of `interfaces` (Pure Abstract Class - class with only pure virtual methods)
- C++ Guide Lines recomends no multiple inheritnce from Base Implementation Classes.

```c++
// dezambiguity in calling base classes methods with the 
// same signature
cout << derivedObj.Base1::getData();
cout << derivedObj.Base2::getData();
```


```c++
Base1 *base1Ptr = &derivedObj
cout << derivedObj->getData(); // calls the Base1 implementation

Base2 *base2Ptr = &derivedObj
cout << derivedObj->getData(); // calls the Base2 implementation

```

### Diamond Inheritance 

issues when the compiler needs to decide on double sub-class base objects.
```c++
class Base {
};

class Dervi1 : public Base {
};

class Deriv2 : public Base {
    
};

class Multiple : public Deriv1, public Deriv2 {

};

Multiple m{};
Deriv1   d1{};
Deriv2   d2{};
Base* table[3];

table[0] = &d1;
table[1] = &d2;
table[2] = &m; // AMBIGOUS


```

### Virtual Inheritance solved the Diamond Inheritance problem

```c++
class Base {
};

class Dervi1 : virtual public Base {
};

class Deriv2 : virtual public Base {
    
};

class Multiple : public Deriv1, public Deriv2 {

};
```


`private` and `protected` inheritance breaks a **isA** relationship.
