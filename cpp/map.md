# map
---

```c++

#include <iostream>
#include <ranges>
#include <map>
#include <string>
#include <format>
#include <algorithm>

using namespace std;
using namespace std::string_literals;

int main() {

    std::map<std::string, int> myMap {
        {"james", 10},
        {"tom", 12},
        {"rumba" ,6},
        {"ole", 21},
        {"ana" ,2 }
    };

    cout << "james: " << myMap["james"] << endl;
    cout << "james: " << myMap.find("james")->second << endl << endl;

    for(const std::map<std::string, int>::value_type & p : myMap) {
        cout << format("{:>10s} - {:>2}", p.first, p.second) << endl;
    }
    cout << endl;
    for (const auto& [key, value] : myMap) {
        cout << format("{:>10s} - {:>2}", key, value) << endl;
    }
    cout << endl;
    for (auto p = myMap.begin(); p != myMap.end(); p++) {
        cout << format("{:>10s} - {:>2}", p->first, p->second) << endl;
    }
    cout << endl;
    auto displayPair{ [](auto p) { cout << format("{:>10s} - {:>2}", p.first, p.second) << endl; } };
    std::ranges::for_each(myMap, displayPair);
    cout << endl;

};

```