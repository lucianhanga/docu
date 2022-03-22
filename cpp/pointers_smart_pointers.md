# Pointers in C++20

Initialization of a null pointer in C++11 and above

```c++
int* ptrInt{nullptr}; // pointer to nothing
```

display a pointer value

```c++
    const int value{ 7 };
    const int* valuePtr{ &value };
    cout << value << endl;
    cout << format(" {:#x}", reinterpret_cast<intptr_t>(valuePtr)) << endl;
```

### RAII - Resource Aquisition Is Initialization

C++ Core Guidelines recomends RAII - Resource Aquisition Is Initialization
 - aquire resources during construction of the object
 - use them during the object scope
 - release them when the object goes out of scope in the object destructor


### Smart Pointers 
starting with c++11
```c++
#include<memory>
```

allocate and dealocate an array
```c++
// traditional
int* intArr = new[](10);
// dealocate traditional
delete[] intArr;
intArr = nullptr;

// smart pointers
auto ptr{ make_unique<int[]>(10) };
// dealocation will work automatically when intArr runs out of scope


```