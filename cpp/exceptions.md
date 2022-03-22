# Exceptions

- `catch` should allways catch `const references` to exceptions. In this way exception classes polymorphism is guarantied.

```c++
try {

}
catch( const MyBaseClassExcept& e ) {

}
```
- the order of the catch blocks: derived classes exceptions first and then up the inheritcance tree.

- when an exceptions is thrown, the program tries to locate the fist `try{}`  block. If its not in the current function then it search it in the caller function: **stack unwinding**


### nested exceptions
```c++
#include<iostream>
#include<fstream>
#include<stdexcept>
#include<exception>
#include<format>
#include<string>

using namespace std;

void printException(const exception& e, int level=0) {
    cerr << format("{}exception: {}", string(level,' '), e.what() )<< endl;
    try {
        rethrow_if_nested(e);
    }
    catch (exception nested_e) {
        printException(nested_e, ++level);
    }
    catch (...) {}
}
int readFromFile(const string& filename) {
    try {
        ifstream file(filename);
        file.exceptions(ios_base::failbit);
    }
    catch (...) {
        throw_with_nested(runtime_error("Could not open: " + filename));
    }
}
int main() {
    try {
        readFromFile("alpha");
    }
    catch (const exception& e) {
        printException(e);
    }
}
```

### assert

```c++
#define NDEBUG // disable debug asserts
#include<cassert>
assert(1==1)
```

## exception in costructors 

the exception which is thrown in the initialization list of the constructors even if its catched in the constructor block is re-thrown futher.


```c++
class MyInteger {
public:
    explicit MyInteger(int i) : m_i{ i }  {
        throw runtime_error("Initialization of MyInteger error.");
    }
private:
    int m_i;
};
class MyCompositteClass {
public:
    explicit MyCompositteClass(int i) try :
        m_integer(i) 
    {
        cout << "MyCompositionClass contructor ... " << endl;
    }
    catch (const exception& e) {
        cout << "MyCompositteClass constructor Exception: " << e.what() << endl;
    }
private:
    MyInteger m_integer;
};
int main() {
    try {
        MyCompositteClass myCompositeObject{ 10 };
    }
    catch (const exception& e) {
        cout << "main Exception: " << e.what() << endl;
    }
    return 0;
}
```

