# Python 
<hr>
## **zip()** function

**zip()** function creates an **iterator** that will aggregate elements from two or more **iterables**. 

Returns an iterator of tuples, where the i-th tuple contains the i-th element from each of the argument sequences or iterables. The iterator stops when the **shortest** input iterable is exhausted. 

```python
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7, 8]
print(zip(list1, list2))
print(list(zip(list1, list2)))
```
output
```
<zip object at 0x7f95e9671c40>
[(1, 3), (2, 4), (3, 5), (4, 6), (5, 7)]
```
getting all the elements if lists are not equal:
```python

from itertools import zip_longest
list1 = [1, 2, 3, 4]
list2 = [3, 4, 5, 6, 7, 8]
print(zip_longest(list1, list2))
print(list(zip_longest(list1, list2)))
print(list(zip_longest(list1, list2, fillvalue='?')))
```
output:
```
<itertools.zip_longest object at 0x7f963c70d0e0>
[(1, 3), (2, 4), (3, 5), (4, 6), (None, 7), (None, 8)]
[(1, 3), (2, 4), (3, 5), (4, 6), ('?', 7), ('?', 8)]
```

#### Traversing lists in parallel
```python
letters = ['a', 'b' , 'c']
numbers = [1, 2, 3]
for (l,n) in zip(letters, numbers):
    print(f"{l} - {n} ")
```
output:
```
a - 1 
b - 2 
c - 3 
```

#### Traversing dictionaries in parallel

```python
dict1 = { 
    "name": "james",
    "age" : 20,
    "job" : "software engineer"
}
dict2 = {
    "name": "ana",
    "age" : 30,
    "job" : "web designer"
}
for (k1, v1), (k2, v2) in zip( dict1.items(), dict2.items()):
    print(f"{k1} -> {v1}   {k2}->{v2}")
```
output:
```
name -> james   name->ana
age -> 20   age->30
job -> software engineer   job->web designer
```

#### Unzipping a sequence

```python
pairs = [(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd')]
numbers, letters = zip(*pairs)
print(numbers)
print(list(numbers))
print(letters)
print(list(letters))
```
output:
```
(1, 2, 3, 4)
[1, 2, 3, 4]
('a', 'b', 'c', 'd')
['a', 'b', 'c', 'd']
```

#### Building Dictionaries

```python
fields = ["name", "last_name", "age", "job"]
values = ["james", "johnson", 29, "Software Engineer"]

dict1 = dict(zip(fields, values))
print(dict1)
```
output
```
{'name': 'james', 'last_name': 'johnson', 'age': 29, 'job': 'Software Engineer'}
```

**note** building dictionary from a tuple:
```python
tuple2 = ("name", "james")
list2 = list()
list2.append(tuple2)
dict2 = dict(list2)
print(tuple2)
print(list2)
print(dict2)
```
output
```
('name', 'james')
[('name', 'james')]
{'name': 'james'}
```

**note** building a dictionary from a list:
```python
new_job = ["Python Consultant"]
field = ["job"]
dicto = {}
dicto.update(zip(field, new_job))
print(dicto)
```
output
```
{'job': 'Python Consultant'}
```

