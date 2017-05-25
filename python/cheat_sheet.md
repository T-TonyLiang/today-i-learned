# Python Cheat Sheet
Quick reference for python syntax, data structures uses and tricks.

# Table of Contents
  1. [Data Structures](#1-data-structures)
  
# 1. Data Structures

## [1-Dimensional List](https://docs.python.org/3/tutorial/datastructures.html)

### Initialization

```python
list = [] # empty list
list = [1, 2] # list with 2 int elements
list = [0] * 100 # a list of size 100, all zeroes
list = [x for x in range(9)] # using list comprehension
```
  
### Usage as a Stack
  - `list.append(value)` adds to end of list
  - `list.pop()` removes and returns value at the end of list
  - `list[-1]` returns value at end of list (without removing)
  
### Usage as a Queue
  - `list.append(value)` adds to the end of list
  - `list.pop(0)` removes and returns value at the beginning of the list
  - `list[index]` gets the value at the index

### Notes
  - A list can have elements of multiple types
  - Lists are passed by **reference** in python, ie. they are pointers to other values
    - to pass by value use:
    ```
    lst = []
    lst[:]
    ```
  
