# map - reduce - filter
---

## generate some data for tests

https://www.json-generator.com/

e.g.

```json
[
  '{{repeat(100,120)}}',
  {
    index: '{{index()}}',
    guid: '{{guid()}}',
    age: '{{integer(15,40)}}',
    name: '{{firstName()}} {{surname()}}',
    gender: '{{gender()}}',
    email: '{{email()}}',
    address: '{{integer(100, 999)}} {{street()}}, {{city()}}, {{state()}}, {{integer(100, 10000)}}',
  }
]
```

it generates something like :

```json
[
  {
    "index": 0,
    "guid": "20d31679-bf7b-46e7-b932-f29afa77f62d",
    "age": 24,
    "name": "Kelley Wilkinson",
    "gender": "male",
    "email": "kelleywilkinson@cytrek.com",
    "address": "897 Leonard Street, Nadine, American Samoa, 6915"
  },
  {
    "index": 1,
    "guid": "3c41d255-6f2c-4abb-95c1-d69a204c3f98",
    "age": 27,
    "name": "Emily Mayer",
    "gender": "female",
    "email": "emilymayer@cytrek.com",
    "address": "298 Lott Avenue, Keller, North Carolina, 736"
  } ...
```

## Method Chaining 

**Method chaining** is an **OOP** pattern that allows multiple methods to be called in a single statement. When these methods all belong to the same object, method chaining is referred to as **method cascading**.

the functional standard approach:

```js
concat(toLowerCase(substring('Functional Programming', 1, 10))),' is fun');
```

vs. the method-chainig approach

```js
'Functional Programming'.substring(0, 10).toLowerCase() + ' is fun';
```

**Method-cascanding** can be used on arrays and JSON objects.


## Function Chaining 

Object-oriented programs use inheritance as the main mechanism for code reuse. The **OOP** approach is having generic and derived from the generic types more specialized types.

**Functional programming** takes a different approach. Instead of creating new data structure classes to meet specific needs, it uses common ones like arrays and applies a number of coarse-grained, higher-order operations that are agnostic to the underlying representation of the data. 

### Lambda Expresions

**lambda expressions** are known as **fat-arrow functions** in the JavaScript world.

A lot of functional JavaScript code is based on processing lists of data; hence, the name of the original functional language, **LISP (list processing)**, from which JavaScript is derived. 



