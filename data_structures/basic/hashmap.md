# Hash Map

In computing, hash map is a data structure that implements an associative array or dictionary. It is an abstract data type that maps keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found.

A hash map typically uses a single array or linked list to store values.

## Implementation
### python using dictionary
```python
# Creating a hashmap (dictionary)
hashmap = {}

# Inserting key-value pairs
hashmap["apple"] = 5
hashmap["banana"] = 3
hashmap["orange"] = 8
hashmap["grape"] = 2

# Accessing values using keys
print("Value for 'apple':", hashmap["apple"])  # Output: 5
print("Value for 'banana':", hashmap["banana"])  # Output: 3

# Checking if a key exists
if "orange" in hashmap:
    print("'orange' is present in the hashmap")

# Modifying values
hashmap["banana"] = 10
print("Updated value for 'banana':", hashmap["banana"])  # Output: 10

# Deleting a key-value pair
del hashmap["grape"]
print("Hashmap after deleting 'grape':", hashmap)

# Iterating through all key-value pairs
print("\nIterating through the hashmap:")
for key, value in hashmap.items():
    print(f"{key}: {value}")

# Using get() to access values (without throwing an error if the key doesn't exist)
print("\nValue for 'pear' (using get):", hashmap.get("pear", "Not Found"))  # Output: Not Found

# Checking the size of the hashmap
print("\nSize of the hashmap:", len(hashmap))  # Output: 3

# Clearing the entire hashmap
hashmap.clear()
print("Hashmap after clearing:", hashmap)  # Output: {}

```

## O(1) search and insert 
- Insertion (put(key, value)): O(1) <br>
In a well-implemented HashMap, insertion is typically done in constant time, as it only requires calculating the hash code for the key and updating the bucket array.
- Lookup (get(key)): O(1) <br>
Looking up a value by its key is also typically done in constant time, as it only requires hashing the key and finding the corresponding bucket.
- Deletion (remove(key)): O(1) <br>
Deleting an entry from the HashMap is often done in constant time, as it simply involves updating the bucket array and removing any necessary links.
- Contains Key (containsKey(key)): O(1) <br>
Checking if a key exists in the HashMap is typically done in constant time, as it only requires hashing the key and finding the corresponding bucket.