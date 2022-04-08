## Projections
---




```c++
#include <iostream>
#include <string>
#include <array>
#include <string_view>
#include <format>
#include <ranges>
#include <algorithm>


using namespace std;

class Employee {

    friend std::ostream& operator << (std::ostream& output, const Employee& e);

public:
    Employee(string_view firstname, string_view lastname, int salary) :
        m_firstname{ firstname },
        m_lastname{ lastname },
        m_salary{ salary } {
    };
    int getSalary() const { return m_salary; };


private:
    string m_firstname;
    string m_lastname;
    int m_salary;
};

std::ostream& operator << (std::ostream& output, const Employee& e) {
    // output << e.m_firstname << " " << e.m_lastname << " " << e.m_salary << endl;
    output << format("{:>15s}{:>15s}  {:>5}", e.m_firstname, e.m_lastname, e.m_salary);
    return output;
};


int main() {

    array employees{
        Employee{"James", "Tores", 1000},
        Employee{"Oliver", "Johnson", 2300},
        Employee{"Adrian", "Kamel", 900},
        Employee{"Elena", "Jamiro", 1300},
        Employee{"Alina", "Cocoro", 700},
    };

    // print the array of employees
    //for (Employee& e : employees) {
    //    cout << e << endl;
    //}

    // nother way to print the array
    std::ostream_iterator<Employee> output(std::cout, "\n");
    cout << "unsorted" << endl;
    std::ranges::copy(employees, output);
    cout << endl;

    // order the employees
    std::ranges::sort(employees, {}, [](auto element) { return element.getSalary(); });
    // this would work too
    // std::ranges::sort(employees, {}, &Employee::getSalary);

    cout << "sorted" << endl;
    std::ranges::copy(employees, output);
    cout << endl;

    return 0;
}
```

The **second argument** (`{}`) is the **binary predicate** function that sort uses to compare elements when determining their sort order. The notation `{}` indicates that sort should use the **default** binary predicate function specified in sort’s definition—that is, `std::ranges::less`.

The last argument of `sort` specifies the **projection**. This **unary function** receives an element from the range and returns a **portion of that element**. Here, we implemented the unary function as a lambda that returns its Employee argument’s salary. The **projection** is applied **before** sort compares the elements, so rather than comparing entire Employee objects to determine their sort order, sort compares only the Employees’ salaries.

!!!. To be used as a projection, the member function must be public and must not be overloaded. Also, it must have no parameters because the std::ranges algorithms cannot receive additional arguments to pass to the member function specified in the projection.