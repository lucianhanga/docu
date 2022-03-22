# Range base for loop (foreach)

initialize array 
```c++
array<unsinged int, 6> arr{} // initialize all with 0
array<unsinged int, 6> arr{1,2} // initialize first two with 1,2 and rest with 0
```


just get the array item values without modifying them
```c++
   for (const unsigned int item : arr) {
        cout << format("{} ", item);
    }
    cout << endl;
```

item by reference so they can be modified
```c++
    for (unsigned int& item : arr) {
        item++;
        cout << format("{} ", item);
    }
    cout << endl;
```

with initializator - which creates a local variable to the loop which keeps its value for each iteration (more or less like a `static` variable in a function).

```c++
    for (unsigned long total{0}; const unsigned int item : arr) {
        total+= item;
        cout << format("item:{:>4d}  running total:{:>8d}", item, total) << endl;
    }
```