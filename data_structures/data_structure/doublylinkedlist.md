# Doubly Linked List

In computer science, a **doubly linked list** is a linked data structure that
consists of a set of sequentially linked records called nodes. Each node contains
two fields, called links, that are references to the previous and to the next
node in the sequence of nodes.

<img src="../assets/double_linked_list.png" width="300" />

## Implementation
```c++
 // c++ Implementation
#include <iostream>
using namespace std;

struct {
    int val;
    Node* prev;
    Node* next;
} Node;

int main(){
    Node* head = new Node(0);
    Node* tail = head;

    for(int i = 1; i < 5; i++){
      Node* node = new Node(i);
      tail->next = node;
      node->prev = tail;
      tail = node;
    }

    // Loop from begin of list
    Node* ptr = head;

    while(ptr != NULL){
      cout<<ptr->val<<endl;
      ptr = ptr->next;
    }

    // Loop from end of list
    Node* ptr = tail;
    while(ptr != NULL){
      cout<<ptr->val<<endl;
      ptr = ptr->prev;
    }

    return 0;
}
```

```go
// Go Implementation
package main

import "fmt"

// Node represents a node of linked list
func main(){
    type ListNode struct {
      Val int
      Next *ListNode
      Prev *ListNode
    }

    head := &ListNode{0, nil, nil}
    tail := head;

    // Looping linkedlist
    for i := 1; i < 5; i++ {
        node := &ListNode{i, nil, nil}
        tail.Next = node
        node.Prev = tail;
        tail = node
    }
	
  
	fmt.Println("Loop from begining of the list")
	ptr := head
	for ptr != nil {
		fmt.Println(ptr.Val)
		ptr = ptr.Next
	}

  fmt.Println("Loop from list end")
	ptr = tail
	for ptr != nil {
		fmt.Println(ptr.Val)
		ptr = ptr.Prev
	}
}
```

