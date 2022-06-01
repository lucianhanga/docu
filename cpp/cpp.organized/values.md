## Value Categories
---

Each C++ expresion (a literal, variable name, operation with operands ...) is characterized by two independent properties:
- type
- value category

Value Categories:
- **glvalue** - *generalized* **lvalues** - an expresion which evaluation determines the idenity of an object or a function. 
- **prvalue** -  *pure* value - is an expresion which evaluation computes the value of an operand of a build-in operator. An initializator for an object - in such case is said to have a *result* object.   
- **xvalue** - *e**X**piring* value - is a *glvalue* which denotes an object whose resources can be reused.
- **lvalue** - is a *glvalue* which is not *xvalue*.
- **rvalue** - is a *prvalue* or an *xvalue*.

returning a **rvalue**:
```c++
int&& foo1() {
    return 1;
}
int& foo2() {
    int temp = 1;
    return temp;
}
int main() {
    cout << foo1() << endl;
    cout << foo2() << endl;
    return 0;
}
```

returning a **lvalue** - something which can be assigned:

```c++
int nontemp; // global
int& foo3() {
    return nontemp;
}
int main() {
    foo3() = 1;
    cout << foo3() << endl;
    return 0;
}
```

```c++
class FooContainer {
public:
    explicit FooContainer(const int& x) noexcept : m_member{ x } {}
    const int& operator [] (int index) const { // returns rvalue
        cout << "return rvalue" << endl;
        return m_member;
    };
    int& operator [] (int index) { // returns lvalue
        cout << "return lvalue" << endl;
        return m_member;
    };
private:
    int m_member;
};
```

