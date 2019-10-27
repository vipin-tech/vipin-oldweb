---
title: Unexplored and less famous module in python
date: 2019-10-27
tags: [python, python for data science, python data structures]
header:
  image: "/images/python.gif"
permalink: /blogs/
author: "Vipin Ragashetti"
excerpt: "Python, Data Structures, Data Science"
---

Collections is a built-in Python module that implements specialized container datatypes providing alternatives to Python’s general purpose built-in containers such as dict, list, set, and tuple.

Some of the useful data structures present in this module are:

1. namedtuple()

The data stored in a plain tuple can only be accessed through indexes as can be seen in the example below:

```python
      plain_tuple = (10,11,12,13)
      plain_tuple[0]
      10
      plain_tuple[3]
      13
```

We can’t give names to individual elements stored in a tuple. Now, this might not be needed in simple cases. However, in case a tuple has many fields this might be kind of a necessity and will also impact the code’s readability.
It is here that namedtuple’s functionality comes into the picture. It is a function for tuples with Named Fields and can be seen as an extension of the built-in tuple data type. Named tuples assign meaning to each position in a tuple and allow for more readable, self-documenting code. Each object stored in them can be accessed through a unique (human-readable) identifier and this frees us from having to remember integer indexes. Let’s see its implementation.

```python
    from collections import namedtuple
    fruit = namedtuple('fruit','number variety color')
    guava = fruit(number=2,variety='HoneyCrisp',color='green')
    apple = fruit(number=5,variety='Granny Smith',color='red')
```

We construct the namedtuple by first passing the object type name (fruit) and then passing a string with the variety of fields as a string with spaces between the field names. We can then call on the various attributes:

```python
    guava.color
    'green'
    apple.variety
    'Granny Smith'
```

Namedtuples are also a memory-efficient option when defining an immutable class in Python.

2. Counter

Counter is a dict subclass which helps to count hashable objects. The elements are stored as dictionary keys while the object counts are stored as the value. Let’s work through a few examples with Counter.

```python
    # Importing Counter from collections

    from collections import Counter

    # With Strings

    c = Counter('abcacdabcacd')
    print(c)
    Counter('a': 4, 'c': 4, 'b': 2, 'd': 2)

    # With lists

    lst = [5,6,7,1,3,9,9,1,2,5,5,7,7]
    c = Counter(lst)
    print(c)
    Counter('a': 4, 'c': 4, 'b': 2, 'd': 2)

    # With Sentence

    s = 'the lazy dog attacked over another lazy dog'
    words = s.split()
    Counter(words)
    Counter('another': 1, 'dog': 2, 'attacked': 1, 'lazy': 2, 'over': 1, 'the': 1)
```

*Counter objects support three methods beyond those available for all dictionaries:*

* *elements*
Returns a count of each element and If an element’s count is less than one, it is ignored.

```python
    c = Counter(a=3, b=2, c=1, d=-2)
    sorted(c.elements())
    ['a', 'a', 'a', 'b', 'b', 'c']
```

* *most_common([n])*
Returns a list of the most common elements with their counts. The number of elements has to be specified as n. If none is specified it returns the count of all the elements.

```python
    s = 'the lazy dog attacked over another lazy dog'
    words = s.split()
    Counter(words).most_common(3)
    [('lazy', 2), ('dog', 2), ('the', 1)]
```

**Common patterns when using the Counter() object**

```python
      sum(c.values())                 # total of all counts
      c.clear()                       # reset all counts
      list(c)                         # list unique elements
      set(c)                          # convert to a set
      dict(c)                         # convert to a regular dictionary c.items()# convert to a list like (elem, cnt)
      Counter(dict(list_of_pairs))    # convert from a list of(elem, cnt)
      c.most_common()[:-n-1:-1]       # n least common elements
      c += Counter()                  # remove zero and negative counts
```

3. defaultdict

Dictionaries are an efficient way to store data for later retrieval having an unordered set of key: value pairs. Keys must be unique and immutable objects.

```python
    fruits = 'apple':300, 'guava': 200
    fruits['guava']
    200
```

Things are simple if the values are ints or strings. However, if the values are in the form of collections like lists or dictionaries, the value (an empty list or dict) must be initialized the first time a given key is used. defaultdict automates and simplifies this stuff. The example below will make it more obvious:

```python
      d =
      print(d['A'])

      Here, the Python dictionary throws an error since ‘A’ is not currently in the dictionary. Let us now run the same example with defaultdict.

      ```python
      from collections import defaultdict
      d = defaultdict(object)
      print(d['A'])
      <object object at 0x7fc9bed4cb00>
```

The defaultdict in contrast will simply create any items that you try to access (provided of course they do not exist yet).The defaultdict is also a dictionary-like object and provides all methods provided by a dictionary. However, the point of difference is that it takes the first argument (default_factory) as a default data type for the dictionary.

4. OrderedDict
An OrderedDict is a dictionary subclass that remembers the order in which that keys were first inserted. When iterating over an ordered dictionary, the items are returned in the order their keys were first added. Since an ordered dictionary remembers its insertion order, it can be used in conjunction with sorting to make a sorted dictionary:

+ regular dictionary

```python

    d = 'banana': 3, 'apple': 4, 'pear': 1, 'orange': 2

```

+ dictionary sorted by key

```python
    OrderedDict(sorted(d.items(), key=lambda t: t[0]))
    OrderedDict([('apple', 4), ('banana', 3), ('orange', 2), ('pear', 1)])
```

+ dictionary sorted by value

```python

    OrderedDict(sorted(d.items(), key=lambda t: t[1]))
    OrderedDict([('pear', 1), ('orange', 2), ('banana', 3), ('apple', 4)])

```

+ dictionary sorted by the length of the key string

```python

        OrderedDict(sorted(d.items(), key=lambda t: len(t[0])))
        OrderedDict([('pear', 1), ('apple', 4), ('banana', 3), ('orange', 2)])

```

**Point to be noted: from python 3.6+ dictionary maintains the insertion order.**


## Coming Up!

### deque, chainmap
