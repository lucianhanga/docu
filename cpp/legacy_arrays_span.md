#  Legacy Arrays

## `to_array`

transform from a legacy array to a `std::array`:

```c++
    auto displayElements = [](auto& collection) {
        for (auto& element : collection)
            cout << element << " ";
        cout << endl;
    };

    const int legacyArr[4] = { 10, 20, 30, 40 };
    auto cpp20Arr = to_array(legacyArr);
    displayElements(cpp20Arr);
```

find out info about the type of an object 

```c++
    cout << typeid(legacyArr).name() << endl;
    cout << typeid(cpp20Arr).name() << endl;
```

## `std::span`


```c++
    int legacyArr[4] = { 10, 20, 30, 40 };
    auto cpp20SpanArr = span(begin(legacyArr), end(legacyArr));
    displayElements(cpp20SpanArr);
    cpp20SpanArr[1] = 99;
    displayElements(cpp20SpanArr);
```