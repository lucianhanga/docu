# Algorithms
---
!!! . C++20 algorithms are in `std::ranges` namespace and use C++20 `ranges`. The old c++ algorithms are in the `std` namespace and are using the pre C++20 common ranges: two iterators represinting the begin and one element past the end of a range.

The C++ standard library separates `containers` from the `algorithms` that manipulate the containers. Most `algorithms` operate on `container` elements indirectly via `iterators`. This architecture makes it easier to write generic algorithms applicable various containers— a strength of the standard library algorithms.


### C++20 Concepts

One of the **“big four” C++20 features** is `concepts` — a technology for constraining the types used with templates.

Each concept specifies a type’s requirements or a **relationship** between types.


### for_each

```c++
std::array arr{ 1,2,3,4,5 }; // detects the type automatically
std::ranges::for_each(arr, [](auto i) { std::cout << i << " ";  });
```

###copy c++20

```c++
std::array arr{ 1,2,3,4,5 }; // detects the type automatically
std::ostream_iterator<int> output{ std::cout, " " };
std::cout << "the vector contains the values: ";
std::ranges::copy(arr, output);  //C++20 ranges
std::cout << std::endl;
```

### lambda functions 

Lambdas begin with the **lambda introducer ([])**, followed by a parameter list and a body. This lambda introducer is empty, so it does not capture any local variables. The parameter’s type is auto, so this is a generic lambda for which the compiler infers the type based on the context. 

## std::ranges::for_each

```c++
std::array arr{ 1,2,3,4,5 }; // detects the type automatically
std::ranges::for_each(arr, [](auto i) { std::cout << i << " ";  });
```

Lambda function with capturing a local variable, passed through **reference**

```c++
int sum{ 0 };
std::ranges::for_each(arr, [&sum](auto i) { sum += i;  });
```

Lambda function with capturing a local variable, passed through **value** only

```c++
int factor{ 2 };
std::ranges::for_each(arr, [factor](auto i) {std::cout << i * factor << " "; });
```

## std::ranges::fill 

```c++
std::array<char, 10> title{};
std::ranges::fill(title, 'a');
std::ostream_iterator<char> output_chars{ std::cout, " " };
std::ranges::copy(title, output_chars);
std::cout << std::endl;
```

## std::ranges::generate
```c++
char chr{ 'A' };
std::array<char, 8> chars{};
std::ranges::generate(chars, [&chr]() { return chr++; });
```

or with a lambda which contains a `static` variable
```c++
std::array<char, 8> chars{};
std::ranges::generate(chars, []() { static char chr{ 'A' };  return chr++; });
```

## std::ranges:equal
```c++
std::array<int, 5> array1{ 1,2,3,4,5 };
std::array<int, 5> array2{ 1,2,3,4,5 };
std::array<int, 5> array3{ 2,2,3,4,5 };
std::cout << std::ranges::equal(array1, array2) << std::endl;
// with a predicate
std::cout << std::ranges::equal(array1, array2, [](auto e1, auto e2) { return e1 == e2; }) << std::endl;
```

## std::mismatch

the result type for `std::ranges::mismatch` is `std::ranges::mismatch_result`

using `auto`: C++17 class-template argument deduction (**CTAD**) also could be used to infer the type arguments.

```c++
std::array<int, 10> array4{ 1,2,3,4,5,6,7,8,9,10 };
std::array<int, 10> array5{ 1,2,3,4,0,6,7,8,9,10 };

auto res{ std::ranges::mismatch(array4, array5) };
std::cout << std::format("Mismatching at {} and {}", res.in1 - array4.begin() , res.in2 - array5.begin()) << std::endl;
```

## std::ranges::remove & std::ranges::remove_if

Remove-Erase Idiom

You remove elements via `remove` or `remove_if`, then call the vector’s `erase` member function to eliminate the now unused elements.

```c++
std::vector<int> vector1{ 1,2,3,4,5,6,7,8,9,10,11,12 };

for (auto& e : vector1) {
    std::cout << e << " ";
};

std::cout << std::endl;
auto isOdd = [](auto nr) { return (nr % 2) == 0 ? false : true; };
auto removedElements{ std::ranges::remove_if(vector1, isOdd) };
vector1.erase(removedElements.begin(), removedElements.end());

for (auto& e : vector1) {
    std::cout << e << " ";
};
std::cout << std::endl;
```

