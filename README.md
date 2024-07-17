# Python Data Structures
## Table of Contents
- [Dictionaries, Maps, and Hash Tables](#dictionaries-maps-and-hash-tables)
  - [dict](#dict)
  - [collections.OrderedDict: Remember the Insertion Order of Keys](#collectionsordereddict-remember-the-insertion-order-of-keys)
  - [collections.defaultdict: Return Default Values for Missing Keys](#collectionsdefaultdict-return-default-values-for-missing-keys)
  - [collections.ChainMap: Search Multiple Dictionaries as a Single Mapping](#collectionschainmap-search-multiple-dictionaries-as-a-single-mapping)
  - [types.MappingProxyType: A Wrapper for Making Read-Only Dictionaries](#typesmappingproxytype-a-wrapper-for-making-read-only-dictionaries)
- [Array Data Structures](#array-data-structures)
  - [list: Mutable Dynamic Arrays](#list-mutable-dynamic-arrays)
  - [tuple: Immutable Containers](#tuple-immutable-containers)
  - [array.array: Basic Typed Arrays](#arrayarray-basic-typed-arrays)
  - [str: Immutable Arrays of Unicode Characters](#str-immutable-arrays-of-unicode-characters)
  - [bytes: Immutable Arrays of Single Bytes](#bytes-immutable-arrays-of-single-bytes)
  - [bytearray: Mutable Arrays of Single Bytes](#bytearray-mutable-arrays-of-single-bytes)
  - [Arrays in Python: Summary](#arrays-in-python-summary)
- [Records, Structs, and Data Transfer Objects](#records-structs-and-data-transfer-objects)
  - [dict: Simple Data Objects](#dict-simple-data-objects)
  - [tuple: Immutable Groups of Objects](#tuple-immutable-groups-of-objects)
  - [Write a Custom Class: More Work, More Control](#write-a-custom-class-more-work-more-control)
  - [dataclasses.dataclass: Python 3.7+ Data Classes](#dataclassesdataclass-python-37-data-classes)
  - [collections.namedtuple: Convenient Data Objects](#collectionsnamedtuple-convenient-data-objects)
  - [typing.NamedTuple: Improved Namedtuples](#typingnamedtuple-improved-namedtuples)
  - [struct.Struct: Serialized C Structs](#structstruct-serialized-c-structs)
  - [types.SimpleNamespace: Fancy Attribute Access](#typessimplenamespace-fancy-attribute-access)
- [Sets and Multisets](#sets-and-multisets)
  - [Set: Mutable](#set-mutable)
  - [Frozenset: Immutable](#frozenset-immutable)
  - [Counter: Multiset](#counter-multiset)
  - [Summary: Sets and Multisets](#summary-sets-and-multisets)
- [Stacks (LIFOs)](#stacks-lifos)
  - [list: Simple Built-in Stacks](#list-simple-built-in-stacks)
  - [collections.deque: Fast and Robust Stacks](#collectionsdeque-fast-and-robust-stacks)
  - [queue.LifoQueue: Locking Semantics](#queuelifoqueue-locking-semantics)
  - [Summary: Stacks](#summary-stacks)
- [Queues (FIFOs)](#queues-fifos)
  - [Using Lists for Queues](#using-lists-for-queues)
  - [collections.deque: Fast and Robust Queues](#collectionsdeque-fast-and-robust-queues)
  - [queue.Queue: Locking Semantics for Parallel Computing](#queuequeue-locking-semantics-for-parallel-computing)
  - [multiprocessing.Queue: Shared Job Queues](#multiprocessingqueue-shared-job-queues)
  - [Summary: Queues](#summary-queues)
- [Priority Queues](#priority-queues)
  - [list: Manually Sorted Queues](#list-manually-sorted-queues)
  - [heapq: List-Based Binary Heaps](#heapq-list-based-binary-heaps)
  - [queue.PriorityQueue: Beautiful Priority Queues](#queuepriorityqueue-beautiful-priority-queues)
  - [Priority Queues in Python: Summary](#priority-queues-in-python-summary)

## Dictionaries, Maps, and Hash Tables

In Python, dictionaries (or dicts for short) are a central data structure. Dicts store an arbitrary number of objects, each identified by a unique dictionary key.

### Key Features:
- **Efficient Lookup:** Allows for quick retrieval of values associated with a key.
- **Insertion and Deletion:** Supports efficient insertion and deletion operations.
- **Flexible:** Stores any Python object as values, and keys can be of various types (immutable types like strings and numbers are commonly used).
- **Analogous to Real-World Maps:** Similar to how a phone book allows quick lookup of phone numbers using names, dictionaries enable fast retrieval of values based on keys.

### Terminology:
- **Aliases:** Maps, hashmaps, lookup tables, associative arrays.

### Performance:
- **Lookup:** Typically O(1) on average for retrieval, insertion, and deletion operations, making them highly efficient for large datasets.

### Applications:
- **Common Use:** Data caching, memoization, symbol tables, configurations.
- **Versatility:** Widely used across programming languages and applications due to their efficiency and flexibility.


### dict:

Python's `dict` type provides a flexible and efficient way to manage key-value pairs. 

### Syntax and Initialization:

Dictionaries are initialized using curly braces `{}` and key-value pairs separated by colons `:`:

```
phonebook = {
    "bob": 7387,
    "alice": 3719,
    "jack": 7052,
}

squares = {x: x * x for x in range(6)}

print(phonebook["alice"])  # Output: 3719

print(squares)  # Output: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

```
### Key Restrictions:

Keys in dictionaries must be hashable. Immutable types like strings, numbers, and tuples (if their elements are hashable) are suitable as keys.

### Performance:

Python dictionaries offer average O(1) time complexity for lookup, insert, update, and delete operations due to their hash table implementation.

### Underlying Implementation:

Internally, Python dictionaries are based on hash tables, ensuring efficient storage and retrieval of key-value pairs.

### Specialized Implementations:

While Python's built-in dictionary (`dict`) is optimized for general use cases, specialized third-party implementations like skip lists or B-tree-based dictionaries exist for specific needs.

### Standard Library Enhancements:

Python's standard library includes specialized dictionary implementations that extend upon the `dict` class, offering additional features while maintaining performance.

### collections.OrderedDict: Remember the Insertion Order of Keys

Python's `collections.OrderedDict` is a specialized dictionary implementation from the `collections` module that retains the order of keys as they are inserted.

```
import collections

# Create an OrderedDict with initial key-value pairs
d = collections.OrderedDict(one=1, two=2, three=3)

print(d)
# Output: OrderedDict([('one', 1), ('two', 2), ('three', 3)])

# Add a new key-value pair to the OrderedDict
d["four"] = 4
print(d)
# Output: OrderedDict([('one', 1), ('two', 2), ('three', 3), ('four', 4)])

# Print the keys of the OrderedDict
print(d.keys())
# Output: odict_keys(['one', 'two', 'three', 'four'])
```

### collections.defaultdict: Return Default Values for Missing Keys

The `defaultdict` class is another dictionary subclass from the `collections` module that accepts a callable in its constructor. The callable's return value will be used if a requested key cannot be found.

This can save some typing and make intentions clearer compared to using `get()` or catching a `KeyError` exception in regular dictionaries:

```
from collections import defaultdict

# Create a defaultdict with a default factory of list
dd = defaultdict(list)

# Accessing a missing key creates it and initializes it using the default factory (list() in this example):
dd["dogs"].append("Rufus")
dd["dogs"].append("Kathrin")
dd["dogs"].append("Mr Sniffles")

print(dd["dogs"])
# Output: ['Rufus', 'Kathrin', 'Mr Sniffles']
```
### collections.ChainMap: Search Multiple Dictionaries as a Single Mapping

The `collections.ChainMap` data structure groups multiple dictionaries into a single mapping. Lookups search the underlying mappings one by one until a key is found. Insertions, updates, and deletions only affect the first mapping added to the chain:

```
from collections import ChainMap

dict1 = {"one": 1, "two": 2}
dict2 = {"three": 3, "four": 4}
chain = ChainMap(dict1, dict2)

print(chain)
# Output: ChainMap({'one': 1, 'two': 2}, {'three': 3, 'four': 4})

# ChainMap searches each collection in the chain
# from left to right until it finds the key (or fails):
print(chain["three"])  # Output: 3
print(chain["one"])    # Output: 1
```
### types.MappingProxyType: A Wrapper for Making Read-Only Dictionaries

`MappingProxyType` is a wrapper around a standard dictionary that provides a read-only view into the wrapped dictionary’s data. This class was added in Python 3.3 and can be used to create immutable proxy versions of dictionaries.

`MappingProxyType` can be helpful if, for example, you’d like to return a dictionary carrying internal state from a class or module while discouraging write access to this object. Using `MappingProxyType` allows you to put these restrictions in place without first having to create a full copy of the dictionary:

```
from types import MappingProxyType

writable = {"one": 1, "two": 2}
read_only = MappingProxyType(writable)

# The proxy is read-only:
print(read_only["one"])  # Output: 1

# Attempting to modify the proxy raises an error:
try:
    read_only["one"] = 23
except TypeError as e:
    print(f"TypeError: {e}")

# Updates to the original dictionary are reflected in the proxy:
writable["one"] = 42
print(read_only)  # Output: mappingproxy({'one': 42, 'two': 2})
```
## Arrays Data Structures:

An array is a fundamental data structure available in most programming languages, and it has a wide range of uses across different algorithms.

### Basics of Arrays:

Arrays consist of fixed-size data records that allow each element to be efficiently located based on its index. They store information in adjoining blocks of memory, making them contiguous data structures.

### Real-World Analogy:

A real-world analogy for an array data structure is a parking lot, where each parking spot is indexed and can contain different types of vehicles or be restricted to specific types.

### Performance:

Arrays offer fast lookup times with O(1) complexity for accessing elements by index.


### list: Mutable Dynamic Arrays

Lists are a core part of the Python language and are implemented as dynamic arrays behind the scenes. This allows lists to dynamically adjust their size by allocating or releasing memory as needed when elements are added or removed.

### Features of Lists:

- **Dynamic Sizing:** Lists can grow or shrink dynamically based on the elements they contain, adjusting their memory footprint accordingly.
  
- **Arbitrary Elements:** Python lists can hold arbitrary elements, allowing you to mix different data types within the same list. Since everything in Python is an object, lists can contain a variety of objects including functions.
  
- **Mutability:** Lists are mutable, meaning you can modify their elements after creation. This includes operations like setting values at specific indices, appending elements, and deleting elements.
  
- **Memory Usage:** Due to their ability to store different types of objects, lists are generally less memory-efficient than arrays that store elements of a single type. This is because the elements are not tightly packed in memory.
```
arr = ["one", "two", "three"]
print(arr[0])   # Output: 'one'

# Lists have a nice repr:
print(arr)      # Output: ['one', 'two', 'three']

# Lists are mutable:
arr[1] = "hello"
print(arr)      # Output: ['one', 'hello', 'three']

del arr[1]
print(arr)      # Output: ['one', 'three']

# Lists can hold arbitrary data types:
arr.append(23)
print(arr)      # Output: ['one', 'three', 23]
```
### tuple: Immutable Containers

Tuples are fundamental data structures in Python, similar to lists, but with the key difference that tuples are immutable. Once a tuple is created, its elements cannot be added, removed, or modified. This immutability makes tuples suitable for situations where data should not change after creation.

### Features of Tuples:

- **Immutable:** Elements of a tuple cannot be modified after creation. Operations like item assignment and deletion are not supported.

- **Arbitrary Elements:** Like lists, tuples can hold elements of arbitrary data types, allowing for flexibility in data storage.

- **Memory Efficiency:** Tuples are more memory-efficient than lists for static data because their elements are tightly packed in memory.

```
arr = ("one", "two", "three")
print(arr[0])   # Output: 'one'

# Tuples have a nice repr:
print(arr)      # Output: ('one', 'two', 'three')

# Tuples are immutable:
# Attempting to modify or delete elements raises TypeError
# arr[1] = "hello"
# del arr[1]

# Tuples can hold arbitrary data types:
# Adding elements creates a copy of the tuple
print(arr + (23,))   # Output: ('one', 'two', 'three', 23)
```
### array.array: Basic Typed Arrays

Python’s `array` module provides efficient storage for basic C-style data types such as bytes, 32-bit integers, and floating-point numbers. Arrays created with `array.array` are mutable and offer space efficiency due to their tightly packed storage of elements constrained to a single data type.

### Key Features:

- **Typed Arrays:** Elements in `array.array` are constrained to a single data type, making them more space efficient compared to lists and tuples.
  
- **Mutability:** Similar to lists, `array.array` objects can be modified after creation. They support operations like element assignment, deletion, and appending.

- **Performance:** Due to their typed nature, operations on `array.array` objects can be faster than equivalent operations on lists, especially when dealing with large datasets of a consistent type.

```
import array

arr = array.array("f", [1.0, 1.5, 2.0, 2.5])
print(arr[1])   # Output: 1.5

# Arrays have a nice repr:
print(arr)      # Output: array('f', [1.0, 1.5, 2.0, 2.5])

# Arrays are mutable:
arr[1] = 23.0
print(arr)      # Output: array('f', [1.0, 23.0, 2.0, 2.5])

del arr[1]
print(arr)      # Output: array('f', [1.0, 2.0, 2.5])

arr.append(42.0)
print(arr)      # Output: array('f', [1.0, 2.0, 2.5, 42.0])

# Arrays are "typed":
# Attempting to assign a different type raises TypeError
# arr[1] = "hello"
```
### str: Immutable Arrays of Unicode Characters

In Python 3.x, `str` objects are used to store textual data as immutable sequences of Unicode characters. Each character in a string is itself a `str` object of length 1, making strings a recursively structured data type.

### Key Features:

- **Immutable Nature:** Strings in Python are immutable, meaning once created, their content cannot be changed. Operations like item assignment or deletion raise `TypeError`.

- **Space Efficiency:** String objects are tightly packed and optimized for storing Unicode text, making them efficient in terms of memory usage.

- **Unicode Support:** Strings in Python are designed to handle Unicode characters, making them suitable for internationalization and diverse character sets.

- **Recursive Structure:** Each character within a string is itself a `str` object, contributing to the recursive nature of strings.


```
arr = "abcd"
print(arr[1])       # Output: 'b'

# Strings have a nice repr:
print(arr)          # Output: 'abcd'

# Strings are immutable:
# Modifying or deleting elements raises TypeError
# arr[1] = "e"
# del arr[1]

# Strings can be unpacked into a list for mutable operations:
print(list("abcd"))         # Output: ['a', 'b', 'c', 'd']
print("".join(list("abcd")))    # Output: 'abcd'

# Strings are recursive data structures:
print(type("abc"))      # Output: <class 'str'>
print(type("abc"[0]))   # Output: <class 'str'>
```
### bytes: Immutable Arrays of Single Bytes

In Python, `bytes` objects represent immutable sequences of single bytes, where each byte is an integer in the range 0 ≤ x ≤ 255. These objects are designed for handling binary data efficiently.

### Key Features:

- **Immutable Nature:** Like strings, `bytes` objects are immutable. Once created, their content cannot be changed. Attempts to modify or delete elements will raise `TypeError`.

- **Space Efficiency:** `bytes` objects are tightly packed and optimized for handling binary data, making them efficient in terms of memory usage.

- **Literal Syntax:** `bytes` objects have their own literal syntax for creating objects using byte values.

- **Range Constraints:** `bytes` objects only accept integers within the range 0 to 255. Attempts to use values outside this range will raise a `ValueError`.

- **Conversion to Mutable Type:** While `bytes` are immutable, they can be converted to mutable `bytearray` objects for situations requiring dynamic byte-level operations.

```
arr = bytes((0, 1, 2, 3))
print(arr[1])       # Output: 1

# Bytes literals have their own syntax:
print(arr)          # Output: b'\x00\x01\x02\x03'
arr = b"\x00\x01\x02\x03"

# Only valid `bytes` are allowed:
# bytes((0, 300))   # ValueError: bytes must be in range(0, 256)

# Bytes are immutable:
# Modifying or deleting elements raises TypeError
# arr[1] = 23
# del arr[1]
```
### bytearray: Mutable Arrays of Single Bytes

The `bytearray` type in Python is a mutable sequence of integers within the range 0 ≤ x ≤ 255. It is closely related to the `bytes` object but differs in that a `bytearray` can be modified freely—elements can be overwritten, removed, or added dynamically, causing the array to resize as needed.

### Features of bytearray:

- **Mutability**: Elements of a `bytearray` can be modified after creation, making it suitable for scenarios requiring dynamic changes.
  
- **Representation**: Bytearrays are represented as sequences of bytes, providing a clear and efficient way to handle byte-level data.
  
- **Dynamic Sizing**: The size of a `bytearray` can grow or shrink based on operations like appending elements or deleting existing ones.

```
arr = bytearray((0, 1, 2, 3))
print(arr[1])   # Output: 1

# Bytearray representation
print(arr)      # Output: bytearray(b'\x00\x01\x02\x03')

# Modify elements
arr[1] = 23
print(arr)      # Output: bytearray(b'\x00\x17\x02\x03')

# Delete an element
del arr[1]
print(arr)      # Output: bytearray(b'\x00\x02\x03')

# Append a new element
arr.append(42)
print(arr)      # Output: bytearray(b'\x00\x02\x03*')

# Type constraints
try:
    arr[1] = "hello"
except TypeError as e:
    print(e)    # Output: 'str' object cannot be interpreted as an integer

try:
    arr[1] = 300
except ValueError as e:
    print(e)    # Output: byte must be in range(0, 256)

# Convert to bytes (immutable)
bytes_arr = bytes(arr)
print(bytes_arr)  # Output: b'\x00\x02\x03*'
```

### Arrays in Python: Summary

When working with arrays in Python, you have several built-in data structures to choose from, each suited to different types of data and performance requirements:

1. **Lists**:
   - **Use Case**: Storing arbitrary objects with potentially mixed data types.
   - **Mutability**: Lists are mutable, allowing elements to be added, removed, or modified.
   - **Flexibility**: Suitable for general-purpose use cases where flexibility in data handling is needed.
   
2. **Tuples**:
   - **Use Case**: Immutable storage of elements with mixed data types.
   - **Immutability**: Elements cannot be added or removed after creation, ensuring data integrity.
   - **Efficiency**: Tuples are slightly more memory-efficient than lists due to immutability.
   
3. **array.array**:
   - **Use Case**: Storing numeric data (integers, floats) where performance and memory efficiency are critical.
   - **Typed Arrays**: Ensures elements are of a single data type, optimizing memory usage and performance.
   - **Mutability**: Similar to lists in mutability but constrained to a single data type.
   
4. **str (Strings)**:
   - **Use Case**: Immutable storage of Unicode characters for text data.
   - **Efficiency**: Strings are tightly packed and optimized for Unicode character storage.
   - **Immutability**: Once created, strings cannot be modified, ensuring data integrity.
   
5. **bytes** and **bytearray**:
   - **Use Case**: Handling binary data efficiently.
   - **Immutable vs Mutable**: `bytes` for immutable storage of byte-level data, `bytearray` for mutable operations.
   - **Efficiency**: Both types are optimized for byte-level operations and efficient memory usage.
   
#### Choosing the Right Data Structure:

- **General-Purpose Use**: Start with lists for their flexibility and ease of use. Lists provide fast development speed and are convenient for most programming tasks.
  
- **Performance Considerations**: Transition to specialized data structures like `array.array` or `bytearray` when performance or memory efficiency becomes crucial, especially for numeric or byte-level operations.

- **Immutable Requirements**: Use tuples for immutable collections of data with mixed types or strings for immutable Unicode text storage.

By understanding these distinctions, you can choose the appropriate array-like data structure in Python based on your specific application needs, balancing between flexibility, performance, and memory efficiency.

## Records, Structs, and Data Transfer Objects

Compared to arrays, record data structures provide a fixed number of fields, each with a name and possibly a different type. Python offers several data types to implement records, structs, and data transfer objects. Let's explore these options.

### dict: Simple Data Objects

Dictionaries in Python allow easy creation with concise syntax using literals. They support mutable data objects, but lack robust protection against misspelled field names, potentially leading to unexpected bugs, emphasizing a trade-off between convenience and error resilience.

```
car1 = {
    "color": "red",
    "mileage": 3812.4,
    "automatic": True,
}
car2 = {
    "color": "blue",
    "mileage": 40231,
    "automatic": False,
}

# Dicts have a nice repr:
print(car2)  # {'color': 'blue', 'automatic': False, 'mileage': 40231}

# Get mileage:
print(car2["mileage"])  # 40231

# Dicts are mutable:
car2["mileage"] = 12
car2["windshield"] = "broken"
print(car2)  # {'windshield': 'broken', 'color': 'blue', 'automatic': False, 'mileage': 12}

# No protection against wrong field names,
# or missing/extra fields:
car3 = {
    "colr": "green",
    "automatic": False,
    "windshield": "broken",
}
```
### tuple: Immutable Groups of Objects

Python tuples are immutable data structures used for grouping arbitrary objects. They take up slightly less memory and are faster to construct than lists in CPython.

**Performance Comparison:**
Tuples require fewer bytecode operations to construct compared to lists, as shown in the disassembly examples below.

```
>>> import dis
>>> dis.dis(compile("(23, 'a', 'b', 'c')", "", "eval"))
      0 LOAD_CONST           4 ((23, "a", "b", "c"))
      3 RETURN_VALUE

>>> dis.dis(compile("[23, 'a', 'b', 'c']", "", "eval"))
      0 LOAD_CONST           0 (23)
      3 LOAD_CONST           1 ('a')
      6 LOAD_CONST           2 ('b')
      9 LOAD_CONST           3 ('c')
     12 BUILD_LIST           4
     15 RETURN_VALUE
```
### Characteristics and Limitations of Tuples:

- Tuples lack named fields and rely on integer indexing for data access.
- They are ad-hoc structures, which can lead to challenges in maintaining consistent field numbers and properties across instances.

```
# Example usage:
car1 = ("red", 3812.4, True)
car2 = ("blue", 40231.0, False)

# Tuple instances have a clear representation:
print(car1)  # ('red', 3812.4, True)
print(car2)  # ('blue', 40231.0, False)

# Accessing data:
print(car2[1])  # 40231.0

# Tuples are immutable:
try:
    car2[1] = 12  # Raises TypeError
except TypeError as e:
    print(e)

# No protection against missing or extra fields or incorrect order:
car3 = (3431.5, "green", True, "silver")
```
### Write a Custom Class: More Work, More Control

Classes in Python allow you to define reusable blueprints for data objects, ensuring consistent fields and enabling the addition of business logic and methods.

Using regular Python classes as record data types requires manual effort for features like initializing new fields in the `__init__` constructor and defining a meaningful `__repr__` method.

Fields stored on classes are mutable, allowing for dynamic field addition. You can enforce access control and create read-only fields using the `@property` decorator.

```
# Example of a custom class for a Car object:
class Car:
    def __init__(self, color, mileage, automatic):
        self.color = color
        self.mileage = mileage
        self.automatic = automatic

# Example usage:
car1 = Car("red", 3812.4, True)
car2 = Car("blue", 40231.0, False)

# Accessing fields:
print(car2.mileage)  # 40231.0

# Classes allow mutation of fields:
car2.mileage = 12
car2.windshield = "broken"  # Adding new fields is possible

# Default string representation isn't informative:
print(car1)  # <Car object at 0x1081e69e8>
```
### dataclasses.dataclass: Python 3.7+ Data Classes

Data classes in Python 3.7 and above provide a streamlined way to define classes for storing data, reducing boilerplate code.

By using `@dataclass` decorator, you can define data classes with instance variables, benefiting from:
- Automatic generation of `__init__()` and `__repr__()` methods.
- Concise syntax with type annotations for self-documentation (not enforced without additional tools like mypy).

```
from dataclasses import dataclass

# Example of a data class for a Car object:
@dataclass
class Car:
    color: str
    mileage: float
    automatic: bool

# Example usage:
car1 = Car("red", 3812.4, True)

# Instances have a clear and informative repr:
print(car1)  # Car(color='red', mileage=3812.4, automatic=True)

# Accessing fields:
print(car1.mileage)  # 3812.4

# Fields are mutable:
car1.mileage = 12
car1.windshield = "broken"  # Adding new fields is possible

# Type annotations are hints and not enforced:
print(Car("red", "NOT_A_FLOAT", 99))  # Car(color='red', mileage='NOT_A_FLOAT', automatic=99)
```
### `collections.namedtuple`: Convenient Data Objects

The `namedtuple` class in Python (available from version 2.6 onwards) extends the functionality of the built-in tuple data type by providing named fields for accessing elements.

Namedtuple objects:
- **Immutable**: Once created, fields cannot be modified.
- **Named**: Elements are accessed using named attributes, improving code readability.
- **Memory Efficient**: Comparable to regular tuples and better than custom classes.

```
from collections import namedtuple

# Example of defining a namedtuple for a Car object:
Car = namedtuple("Car", ["color", "mileage", "automatic"])

# Creating instances:
car1 = Car("red", 3812.4, True)

# Instances have a clear and informative repr:
print(car1)  # Car(color='red', mileage=3812.4, automatic=True)

# Accessing fields:
print(car1.mileage)  # 3812.4

# Namedtuples are immutable:
try:
    car1.mileage = 12  # Raises AttributeError
except AttributeError as e:
    print(e)

# Adding new fields is not allowed:
try:
    car1.windshield = "broken"  # Raises AttributeError
except AttributeError as e:
    print(e)
```
### typing.NamedTuple: Improved Namedtuples

Introduced in Python 3.6, `typing.NamedTuple` provides an enhanced syntax for defining named tuples with added support for type annotations.

Features of `NamedTuple`:
- **Immutable**: Fields cannot be modified after instantiation.
- **Named Fields**: Accessed using named attributes, improving code readability.
- **Type Annotations**: Supports type hints for each field, though these are not enforced without additional type-checking tools like mypy.

```
from typing import NamedTuple

# Example of defining a NamedTuple for a Car object:
class Car(NamedTuple):
    color: str
    mileage: float
    automatic: bool

# Creating instances:
car1 = Car("red", 3812.4, True)

# Instances have a clear and informative repr:
print(car1)  # Car(color='red', mileage=3812.4, automatic=True)

# Accessing fields:
print(car1.mileage)  # 3812.4

# NamedTuples are immutable:
try:
    car1.mileage = 12  # Raises AttributeError
except AttributeError as e:
    print(e)

# Adding new fields is not allowed:
try:
    car1.windshield = "broken"  # Raises AttributeError
except AttributeError as e:
    print(e)

# Type annotations are not enforced without a type-checking tool:
print(Car("red", "NOT_A_FLOAT", 99))  # Car(color='red', mileage='NOT_A_FLOAT', automatic=99)
```
### struct.Struct: Serialized C Structs

The `struct.Struct` class in Python facilitates the conversion between Python values and C structs serialized into bytes objects. It is commonly used for handling binary data from files or network connections.

**Key Features of `struct.Struct`:**
- **Format String**: Uses a format string syntax to define the layout of C data types (e.g., `int`, `float`, `char`) and their variants (`unsigned`, etc.).
- **Serialization**: Packs Python values into bytes objects according to the specified format string.
- **Deserialization**: Unpacks bytes objects back into Python values based on the format string.

```
from struct import Struct

# Example of defining a Struct and packing/unpacking data:
MyStruct = Struct("i?f")
data = MyStruct.pack(23, False, 42.0)

# Packed data is returned as bytes:
print(data)  # b'\x17\x00\x00\x00\x00\x00\x00\x00\x00\x00(B'

# Unpacking bytes data back into Python values:
print(MyStruct.unpack(data))  # (23, False, 42.0)
```
### types.SimpleNamespace: Fancy Attribute Access

`types.SimpleNamespace` in Python provides a simple way to create objects that act like namespaces with attribute access, similar to dictionaries but with the convenience of attribute-style access syntax.

**Key Features of `types.SimpleNamespace`:**
- **Attribute Access**: Instances of `SimpleNamespace` support attribute access (`obj.key`) instead of the traditional dictionary syntax (`obj['key']`).
- **Default `__repr__`**: Objects have a meaningful default string representation (`__repr__`) that displays all attributes.
- **Mutability**: Attributes can be freely added, modified, and deleted after the object is created.

```
from types import SimpleNamespace

# Example usage of SimpleNamespace:
car1 = SimpleNamespace(color="red", mileage=3812.4, automatic=True)

# Default representation:
print(car1)  # namespace(automatic=True, color='red', mileage=3812.4)

# Attribute access and mutation:
car1.mileage = 12
car1.windshield = "broken"
del car1.automatic

print(car1)  # namespace(color='red', mileage=12, windshield='broken')
```

## Sets and Multisets

### Set: Mutable

Python's `set` is mutable, supporting dynamic insertion and deletion of elements. It's efficient for membership tests and set operations like intersection and union.

```
vowels = {"a", "e", "i", "o", "u"}
"e" in vowels  # True

letters = set("alice")
letters.intersection(vowels)  # {'a', 'e', 'i'}

vowels.add("x")
len(vowels)  # 6
```
### Frozenset: Immutable

`frozenset` provides an immutable set in Python, ideal for hashable objects and as dictionary keys.

```
vowels = frozenset({"a", "e", "i", "o", "u"})
d = {frozenset({1, 2, 3}): "hello"}
```
### Counter: Multiset

`Counter` from `collections` implements a multiset for counting elements with multiple occurrences.

```
from collections import Counter

inventory = Counter()

loot = {"sword": 1, "bread": 3}
inventory.update(loot)
print(inventory)  # Counter({'bread': 3, 'sword': 1})

more_loot = {"sword": 1, "apple": 1}
inventory.update(more_loot)
print(inventory)  # Counter({'bread': 3, 'sword': 2, 'apple': 1})
```
### Summary: Sets and Multisets

Sets (`set`), immutable sets (`frozenset`), and multisets (`Counter`) provide versatile options for managing collections in Python:

- **Set**: Mutable collection with efficient membership tests and set operations.
- **Frozenset**: Immutable version of set, ideal for hashable objects and as dictionary keys.
- **Counter**: Multiset for counting elements with multiple occurrences.



## Stacks (LIFOs)

A stack is a collection of objects that follows Last-In/First-Out (LIFO) semantics for inserts and deletes. It's commonly used in algorithms and memory management.

### list: Simple Built-in Stacks

Python's built-in list can serve as a stack with push and pop operations, achieving amortized O(1) time complexity.

```
s = []
s.append("eat")
s.append("sleep")
s.append("code")

s.pop()  # 'code'
s.pop()  # 'sleep'
s.pop()  # 'eat'
```
### collections.deque: Fast and Robust Stacks

Python's `deque` implements a double-ended queue with efficient O(1) time complexity for append and pop operations. It's built on a doubly-linked list, ensuring consistent performance.

```
from collections import deque

s = deque()
s.append("eat")
s.append("sleep")
s.append("code")

s.pop()  # 'code'
s.pop()  # 'sleep'
s.pop()  # 'eat'
```
## queue.LifoQueue: Locking Semantics

`LifoQueue` from the `queue` module supports synchronization for multiple producers and consumers, useful in parallel computing scenarios.

```
from queue import LifoQueue

s = LifoQueue()
s.put("eat")
s.put("sleep")
s.put("code")

s.get()  # 'code'
s.get()  # 'sleep'
s.get()  # 'eat'
```
### Summary: Stacks

Python offers multiple stack implementations with different performance and usage characteristics:

- **list**: Suitable for simple stacks, supports amortized O(1) time complexity for push and pop operations.
- **deque**: Optimized for fast appends and pops from both ends, maintaining O(1) performance.
- **LifoQueue**: Provides locking and synchronization for parallel computing, ensuring safe operations in multi-threaded environments.



## Queues (FIFOs)

A queue is a collection of objects that supports fast FIFO semantics for inserts (enqueue) and deletes (dequeue). Unlike lists or arrays, queues typically don’t allow for random access to the objects they contain.

### Real-world Analogy:

Imagine a line at a conference where attendees queue up to receive their badges. New arrivals join at the back (enqueue), and attendees at the front receive their badges and leave (dequeue).

Another analogy is a pipe where you add items at one end and remove them from the other, mimicking FIFO behavior.

### Performance and Characteristics:

Queues differ from stacks in that items are removed in the order they were added (FIFO). Performance-wise, a queue should offer O(1) time complexity for both enqueue and dequeue operations.

#### Applications:

Queues are essential in algorithms like BFS and for solving scheduling and parallel programming problems. Priority queues are specialized variants where elements are retrieved based on their priority rather than insertion order.

### Using Lists for Queues:

Using a regular list as a queue is possible but not ideal due to performance issues. Lists are slow for queue operations because inserting or deleting an element at the beginning requires shifting all other elements, which takes O(n) time.

```
q = []
q.append("eat")
q.append("sleep")
q.append("code")

print(q)  # ['eat', 'sleep', 'code']

print(q.pop(0))  # 'eat'
```
### collections.deque: Fast and Robust Queues

The `deque` class in Python implements a double-ended queue, supporting O(1) time complexity for adding and removing elements from either end. This makes it efficient for both queues and stacks.

Python’s `deque` objects use doubly-linked lists, ensuring consistent performance for insertion and deletion operations. However, accessing elements in the middle of the deque is slow (O(n)).

```
from collections import deque

# Create a deque
q = deque()

# Adding elements
q.append("eat")
q.append("sleep")
q.append("code")

# Display the deque
print(q)  # Output: deque(['eat', 'sleep', 'code'])

# Removing elements
print(q.popleft())  # Output: 'eat'
print(q.popleft())  # Output: 'sleep'
print(q.popleft())  # Output: 'code'

# This will raise an IndexError because the deque is empty
print(q.popleft())
```
### queue.Queue: Locking Semantics for Parallel Computing

The `queue.Queue` implementation in Python's standard library provides synchronized operations with locking semantics. It supports multiple producers and consumers, making it suitable for parallel computing scenarios.

Python's `queue` module offers various classes for multi-producer, multi-consumer queues tailored for parallel computing tasks. However, the locking mechanisms can introduce unnecessary overhead depending on your specific use case. For general-purpose queue operations without needing explicit locking, `collections.deque` is often a more efficient choice.

```
from queue import Queue

# Create a synchronized Queue
q = Queue()

# Adding elements
q.put("eat")
q.put("sleep")
q.put("code")

# Display the Queue object
print(q)  # Output: <queue.Queue object at 0x1070f5b38>

# Removing elements
print(q.get())  # Output: 'eat'
print(q.get())  # Output: 'sleep'
print(q.get())  # Output: 'code'

# Using get_nowait() to avoid blocking
try:
    print(q.get_nowait())  # Raises queue.Empty exception if empty
except queue.Empty:
    print("Queue is empty")
```

### multiprocessing.Queue: Shared Job Queues

The `multiprocessing.Queue` in Python provides a shared job queue implementation designed for parallel processing using multiple concurrent workers. This is particularly useful in CPython where the global interpreter lock (GIL) limits certain forms of parallel execution within a single interpreter process.

This specialized queue allows items to be queued and processed across multiple processes, facilitating parallelization and overcoming the limitations imposed by the GIL. It supports storing and transferring any pickleable object across process boundaries.

```
from multiprocessing import Queue

# Create a multiprocessing Queue
q = Queue()

# Adding elements
q.put("eat")
q.put("sleep")
q.put("code")

# Display the Queue object
print(q)  # Output: <multiprocessing.queues.Queue object at 0x1081c12b0>

# Removing elements
print(q.get())  # Output: 'eat'
print(q.get())  # Output: 'sleep'
print(q.get())  # Output: 'code'

# Using get() blocks indefinitely if queue is empty
print(q.get())  # Blocks indefinitely if queue is empty
```

### Summary: Queues

Python provides versatile queue implementations catering to different performance needs and concurrency requirements:

- **list**: Basic but slow for queue operations.
- **deque**: Efficient for both ends operations, suitable for general-purpose queues.
- **Queue**: Synchronized queue for multi-threaded applications.
- **multiprocessing.Queue**: Shared queues for parallel processing in multi-process environments.



## Priority Queues:

A priority queue is a data structure that manages records with totally-ordered keys, allowing quick access to the record with the highest or lowest key.

### list: Manually Sorted Queues

Using a sorted list for a priority queue requires manual sorting after each insertion, making it suitable only for scenarios with few insertions.

```
q = []
q.append((2, "code"))
q.append((1, "eat"))
q.append((3, "sleep"))
q.sort(reverse=True)
while q:
    next_item = q.pop()
    print(next_item)
```
### heapq: List-Based Binary Heaps

`heapq` provides a binary heap implementation backed by a list, supporting O(log n) insertion and extraction of the smallest element.

```
import heapq
q = []
heapq.heappush(q, (2, "code"))
heapq.heappush(q, (1, "eat"))
heapq.heappush(q, (3, "sleep"))
while q:
    next_item = heapq.heappop(q)
    print(next_item)
```
### queue.PriorityQueue: Beautiful Priority Queues

`PriorityQueue` provides a synchronized priority queue using `heapq` internally, suitable for concurrent producers and consumers.

```
from queue import PriorityQueue

q = PriorityQueue()
q.put((2, "code"))
q.put((1, "eat"))
q.put((3, "sleep"))

while not q.empty():
    next_item = q.get()
    print(next_item)
```
### Priority Queues in Python: Summary

Python offers several priority queue implementations:

- **queue.PriorityQueue:** Provides a clear object-oriented interface with synchronization.
  
- **heapq:** Direct module for binary heap operations, suitable for scenarios where direct control over synchronization is preferred.
