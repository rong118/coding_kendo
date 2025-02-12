# Tree Map

TreeMap: A TreeMap is a fundamental data structure that represents a sorted map, where the keys are stored in a tree-like structure. It allows for efficient insertion, deletion, and lookup operations.
In a TreeMap:

## Characteristics
- Each key-value pair is associated with a unique key or identifier.
- The set of keys is maintained in a sorted order (typically by key).

## Runtime Complexity
Lookup, insertion, and deletion operations are typically O(log n) in the average case.

## Implementation
### Python using SortedDict
```python
from sortedcontainers import SortedDict

# Create a SortedDict
treemap = SortedDict()

# Insert elements
treemap['c'] = 3
treemap['a'] = 1
treemap['b'] = 2

# Access elements by key
print(treemap['a'])  # Output: 1

# Iterate through keys in sorted order
for key in treemap:
    print(key, treemap[key])  # Output: a 1, b 2, c 3

# Check if a key exists
print('b' in treemap)  # Output: True

# Delete a key
del treemap['a']
print(treemap)  # Output: SortedDict({'b': 2, 'c': 3})
```
