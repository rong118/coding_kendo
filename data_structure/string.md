# String

String is traditionally a sequence of characters, it may allow its elements to be mutated and the length changed, or it may be fixed (after creation). A string is generally considered as a data type and is often implemented as an array data structure of bytes (or words) that stores a sequence of elements, typically characters, using some character encoding. 

String may also denote more general arrays or other sequence (or list) data types and structures.

## Implementation
```c++
// c++ Implementation
#include <string>

// Initial string
std::string a;
a = "123";
std::string b ("abc");

// Check Length
int len = a.length();

if(a.empty()){
    // Do something in here
}

// Access elements in string
char c = a[0];
char d = a.at(0);

// Operate string (
// C++ std::string is mutable and assignment/copies the string data.
a += b;             // a = "123abc"
a.append(b);        // a = "123abcabc"
a.insert(0, "abc"); // a = "abc123abcabc"
a.erase(0, 3);      // a = "123abcabc"

// Search string
std::size_t found = a.find("abc");
if (found != std::string::npos){
    // Do somthing in here
}

// convert string to lowcase
std::tolower(s[l++]);

// check string if is alphanumeric
isalnum(s[l]);
```

## Leetcode questions
- [3. Longest Substring Without Repeating Characters](../leetcode_questions/3_longest_substring_without_repeating_characters.md)
- [125. Valid Palindrome](../leetcode_questions/125_valid_palindrome.md)
- [242. Valid Anagram](../leetcode_questions/242_valid_anagram.md)
- [409. Longest Palindrome](../leetcode_questions/409_longest_palindrome.md)