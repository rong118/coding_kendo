## Trie (Prefix Tree)

A Trie (also known as a prefix tree) is a type of search tree used to store a dynamic set or associative array where the keys are usually strings.

## key Characteristic
- Each node in the trie represents a string.
- The root node represents the empty string.
- Each edge from a node to its child represents appending one character to the string represented by that node.
- A node is said to be complete if all possible characters are present at each position in the string represented by that node.

## Implementation
### C++ Implementation
```c++
#include <iostream>
#include <string>

using namespace std;

class Trie {
public:
    struct Node {
        bool isEndOfWord;
        map<char, Node*> children;
    };

    Trie() : root(new Node()) {}

    void insert(const string& word) {
        Node* current = root;
        for (char c : word) {
            if (!current->children.count(c)) {
                current->children[c] = new Node();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(const string& word) {
        Node* current = root;
        for (char c : word) {
            if (!current->children.count(c)) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    vector<string> prefix_search(const string& prefix) {
        Node* current = &root;
        for (char c : prefix) {
            if (!current->children.count(c)) {
                return {}; // prefix not found
            }
            current = current->children[c];
        }
        vector<string> results;
        _Search(current, prefix, results);
        return results;
    }

private:
    Node* root;

    void _Search(Node* node, const string& prefix, vector<string>& results) {
        if (node->isEndOfWord) {
            results.push_back(prefix);
        }
        for (const auto& pair : node->children) {
            _Search(pair.second, prefix + pair.first, results);
        }
    }
};

int main() {
    Trie trie;

    trie.insert("apple");
    trie.insert("banana");
    trie.insert("app");

    cout << "Is 'apple' in the trie? " << (trie.search("apple") ? "Yes" : "No") << endl;
    cout << "Is 'bananas' in the trie? " << (trie.search("bananas") ? "Yes" : "No") << endl;
    cout << "Is 'apples' in the trie? " << (trie.search("apples") ? "Yes" : "No") << endl;

    vector<string> results = trie.prefix_earch("a"); // returns ["apple", "app"]
    for (const auto& result : results) {
        cout << result << endl;
    }

    return 0;
}
```

### Golang Implementation
```golang
package main

import (
    "fmt"
)

type TrieNode struct {
    IsEndOfWord bool
    Children map[rune]*TrieNode
}

func NewTrie() *TrieNode {
    return &TrieNode{nil, make(map[rune]*TrieNode))}
}

func (n *TrieNode) Insert(word string) {
    current := n
    for _, c := range word {
        if _, ok := current.Children[c]; !ok {
            current.Children[c] = NewTrie()
        }
        current = current.Children[c]
    }
    current.IsEndOfWord = true
}

func (n *TrieNode) Search(word string) bool {
    current := n
    for _, c := range word {
        if _, ok := current.Children[c]; !ok {
            return false
        }
        current = current.Children[c]
    }
    return current.IsEndOfWord
}

func main() {
    trie := NewTrie()

    trie.Insert("apple")
    trie.Insert("banana")
    trie.Insert("app")

    fmt.Println("Is 'apple' in the trie? ", trie.Search("apple"))
    fmt.Println("Is 'bananas' in the trie? ", trie.Search("bananas"))
    fmt.Println("Is 'apples' in the trie? ", trie.Search("apples"))
}
```

## Runtime Complexity
### - Insertion

**O(m)**, where m is the length of the string. This is because we need to traverse the Trie, creating new nodes as needed, and update the child pointers. Each step takes constant time, so the total time complexity is linear in the length of the string.

### - Search

**O(m)**, where m is the length of the string. This is because we need to traverse the Trie, following the child pointers until we reach the end of the string. If the string is not found, the search operation will terminate earlier.

### - Prefix matching

The time complexity for finding all strings that start with a given prefix in a Trie is **O(n)**, where n is the number of strings in the Trie that match the prefix.

This is because we need to traverse the Trie, starting from the root node and following the child pointers until we reach the end of the string. We then need to collect all the strings that match the prefix.
