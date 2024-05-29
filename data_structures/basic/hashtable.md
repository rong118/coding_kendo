# Hashtable

A hashtable (also known as a hash table, hashmap, or dictionary) is a data structure that stores key-value pairs in an unordered manner. The main idea behind a hash table is to map keys to values using a hash function.
It can be implemented as a **hash map** or a **hash set**.

## Characteristics
1. Key-Value Pairs: A hashtable is made up of key-value pairs, where each pair consists of a unique key and an associated value.
2. Hash Function: When you add a new key-value pair to the hashtable, the hash function takes the key as input and generates a hash code, which represents the position of the corresponding value in the array.

## Hash Collision
A hash collision occurs when two or more different keys hash to the same index in a hash table. This happens because the hash function is not perfect and cannot always guarantee unique indices for each key.

### Hash Table Techniques to Overcome Hash Collisions
- **Chaining**: Each bucket in the hash table's array holds a linked list (or another data structure) of key-value pairs that hash to the same index. When a collision occurs, the key-value pair is added to the linked list associated with the corresponding index. This way, multiple key-value pairs can coexist at the same index without overwriting each other.
- **Open Addressing**: when a collision occurs, the hash table searches for an alternative location (probe sequence) to store the key-value pair. This can involve techniques such as linear probing (checking the next available slot), quadratic probing (checking slots with quadratic increments), or double hashing (using a secondary hash function to calculate the next index).

## Runtime Complexity
There are some common operations and their average-case time complexities for a hash table:
- Lookup: O(1) - This is the most common operation, where you look up a value by its key.
- Insert: O(1) - When inserting a new key-value pair, the hash function generates the index, and the insertion takes constant time on average.
- Delete: O(1) - Deleting a key-value pair also takes constant time on average.
- Iteration (iterate over all entries): O(n) - When you need to iterate over all key-value pairs, the hash table must traverse the entire array, which takes linear time proportional to the number of elements n.
- Collision resolution: O(1), O(k), or O(log n) - Hash tables use various techniques (e.g., chaining, open addressing) to handle collisions (when two keys hash to the same index). The specific collision resolution method affects the runtime complexity.

## Leetcode Questions
- [1. Two Sum](../../leetcode_questions/1_two_sum.md)
- [3. Longest Substring Without Repeating Characters]()
- [49. Group Anagrams]()
- [217. Contains Duplicate](../../leetcode_questions/217_contain_duplicate.md)
- [242. Valid Anagram]()
- [347. Top K Frequent Elements]()
- [350. Intersection of Two Arrays II]()
