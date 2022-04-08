## Functional Style Programming
---

 `view` does not have its own copy of a **range**’s elements—it simply moves the elements through a pipeline of operations. Views are one of C++20’s key functional-style programming capabilities.

`views` are **lazy**—they do not produce results until you iterate over them in a loop or pass them to an algorithm that iterates over them.


`std::views::filter` and `std::views::transform` are **range adapters**.

Each **range adaptor** takes a `std::ranges::viewable_range` as an argument and returns a view of that range for use in a pipeline of operations.

A `viewable_range` is a range that can be safely converted into a `view`.


- `filter` - reates a `view` representing only the range elements for which a **predicate** returns `true`.

```c++
    auto isEven{ [](auto element) {return (element % 2) == 0; } };

    auto infiniteEvens{ 
        std::ranges::views::iota(0) | 
        std::ranges::views::filter(isEven)
    };

```

- `take` - creates a `view` containing the specified number of elements from the beginning of another `view`.
```c++
    auto fist10Evens{
        infiniteEvens |
        std::ranges::views::take(10)
    };
    std::ranges::copy(fist10Evens, output);
```

- `take_while` - creates a `view` containing the elements from the beginning of another `view` as long as a **predicate** returns `true`.
```c++
    auto upTo50Evens{
        infiniteEvens |
        std::ranges::views::take_while([](auto element) { return element <= 50; })
    };
    std::ranges::copy(upTo50Evens, output);
```

- `drop` - Creates a view that ignores the specified number of elements at the beginning of another view.

- `drop_while` - Creates a view that ignores the elements at the beginning of another view as long as a predicate returns true.

```c++
    auto from20To40Evens{
        infiniteEvens |
        std::ranges::views::drop_while([](auto el) { return el < 20; }) |
        std::ranges::views::take_while([](auto el) { return el <= 40; })
    };
    cout << "evens from 20 to 40: ";
    std::ranges::copy(from20To40Evens, output);
    cout << endl;
```

- `reverse` - Creates a `view` for processing a bidirectional `view` in **reverse order**.

```c++
    auto first10EvensReverse{
        infiniteEvens |
        std::ranges::views::take(10) |
        std::ranges::views::reverse
    };

    cout << "first 10 evens in reverse: ";
    std::ranges::copy(first10EvensReverse, output);
    cout << endl;
```


- `transform` - Creates a `view` that **maps** elements to new values.

```c++
    auto first10EvensReverseSquares{
        infiniteEvens |
        std::ranges::views::take(10) |
        std::ranges::views::reverse |
        std::ranges::views::transform([](auto el) { return el * 2; })
    };

    cout << "first 10 evens in reverse and squared: ";
    std::ranges::copy(first10EvensReverseSquares, output);
    cout << endl;
```


- `keys` - Creates a `view` of the **keys in key—value pairs**, such as those in a `map`. The keys are the first elements in the pairs.
- `values` - Creates a `view` of the **values in key—value pairs**, such as those in a `map`. The `values` are the second elements in the pairs.




common

Used to convert a view into a std::ranges::common_range, which enables a range to be used with common-range algorithms that require begin/end iterator pairs of the same type.

all

Creates a view representing all of a range’s elements.

counted

Creates a view of a specified number of elements from either the beginning of a range or from a specific iterator position.




join

Creates a view that combines the elements of multiple ranges.

split

Splits a view based on a delimiter. The new view contains a separate view for each subrange.


elements

For a view containing tuples, pairs or arrays, creates a view consisting of elements from a specified index in each object.