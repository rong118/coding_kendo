# Hashtable

A **hashtable** (also called hashmap, dictionary, or hash set) stores key-value pairs using a **hash function** to compute indices. It enables fast, unordered data access.

## Key Traits
- **Key-Value Pairs**: Unique keys mapped to values.
- **Hash Function**: Converts keys to array indices.

## Hash Collisions
When multiple keys hash to the same index:
- **Chaining**: Store entries in a list at that index.
- **Open Addressing**: Find alternate slots (linear, quadratic, or double hashing).

## Time Complexity (Average Case)
| Operation           | Time      |
|---------------------|-----------|
| Lookup / Insert / Delete | O(1) |
| Iteration           | O(n)     |
| Collision Resolution | O(1) ~ O(log n) |

---

# Hash Map

A **hash map** implements a key-value store using an array and a hash function.

## Python Example
```python
# Create & update
hashmap = {"apple": 5, "banana": 3}
hashmap["orange"] = 8
hashmap["banana"] = 10

# Access & delete
print(hashmap["apple"])
del hashmap["banana"]

# Check & iterate
print("orange" in hashmap)
for k, v in hashmap.items():
    print(k, v)

# Safe access, size, and clear
print(hashmap.get("pear", "Not Found"))
print(len(hashmap))
hashmap.clear()
```

# HashSet

A **HashSet** is an unordered collection of **unique** elements, implemented using a hash table. It allows efficient insertion, deletion, and membership testing.

## Key Traits
- Only unique elements are allowed (no duplicates).
- Unordered storage.
- Average-case time complexity: O(1) for add, remove, and lookup.

## Python Example
```python
# Create a hashset
hashset = set()

# Add elements
hashset.add(10)
hashset.add(20)

# Duplicate add (ignored)
hashset.add(20)

# Membership test
print(20 in hashset)  # True
print(50 in hashset)  # False

# Remove elements
hashset.remove(10)     # Raises error if not found
hashset.discard(50)    # Safe remove (no error)

# Print current elements
print("HashSet:", hashset)

# Iterate over elements
for item in hashset:
    print(item)

# Size and clear
print("Size:", len(hashset))
hashset.clear()
print("After clear:", hashset)
```

## Leetcode Questions
- [1. Two Sum](../../leetcode_questions/1_two_sum.md)
- [3. Longest Substring Without Repeating Characters]()
- [49. Group Anagrams]()
- [217. Contains Duplicate](../../leetcode_questions/217_contain_duplicate.md)
- [242. Valid Anagram]()
- [347. Top K Frequent Elements]()
- [350. Intersection of Two Arrays II]()
