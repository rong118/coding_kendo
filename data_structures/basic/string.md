# String

In computer science, a string is a sequence of characters, typically used to represent text. Strings are a fundamental data type in most programming languages and are often treated as a built-in data structure.

## Implementation
- C++ Example using std::string:
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

- Go Example using string type:
```golang
package main

import "fmt"

func main() {
    // Creating and initializing a string in Go
    str := "Hello, world!"

    // Accessing and printing the string
    fmt.Println("String in Go:", str)
}
```

- Python Example:
```python
# 1. Concatenating Strings
str1 = "Hello"
str2 = "World"
result = str1 + " " + str2
print(result)  # Output: Hello World

# 2. String Slicing
text = "PythonProgramming"
print(text[0:6])  # Output: Python
print(text[-11:]) # Output: Programming

# 3. Changing Case
text = "hello, World!"
print(text.upper())       # Output: HELLO, WORLD!
print(text.lower())       # Output: hello, world!
print(text.capitalize())  # Output: Hello, world!

# 4. Finding and Replacing
text = "I love programming in Python."
print(text.find("Python"))                     # Output: 23
print(text.replace("Python", "JavaScript"))    # Output: I love programming in JavaScript.

# 5. Splitting and Joining
text = "apple,banana,cherry"
fruits = text.split(",")
print(fruits)  # Output: ['apple', 'banana', 'cherry']

joined_text = "-".join(fruits)
print(joined_text)  # Output: apple-banana-cherry

# 6. Checking Content
text = "Python123"
print(text.isalpha())  # Output: False
print(text.isalnum())  # Output: True
print(text.isdigit())  # Output: False

# 7. Formatting Strings
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old.")
# Output: My name is Alice and I am 25 years old.

```

## Leetcode Questions
- [3. Longest Substring Without Repeating Characters](../../leetcode_questions/3_longest_substring_without_repeating_characters.md)
- [5. Longest Palindromic Substring](../../leetcode_questions/5_longest_palindromic_substring.md)
- [8. String to Integer](../../leetcode_questions/8_string_to_integer.md)
- [76. Minimum Window Substring](../../leetcode_questions/76_minimum_window_substring.md)
- [125. Valid Palindrome](../../leetcode_questions/125_valid_palindrome.md)
- [242. Valid Anagram](../../leetcode_questions/242_valid_anagram.md)
- [409. Longest Palindrome](../../leetcode_questions/409_longest_palindrome.md)
- [438. Find All Anagrams in a String](../../leetcode_questions/438_find_all_anagrams_in_a_string.md)