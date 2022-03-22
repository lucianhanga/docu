# C++20 Ranges

```c++
#include <ranges>
```

namespace `views` defines operations for ranges

example of `transform`, `filter` and chaining them

```c++

    auto showValues = [](auto & values) {
        for (auto const& value : values) {
            cout << boolalpha << value << " ";
        }
        cout << endl;
    };

    auto values1 = views::iota(1,11); // generate [1..11) ; 11 is not included
    showValues(values1);

    // filter   out the odd number 
    auto values2 = values1 | views::filter([](auto const& val) { return (val % 2) == 0; } );
    showValues(values2);

    // map     double the values
    auto values3 = values1 | views::transform([](auto const& val) {return val * 2;  });
    showValues(values3);
    // map     return an array with true - odd and false - even
    auto values4 = values1 | views::transform([](auto const& val) {return val % 2 == 0;  });
    showValues(values4);

    // chaining
    auto values5 = 
        values1 
        | views::filter([](auto const& val)    { return (val % 2) == 0; })
        | views::transform([](auto const& val) {return val * 2;  });
    showValues(values5);

    return 0;

```