# const 

```c++

    int a;
    int* ptrA;
    ptrA = &a;

    const int b{ 10 };  // const 
    const int* ptrB;    // pointer to a const
    ptrB = &b;

    int c; 
    int* const ptrC{ &c }; // const pointer to a NON const

    const int d{ 10 };
    const int* const ptrD{&d}; // const pointer to a const

```