## MyArray Implementation considerations 

### Initilalizer List constructor
```c++
    explicit MyArray(const std::initializer_list<int>& lst);
```
```c++
MyArray::MyArray(const std::initializer_list<int>& lst) :
    m_size{ lst.size() },
    m_ptr { make_unique<int[]>(lst.size()) }
{
    std::copy(lst.begin(), lst.end(), m_ptr.get());
}
```

## Rule of Zero

C++ Core Guidelines recomends to build the classes is such a way that the complier generates automatically the:
- copy constructor
- copy assignment operator
- move constructor
- move assignment operator
- destructor
This can be achieved by using composition with:
- basic data types
- classes which do not require custom resource management/handling
- classes which are using RAII e.g. `std:vector`, `std:Array`

## Rule of Five

If you need to define one of the special members specified above, then you should define all **five** of them! 


## special members 

you can define their implementation, use the default or specify that they should not be implemented

```c++
// implement it 

MyClass(const MyClass& obj) {
    // ....
}

// make it default - tell the compiler to generate the default one
MyClass(const MyClass& obj) = default;

// specify that is not implemented - tell compiler not to generate the default implementation 
MyClass(const MyClass& obj) = delete;

```

### noexcept
if a function does not thow exception and if the function it calls also do not thorw exception declare it with `noexcept`:

e.g. a move copy constructor should not thow exceptions
```c++
// MyClass&& R-value reference (dobule ampersand operator)
MyClass(MyClass&& source) noexcept;
```

it also exists 
```c++
noexcept(true) // for sure it does not throw exceptions
noexcept(false) // its intended not to throw exceptions but its not guarantied
```

### comparison operators 

C++ Core Guideline - make all the `==` symetric with the respect operand types.
If the class support **implicit conversion** from other object types to the class type and viceversa then the comparation operators are recomended to be non-member functions.


