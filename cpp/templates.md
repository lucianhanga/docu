# Templates
---

A template enables **compile-time** (or static) **polymorphism** by specifying capabilities generically, then letting the compiler instantiate the template, generating type-specific code specializations on demand. 

**Class templates** are called **parameterized types** because they require one or more parameters to tell the compiler how to customize a class template to form a **class-template specialization** from which objects can be instantiated. 

```c++
template<typename T>
class Stack {
public:
   // return the top element of Stack
   const T& top() const {return stack.front();}

   // push an element onto Stack
   void push(const T& pushValue) {stack.push_front(pushValue);}

   // pop an element from Stack
   void pop() {stack.pop_front();}

   // determine whether Stack is empty
   bool isEmpty() const {return stack.empty();}

   // return size of Stack
   size_t size() const {return stack.empty();}
private:
   std::deque<T> stack{}; // internal representation of Stack
};
```

The compiler associates the **type parameter** with a **type argument** when you instantiate the class template. At that point, the **compiler** generates **a copy of** the class template in which all occurrences of the type parameter are replaced with the specified type. Compilers generate definitions only for the portions of a template used in your code.

### CTAD - Class Template Argument Deduction

```c++
vector vec{10,20,30,40};
// is equivalent with
vector<int> vec {10,20,30,40};
```

