# Segement Tree (ZKW Tree)

A Segment Tree is a data structure that allows for efficient querying and updating of a range of elements in an array. It's particularly useful when you need to perform operations like:

- **Range Sum**
  
  Find the sum of all elements in a specific range.
  
- **Range Minimum/Maximum**
  
  Find the minimum or maximum value in a specific range.
  
- **Range Update**
  
  Update all elements in a specific range.

## Implementation
```python
class Node:
    def __init__(self, sum=0, left=None, right=None):
        self.sum = sum  # Sum of elements in this node's range
        self.left = left  # Left child
        self.right = right  # Right child

# Function to build the segment tree
def build_segment_tree(arr, start, end):
    if start == end:
        # Leaf node: just store the value
        return Node(sum=arr[start])

    mid = (start + end) // 2

    # Internal node: build left and right subtrees
    left_child = build_segment_tree(arr, start, mid)
    right_child = build_segment_tree(arr, mid + 1, end)

    # Calculate the sum for this node's range
    node = Node(sum=left_child.sum + right_child.sum, left=left_child, right=right_child)

    return node

# Function to query the segment tree: find the sum of a range [L, R]
def query_segment_tree(root, start, end, L, R):
    if R < start or L > end:
        # Out-of-range query: return 0
        return 0

    if start >= L and end <= R:
        # Exact match: return the sum for this node's range
        return root.sum

    mid = (start + end) // 2

    # Recursively query left and right subtrees
    left_sum = query_segment_tree(root.left, start, mid, L, min(R, mid))
    right_sum = query_segment_tree(root.right, mid + 1, end, max(L, mid + 1), R)

    return left_sum + right_sum

# Example usage
if __name__ == "__main__":
    arr = [1, 3, 5, 7, 9, 11]
    N = len(arr)

    # Build the segment tree
    root = build_segment_tree(arr, 0, N - 1)

    # Query examples:
    print("Sum of [2, 4]:", query_segment_tree(root, 0, N - 1, 2, 4))
    print("Sum of [5, 5]:", query_segment_tree(root, 0, N - 1, 5, 5))
```

## Runtime Complexity

The runtime complexity of a Segment Tree depends on the type of query being performed:

- **Range Sum Query**

  The time complexity for a range sum query is **O(log N)**, where N is the size of the input array.

  This is because we need to traverse the segment tree recursively until we reach the leaf nodes, which takes logarithmic time.

- **Range Minimum/Maximum Query**

  The time complexity for a range minimum/maximum query is also **O(log N)**.

  Update Operation: The time complexity for an update operation is O(k log N), where k is the number of elements updated.

- **Construction Time**

  The construction time for building the segment tree is **O(N)**, where N is the size of the input array. 

  This is because we need to recursively construct the segment tree, which takes linear time.
