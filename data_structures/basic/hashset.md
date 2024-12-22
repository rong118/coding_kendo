# HashSet

A HashSet is a fundamental data structure that represents an unordered collection of unique elements, typically stored in a hash table. It allows for efficient insertion, deletion, and lookup operations.

## Characteristics
- Each element is associated with a unique key or identifier.
- The set does not allow duplicate elements; if you try to add a duplicate, it will be ignored.
- Lookup, insertion, and deletion operations are typically O(1) in the average case.

## Implementation
```python
# Creating a hashset (set)
hashset = set()

# Adding elements to the hashset
hashset.add(10)
hashset.add(20)
hashset.add(30)
hashset.add(40)

# Adding duplicate elements (sets do not allow duplicates)
hashset.add(20)  # This will not be added since 20 is already in the set

# Checking if an element is in the hashset
print("Is 20 in the hashset?", 20 in hashset)  # Output: True
print("Is 50 in the hashset?", 50 in hashset)  # Output: False

# Removing an element
hashset.remove(30)  # Removes 30 from the set
print("Hashset after removing 30:", hashset)  # Output: {40, 10, 20}

# Using discard to remove an element (doesn't raise an error if element is not found)
hashset.discard(50)  # No error, even though 50 is not in the set
print("Hashset after discarding 50:", hashset)  # Output: {40, 10, 20}

# Iterating through the hashset
print("\nIterating through the hashset:")
for element in hashset:
    print(element)

# Getting the size of the hashset
print("\nSize of the hashset:", len(hashset))  # Output: 3

# Clearing the hashset
hashset.clear()
print("Hashset after clearing:", hashset)  # Output: set()
```