
when reached the end of fine a bit is set in the iostream object which needs also to be manually cleared when the `seekg` is moved from the end of the file to another position.

```c++
input.seekg(0);
input.clear();
```
`tellg` and `tellp` the number of byes from the beginning of the file from the current position pointer.


read quoted text
```c++
cin << quoted(name) << endl;
```

```c++
#include <iostream>
#include <fstream>
#include <format>
#include <iomanip>

using namespace std;


int main(int argc, char* argv[]) {

    if (ofstream os{ "data.txt"s, ios::out }; os) {
        int id{ 0 };
        string name{};
        double account{ 0.0 };

        cout << "Introduce: id name account" << endl;
        cout << "?";

        while (cin >> id >> quoted(name) >> account) {
            // os << format("{} {} {}", id, name, account) << endl;
            os << id << " " << quoted(name) << " " << account << endl;
            cout << "?"; 
        }
    }
    else {
        cout << "error opening file for writing." << endl;
        exit(1);
    }

    cout << "   id " << "     name   " << " account  " << endl;
    cout << "----"   << "------------" << "----------" << endl;

    if (ifstream is{ "data.txt"s, ios::in }; is) {
        int id{ 0 };
        string name{};
        double account{ 0.0 };
        while (is >> id >> quoted(name) >> account) {
            cout << format("{:>4d} {:>12s} {:>8.2f}", id, name, account) << endl;
        }
    }
    else {
        cout << "error operining the file for reading." << endl;
        exit(1);
    }
    return 0;
}
```

string streams 

```c++
    string inputData{ "10 20 30 40 50 60 70 80 90"s };
    istringstream iss{ inputData, ios::in };
    int value{ 0 };
    while (iss >> value) {
        cout << "value: " << value << endl;
    }
```