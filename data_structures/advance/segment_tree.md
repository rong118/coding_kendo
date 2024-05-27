# Segement Tree (ZKW Tree)

A Segment Tree is a data structure that allows for efficient querying and updating of a range of elements in an array. It's particularly useful when you need to perform operations like:

- **Range Sum**
  
  Find the sum of all elements in a specific range.
  
- **Range Minimum/Maximum**
  
  Find the minimum or maximum value in a specific range.
  
- **Range Update**
  
  Update all elements in a specific range.

## Implementation
```c++
#include <iostream>
#include <vector>

using namespace std;

// Node structure for the segment tree
struct Node {
    int sum;  // Sum of elements in this node's range
    Node* left;
    Node* right;
};

// Function to build the segment tree
Node* buildSegmentTree(vector<int>& arr, int start, int end) {
    if (start == end) {
        // Leaf node: just store the value
        Node* node = new Node();
        node->sum = arr[start];
        return node;
    }

    int mid = (start + end) / 2;

    // Internal node: build left and right subtrees
    Node* node = new Node();
    node->left = buildSegmentTree(arr, start, mid);
    node->right = buildSegmentTree(arr, mid + 1, end);

    // Calculate the sum for this node's range
    node->sum = node->left->sum + node->right->sum;

    return node;
}

// Function to query the segment tree: find the sum of a range [L, R]
int querySegmentTree(Node* root, int start, int end, int L, int R) {
    if (R < start || L > end) {
        // Out-of-range query: return 0
        return 0;
    }

    if (start >= L && end <= R) {
        // Exact match: return the sum for this node's range
        return root->sum;
    }

    int mid = (start + end) / 2;

    // Recursively query left and right subtrees
    int leftSum = querySegmentTree(root->left, start, mid, L, min(R, mid));
    int rightSum = querySegmentTree(root->right, mid + 1, end, max(L, mid), R);

    return leftSum + rightSum;
}

// Example usage:
int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11};
    int N = arr.size();

    // Build the segment tree
    Node* root = buildSegmentTree(arr, 0, N - 1);

    // Query examples:
    cout << "Sum of [2, 4]: " << querySegmentTree(root, 0, N - 1, 2, 4) << endl;
    cout << "Sum of [5, 7]: " << querySegmentTree(root, 0, N - 1, 5, 7) << endl;

    return 0;
}
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