## std::erase & std::erase_if

to make the usage of the Remove-Erase Idiom easier.

```c++
std::vector<int> vector2{ 1,2,3,4,5,6,7,8,9,10,11,12 };

std::ranges::copy(vector2, output);
std::cout << std::endl;

auto isOdd = [](auto nr) { return (nr % 2) == 0 ? false : true; };
std::erase_if(vector2, isOdd);

std::ranges::copy(vector2, output);
std::cout << std::endl;
```

## std::ranges::remove_copy_if

```c++
std::vector<int> vector4{ 1,2,3,10,4,5,6,10,7,8,9,10,11,12,10 };
std::vector<int> cleanVector{};

auto isUnwanted = [](auto element) { return element == 10; };
std::ranges::remove_copy_if(vector4, std::back_inserter(cleanVector),isUnwanted);

std::cout << "clean vector: ";
std::ranges::copy(cleanVector, output);
std::cout << std::endl;
```

### Iterator Adapters: back_inserter, front_inserter and inserter

A `back_insert_iterator` cannot be used with `arrays` because they are fixed-size containers and do not have a `push_back` function.

 A **unary predicate function** must receive **one parameter** and **return a bool** value.

## std::ranges::replace & std::ranges::replace_if & std::ranges::replace_copy_if

```c++
std::array<int, 10> a1{ 1,2,3,4,5,6,7,8,9,10 };

//replace
std::ranges::replace(a1, 2, 20);

//replace_if
auto isBiggerThanSix = [](auto element) { return element > 6; };
std::ranges::replace_if(a1, isBiggerThanSix, 10);
```

```c++
std::array<int, 10> a2{ 1,2,3,4,5,6,7,8,9,10 };
std::array<int, a2.size()> aa2{};
auto isBiggerThanFour = [](auto element) { return element > 4; };
std::ranges::replace_copy_if(a2, aa2.begin(), isBiggerThanFour, 10);
```

### std::ranges::min_element

```c++
auto min_result{ std::ranges::min_element(a2) };
std::cout << *min_result << std::endl;

auto max_result{ std::ranges::max_element(a2) };
std::cout << *max_result << std::endl;

auto [min, max] { std::ranges::minmax_element(a2)};
auto result{ std::ranges::min_element(a2) };

std::cout << *min_result << "   " << *max_result << std::endl;
```

`minmax_element_result` returned by `minmax_element` to initialize the variables `min` and `max` using a **C++17 structured binding declaration**.This is sometimes referred to as **unpacking the elements** and can be used to extract into individual variables the elements of a built - in array, `std::array` object, `std::pair` or `std::tuple`(each of which has a size that’s known at compile - time).

## std::ranges::transform

```c++
ostream_iterator<int> output{ cout, " " };

array<int, 10> a1{ 1,2,3,4,5,6,7,8,9,10 };
array<int, a1.size()> a2{};

ranges::transform(a1, a2.begin(), [](auto element) { return element * element * element;  });

cout << "a1: ";
ranges::copy(a1, output);
cout << endl;
cout << "a2: ";
ranges::copy(a2, output);
cout << endl;
```

## ranges::find && ranges::find_if && ranges::find_if_not

```c++
array<int, 10> a1{ 1,2,3,4,5,6,7,8,9,10 };
int value{ 7 };
auto posElement{ ranges::find(a1, value) };
if (posElement == a1.cend())
    cout << "Element was not found." << endl;
else
    cout << format("Element {} at index {}.", value, posElement - a1.cbegin());
```


## ranges::any_of, ranges::all_of , ranges::none_of


## swap, iter_swap, ranges::swap_ranges

## itoa

```c++
#include <numeric>
array<int, 10> a3{};
iota(a3.begin(), a3.end(), 11);
```

## reduce 

The `reduce` algorithm is similar to the accumulate algorithm but does **not** guarantee the order in which the elements are processed. This difference in operation is why the `reduce` algorithm **can be parallelized** for better performance, but the `accumulate` algorithm **cannot**.

```c++
#include <functional> // for std::plus and std::multiply
#include <numeric> // for std::reduce
array ar{ 1,2,3,4,5,6,7,8 };
int mul{ reduce(ar.begin(), ar.end(), 1, multiplies{}) };
int add{ reduce(ar.begin(), ar.end(), 0, plus{})};
```


