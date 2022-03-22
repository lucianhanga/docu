## Function Object / Functor

Any algorithm that can receive a **lambda** or **function pointer** can also receive a **function object** (also called a **functor**)— that is, an object of a class that overloads the **function-call operator** (parentheses) with a function named `operator()`. 

The overloaded `operator()` must meet the algorithm’s requirements for the number of parameters and the return type.

Function objects can be used syntactically and semantically like a lambda or a function pointer. The `operator()` function is invoked using the object’s name followed by parentheses containing the arguments. Most algorithms can use lambdas, function pointers and function objects interchangeably.

example of functor: 


```c++
    std::less<int> smaller{};
    cout << smaller(10, 20) << endl;
```

https://en.cppreference.com/w/cpp/utility/functional

The `std::ranges` algorithms that compare elements for ordering use `less<T>` as their **default predicate** function argument.

```c++
int sumFunc(int element, int sum) {
    return element + sum;
};

class sumClass {
public:
    int operator() (int element, int sum) {
        return element + sum;
    };
};

auto sumLambda = [](int element, int sum) { return element + sum;  };

int main() {

    ostream_iterator<int> output{ std::cout, " " };

    array arr1{ 1,2,3,4,5,6,7,8,9,10 };

    cout << "array: ";
    std::ranges::copy(arr1, output);
    cout << endl;

    cout << std::accumulate(arr1.begin(), arr1.end(), 0, std::plus{} ) << endl;
    cout << std::accumulate(arr1.begin(), arr1.end(), 0, sumFunc     ) << endl;
    cout << std::accumulate(arr1.begin(), arr1.end(), 0, sumClass{}  ) << endl;
    cout << std::accumulate(arr1.begin(), arr1.end(), 0, sumLambda   ) << endl;

}
```