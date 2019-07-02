# Python cheatsheet

A simple cheatsheet for python beginners

## Virtual environment

First things first. It is good practice to work in a virtual environment.
This way, you can work on multiple projects with different dependencies
without causing a mess.

Create the environment:

`python3 -m venv venv`

Load the environment:

`source venv/bin/activate`


## Style matters

Readability counts. Your coding style should be PEP-8 compliant,
unless you absolutely need to do something different, e.g. when using
some libraries that require so.

A few examples:

```python
def my_cool_function():  # very_good
    pass


def myCoolFunction():  # veryBad
    pass
    
```

**There are two empty lines between the functions in the main code**

Same goes for variables:

```python
my_variable = 10  # very_good
myVariable = 10  # veryBad

```

For classes, it is quite the opposite. UpperCamelCase should be used.

```python
class MyCoolClass:  # VeryGood
    pass


class my_cool_class:  # very_bad
    pass
    
```

**There are two empty lines between the classes in the main code**


Use uppercase for "constants" (Python doesnt really have costants)

```python
MY_COSTANT = 10  # VERY_NICE
my_costant = 10  # very_bad

```

**To add comment next to a line of code, let `#` be preceded by _two_ spaces**


## Use __main__

To have a clean code that runs like `python myscript.py`, dont just put code
into the file, organize it neatly

```python
def first_function():
    pass
    

def second_function():
    pass
    

if __name__ == '__main__':
    first_function()
    second_function()

```

Always end a script with a new line

## Do not shadow names

Python has some builtin variables and functions. DO NOT SHADOW THEM.

e.g.:

```python
file = "my/file.txt"  # very, very bad

def open(path):  # I think I might die for this
    pass

```

Shadowing can also be a matter of scope:

```python
def add(a, b):
    c = 2  # shadows 'c' from outer scope
    return a + b + c
    
if __name__ == "__main__":
    c = 10
    print(add(1, 2))

```


## Beware of objects' reference behavior

```python
my_list = [1, 2, 3]
my_new_list = my_list

my_new_list.append(4)

print(my_list)
# >>> [1, 2, 3, 4]

```

**Same goes for `dict`, `classes` and in general any other object**

So, to actually copy:

```python
my_list = [1, 2, 3]
my_other_list = my_list.copy()
# or
my_other_list = my_list[:]

```

But beware, if inside the list are contained other objects, this wont work:

```python
my_dict = dict(a=1, b=2)
my_list = [1, 2, my_dict]
my_other_list = my_list.copy()
my_dict["b"] = 5

print(my_other_list)
# >>> [1, 2, {'a': 1, 'b': 5}]

```

To avoid this problem, use deepcopy from the copy library

```python
import copy

my_dict = dict(a=1, b=2)
my_list = [1, 2, my_dict]
my_other_list = copy.deepcopy(my_list)
my_dict["b"] = 5

print(my_other_list)
# >>> [1, 2, {'a': 1, 'b': 3}]

```

## Some neat tricks

### enumerate
Sometimes you may want to get the index and the value in a list

```python
my_list = ["a", "b", "c"]
for i, c in enumerate(my_list):
    print(i, c)

# >>> 0, 'a'
# >>> 1, 'b'
# >>> 2, 'c'
```

### zip

Sometimes you may want to iterate two lists at once
```python
first_list = [1, 2, 3]
second_list = ["a", "b", "c"]

for x, y in zip(first_list, second_list):
    print(x, y)

# >>> 1, 'a'
# >>> 2, 'b'
# >>> 3, 'c'
```


### dicts

#### Use get

Sometimes you are not sure if a dictionary has a certain key

```python
my_dict = dict(a=1, b=2, c=3)

# DONT:
if "a" in my_dict.keys():
    v = my_dict["a"]
    
# DO:
v = my_dict.get("a")

v = my_dict.get("z")  # returns None

v = my_dict.get("x", 10)  # the second value will be returned if the given key is not present

```

#### use items()

Sometimes you may need to iterate over keys and values

```python
my_dict = dict(a=1, b=2, c=3)
for key, value in my_dict.items():
    print(key, value)

```

### Collections

[Please explore the library here](https://docs.python.org/3.7/library/collections.html)

#### use defaultdict

Sometimes you may need to dynamically build a complex dict

DONT:
```python
d = dict()
d["a"] = []
d["a"].append(1)

```

DO:
```python
from collections import defaultdict

d = defaultdict(list)
d["a"].append(1)

```

If you REALLY, REALLY need a complex dict dynamically built, you
can use nested defaultdicts with lambda functions

```python
from collections import defaultdict

my_ddict = defaultdict(lambda : defaultdict(list))
my_ddict["a"]["x"].append(1)

```

#### use Counter
```python
from collections import Counter

def count_stuff(my_string):
    alph = Counter()
    for char in my_string:
        alph[char] += 1
    return alph
    
# or EVEN BETTER:

def count_stuff(my_string):
    return Counter(my_string)
    
```

## Write classes like a pro

### Coming soon
