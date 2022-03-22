# Accumulate

```c++
#include <numeric>
using namespace std;

int main() {

    constexpr size_t arrSize{ 10 }; // evaluated at compile time vs. const which is at running time
    array<unsigned int, arrSize> arr{ 1,2,3,4,5,6,7,8,9,10 };
    
    auto addEvenNumbers = [](unsigned int acc, unsigned int val) {return acc + (val % 2 == 0 ? val : 0); };
    unsigned int sumAll{ accumulate(begin(arr), end(arr), gsl::narrow_cast<unsigned int>(0)) };

    unsigned int sumEven{ accumulate(begin(arr), end(arr), gsl::narrow_cast<unsigned int>(0), addEvenNumbers )};

    unsigned int mulAll{ accumulate(begin(arr), end(arr), gsl::narrow_cast<unsigned int>(1),
        [](const auto& acc, const auto& val) { return acc * val;  }) };

    cout << "Sum All:  " << sumAll  << endl;
    cout << "Sum Even: " << sumEven << endl;
    cout << "Mul All: "  << mulAll  << endl;

    return 0;
}
```