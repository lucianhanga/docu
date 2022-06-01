# Customer Iterator & Container

C++ Core Guidelines recomends to use templates when implementing any class representing an container or a range of values:
[C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rt-cont)

The definition of the **custom iterators** and **custom container** are contained into a **Single Header file**.

The **iterators** power in descending order:

- contiguous iterators
- random access iterators
- bidirectional iterators
- forward iterators
- input iterators & output iterators

[iterators category and properties](https://www.cplusplus.com/reference/iterator/)

An **iterator** (custom iterator) should contain the following:
