Before diving in, we need to understand what we are actually doing when we are "sorting".

We need to be able to do 2 things in order to sort.
1. Compare 2 elements (sort uses the < (```__lt__()```) operator)
2. Move elements

Sorting numbers or texts is simple. However, you might have specific interests as to how you want the data to be sorted. To suit your interests, Python provides useful features to customize sorting in different ways.
(Especially #1, #2: not really)


One more fact worth keeping in mind while designing the comparison function is that
- If you can compare 2 elements, you can sort the whole list (poset)
- if all neighboring elements are sorted, the list is sorted

## Method 1: Sorting with Custom Key
you might want to specify the "key" for comparing 2 objects. Python's sort supports this function.

```python
>>> student_tuples = [
...     ('john', 'A', 15),
...     ('jane', 'B', 12),
...     ('dave', 'B', 10),
... ]

>>> sorted(student_tuples, key=lambda student: student[2])   # sort by age
>>> sorted(student_tuples, key=itemgetter(2))   # same thing
```

```python
>>> class Student:
...     def __init__(self, name, grade, age):
...         self.name = name
...         self.grade = grade
...         self.age = age
...     def __repr__(self):
...         return repr((self.name, self.grade, self.age))

>>> student_objects = [
...     Student('john', 'A', 15),
...     Student('jane', 'B', 12),
...     Student('dave', 'B', 10),
... ]

>>> sorted(student_objects, key=lambda student: student.age)   # sort by age
>>> sorted(student_objects, key=attrgetter('age'))   # same thing
```

## Method 2: Sorting with Comparison Functions
You can also define custom "comparison" functions to compare 2 objects.

## Lambda function
```python
data = [("Alice", 25), ("Bob", 30), ("Charlie", 25)]

sorted_data = sorted(data, key=lambda x: (x[1], x[0]))  # Sort by age, then by name
```


## cmp_to_key() function
Until Python2, there was ```cmp``` parameter to do this, but it was removed in Python3.

For Python 3, you can use ```functools.cmp_to_key```.

What this does is, it converts positive, 0, negative function value to ordering of values.

Predefined function
```python
from functools import cmp_to_key

def compare(x, y):
    if x < y:
        return -1
    elif x > y:
        return 1
    return 0

sorted_numbers = sorted(numbers, key=cmp_to_key(compare))
```


## Method 3: Redefining the Comparison Operator
Instead of using above methods provided by Python's sort, you may also define the comparison operator ```__lt__()``` (<)

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __lt__(self, other):
        return self.age < other.age

people.sort() 
```


## Some examples
### Sorting by the largest concatenation of integers
```python
def compare(x, y):
    # Compare the strings of their numerical value and return positive if "yx" greater than "xy"
    return (int(y + x) - int(x + y))

numbers = list(map(str, numbers))
    
numbers.sort(key=cmp_to_key(compare))

```