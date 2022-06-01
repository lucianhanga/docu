## Rule of 0,3,5
---

If the user does no t 

### Rule of 3

If a class requires a user-defined **destructor**, or a user-defined **copy constructor** or a user-defined **assignment operator** it most probably require all **three** of them.

```c++
class RuleOfThree {
public:
    explicit RuleOfThree(int val) : m_pVal(new int) {
        cout << "constructor" << endl;
        *m_pVal = val;
    };

    RuleOfThree(const RuleOfThree& other) : m_pVal(nullptr) {
        cout << "copy constructor" << endl;
        RuleOfThree tmp{ *other.m_pVal };
        std::swap(m_pVal, tmp.m_pVal);
    };

    RuleOfThree& operator = (const RuleOfThree& other) {
        cout << "assignment operator" << endl;
        RuleOfThree tmp{ other };
        std::swap(m_pVal, tmp.m_pVal);
        return *this;
    };

    RuleOfThree(RuleOfThree&& other) = delete;
    RuleOfThree& operator = (RuleOfThree&& other) = delete;

    virtual ~RuleOfThree() {
        cout << "destructor" << endl;
        if (m_pVal != nullptr) {
            delete m_pVal;
            m_pVal = nullptr;
        }
    };
private:
    int* m_pVal;
};

```


### Rule of Five

```c++
class RuleOfFive {
public:
    explicit RuleOfFive(int val) noexcept : m_pVal(new int) {
        cout << "constructor" << endl;
        *m_pVal = val;
    };

    explicit RuleOfFive(const RuleOfFive& other) noexcept : m_pVal(nullptr) {
        cout << "copy constructor" << endl;
        RuleOfFive tmp{ *other.m_pVal };
        std::swap(m_pVal, tmp.m_pVal);
    };  

    RuleOfFive& operator = (const RuleOfFive& other) noexcept {
        cout << "assignment operator" << endl;
        RuleOfFive tmp{ other };
        std::swap(m_pVal, tmp.m_pVal);
        return *this;
    };

    RuleOfFive(RuleOfFive&& other) noexcept {
        cout << "move constructor" << endl;
        std::swap(m_pVal, other.m_pVal);
        other.m_pVal = nullptr;
    };

    RuleOfFive& operator = (RuleOfFive&& other) noexcept {
        cout << "assignment move operator" << endl;
        std::swap(m_pVal, other.m_pVal);
        return *this;
    };

    virtual ~RuleOfFive() {
        cout << "destructor" << endl;
        if (m_pVal != nullptr) {
            delete m_pVal;
            m_pVal = nullptr;
        }
    };
private:
    int* m_pVal;
};

```

### Rule of Zero

```c++
class RuleOfZero {
public:
    explicit RuleOfZero(int val) noexcept : m_pVal(val) { };

    RuleOfZero(const RuleOfZero& other) = default;
    RuleOfZero& operator = (const RuleOfZero& other) = default;
    RuleOfZero(RuleOfZero&& other) = default;
    RuleOfZero& operator = (RuleOfZero&& other) = default;
    virtual ~RuleOfZero() = default;
private:
    int m_pVal;
};
```
