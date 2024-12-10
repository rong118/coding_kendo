# Linked List

A linked list is is a data structure that consists of a sequence of nodes, each pointing to the next node in the list. This allows for efficient insertion and deletion of elements at any position in the list.

How it works:
- Each node typically contains two items: a value (or "data") and a reference (i.e., a "link") to the next node in the list.
- The last node in the list has a null or undefined reference, indicating the end of the list.
- To insert a new element at a specific position, you simply need to create a new node and update the links between nodes accordingly.

## Implementation
### C++ Implementation
```c++
#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;
    Node(int val) : data(val), next(NULL) {}
};

class LinkedList {
public:
    Node* head;

    LinkedList() : head(NULL) {}

    void append(int val) {
        Node* newNode = new Node(val);
        if (head == NULL) {
            head = newNode;
        } else {
            Node* current = head;
            while (current->next != NULL) {
                current = current->next;
            }
            current->next = newNode;
        }
    }

    void printList() {
        Node* current = head;
        while (current != NULL) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }
};

int main() {
    LinkedList ll;
    ll.append(1);
    ll.append(2);
    ll.append(3);

    ll.printList(); // Output: 1 2 3

    return 0;
}
```

### Go Implementation
```go
package main

type Node struct {
    value int
    next  *Node
}

func NewNode(value int) *Node {
    return &Node{value, nil}
}

func (n *Node) String() string {
    return fmt.Sprintf("%d", n.value)
}

type LinkedList struct {
    head *Node
}

func NewLinkedList() *LinkedList {
    return &LinkedList{nil}
}

func (l *LinkedList) Append(value int) {
    newNode := NewNode(value)
    if l.head == nil {
        l.head = newNode
    } else {
        current := l.head
        for current.next != nil {
            current = current.next
        }
        current.next = newNode
    }
}

func (l *LinkedList) String() string {
    var sb []byte
    node := l.head
    for node != nil {
        sb = append(sb, fmt.Sprintf("%d ", node.value))
        node = node.next
    }
    return string(sb[:len(sb)-1])
}

func main() {
    ll := NewLinkedList()
    ll.Append(1)
    ll.Append(2)
    ll.Append(3)

    fmt.Println(ll.String()) // Output: 1 2 3
}
```

### Python Implementation
```python
class Node:
    def __init__(self, data):
        self.data = data  # Data stored in the node
        self.next = None  # Pointer to the next node

class LinkedList:
    def __init__(self):
        self.head = None  # The head of the linked list

    # Add a new node at the end
    def append(self, data):
        new_node = Node(data)
        if not self.head:  # If the list is empty
            self.head = new_node
            return
        current = self.head
        while current.next:  # Traverse to the last node
            current = current.next
        current.next = new_node

    # Display the list
    def display(self):
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")

    # Search for an element
    def search(self, key):
        current = self.head
        while current:
            if current.data == key:
                return True
            current = current.next
        return False

    # Delete a node by value
    def delete(self, key):
        current = self.head

        # If the head node is to be deleted
        if current and current.data == key:
            self.head = current.next
            current = None
            return

        # Search for the node to delete
        prev = None
        while current and current.data != key:
            prev = current
            current = current.next

        # If the node was not found
        if not current:
            return

        # Unlink the node
        prev.next = current.next
        current = None
    
# Create a linked list
ll = LinkedList()

# Append elements
ll.append(10)
ll.append(20)
ll.append(30)

# Display the linked list
ll.display()  # Output: 10 -> 20 -> 30 -> None

# Search for an element
print(ll.search(20))  # Output: True
print(ll.search(40))  # Output: False

# Delete an element
ll.delete(20)
ll.display()  # Output: 10 -> 30 -> None

# Add more elements
ll.append(40)
ll.append(50)
ll.display()  # Output: 10 -> 30 -> 40 -> 50 -> None
```

## Runtime Complexity

### Adding a node:
- Append: If you're appending a new node to the end of the list, the runtime complexity is O(1), because you simply need to update the next reference of the last node in the list.
- Insert at specific position: If you want to insert a new node at a specific position within the list (e.g., between two existing nodes), the runtime complexity is O(n), where n is the distance from the head of the list to the insertion point. This is because you need to traverse the list to find the correct position, which takes linear time.
### Deleting a node:
- Delete at specific position: If you want to delete a node at a specific position within the list (e.g., between two existing nodes), the runtime complexity is O(n), where n is the distance from the head of the list to the deletion point. This is because you need to traverse the list to find the correct node, which takes linear time.
- Delete last node: If you're deleting the last node in the list (i.e., the tail of the list), the runtime complexity is O(1), because you simply need to update the next reference of the second-to-last node.
### Other operations:
- Traversing the entire list: The runtime complexity for traversing the entire list is O(n), where n is the number of nodes in the list.
- Searching for a specific node: The runtime complexity for searching for a specific node within the list is O(n), where n is the number of nodes in the list.

## Leetcode question
### 反转
- [206 Reverse Linked List](../../leetcode_questions/206_reverse_linked_list.md)
- [92 Reverse Linked List II](../../leetcode_questions/92_reverse_linked_list_II.md)
- [25 Reverse Nodes in K-Group](../../leetcode_questions/25_reverse_nodes_in_k_group.md)

### 合并
- [2 Add Two Numbers](../../leetcode_questions/2_add_two_numbers.md)
- [445 Add Two Numbers II](../../leetcode_questions/445_add_two_numbers_II.md)
- [21 Merge Two Sorted Lists](../../leetcode_questions/21_merge_two_sorted_lists.md)
- [23 Merge k sorted Lists](../../leetcode_questions/23_merge_k_sorted_lists.md)

### 找环
- [141 Linked List Cycle](../../leetcode_questions/141_linked_list_cycle.md)
- [142 Linked List Cycle II](../../leetcode_questions/142_linked_list_cycle.md)
- [287 Find the Duplicate Number](../../leetcode_questions/287_find_the_duplicate_number.md)
- [160 Intersection of Two Linked Lists](../../leetcode_questions/160_intersection_of_two_linked_lists.md)

### 删除
- [203 Remove Linked List Elements](../../leetcode_questions/203_remove_linked_list_elements.md)
- [83 Remove Duplicates from Sorted List](../../leetcode_questions/83_remove_duplicates_from_sorted_list.md)
- [82 Remove Duplicates from Sorted List II](../../leetcode_questions/82_remove_duplicates_from_sorted_list_II.md)
- [19 Remove Nth Node From End of List](../../leetcode_questions/19_remove_Nth_node_from_end_of_list.md)
- [1171 Remove Zero Sum Consecutive Nodes from Linked List](../../leetcode_questions/1171_remove_zero_sum_consecutive_nodes_from_linkedlist.md)

### 复制
- [234 Palindrome Linked List](../../leetcode_questions/234_palindrome_linked_list.md)
- [138 Copy List with Random Pointer](../../leetcode_questions/138_copy_list_with_random_pointer.md)

### 结构转换
- [426 Convert Binary Search Tree to Sorted Doubly Linked List](../../leetcode_questions/426_convert_binary_search_tree_to_sorted_doubly_linked_list.md)
