
### const member function

member function which does not modify the object 
 - the compiler knows that the function does not mofify the object and can detect possible unwanted modifications
 - if the object is declared as `const` then the const member functions can be still called because they are not modifying the object.
   
```c++
    const string& getName() const {
        //...
    } 
```

### `explicit` single argument Constructors

C++ Core Guidelines asks every single parameter Constructros to be declared `explicit`.  The only way to invoke the constructor is when the object is created to provide also the appropriate argument. To avoid the compiler calling this automatically/implicitelly in case of conversions from another type to the type in discussion.

```c++
    class Account {
    public:
        explicit Account(std::string_view a_name) {
            // ... 
        }
    }
```

#### `::` scope resolution operator 

### Constructors 

- If a constructor (with parameters) is defined for a call the compiler will **not** provide a `default constructor` anymore.

- `Delegating constructor`
  ```c++
    Time::Time() : Time{0,0,0} {}
    Time::Time(int hour) : Time {hour, 0, 0} {}
    Time::Time(int hour, int minute) : Time {hour, minute, 0} {}
    Time::Time(int hour, int minute, int second) : { /* the code */ }
  ```

### Friend functions

the function `SetX` is allowed to access and modify the `m_value` member data.
```c++
class Count {
    friend void SetX(Count& c, int value);
private:
    int m_value;
}
```
`friend` is 
 - granted and **not** taken
 - **not** symetrical 
 - **not** transitive 

### Const member functions

```c++
class Test {
public:
    void memberConstFunction() const {
        cout << typeid(this).name() << endl; };
    void memberFunction()  {
        cout << typeid(this).name() << endl; };
private:
    int m_member;
};
int main() {
    Test test1{};
    test1.memberConstFunction();
    test1.memberFunction();
    return 0;
```

result:

```c++
class Test const * __ptr64
class Test * __ptr64
```

### Chaining calls
```c++
class Test {
public:
    Test& member1() { return *this; }
    Test& member2() { return *this; }
};
int main() {
    Test t;
    t.member1().member2();
    return 0;
```

### Static data members and static function members 

in c++20 the `inline` is used so the static member should not be defined & initialized at the file scope.

```c++
    inline static int m_staticMember{0};
```

The static member functions are not allowed to be **const**.

### Aggregates

In a `class` all members are `private` by default; in a `struct` all members are `public` by default.

