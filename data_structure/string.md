# String

## 定义
String is a sequence of characters, and it is a non-primitive data type. It is usually a string object.
primitive type指的是boolean, int, char, double, long, byte, short, float

```c++
// c++ Implementation
#include <string>

// Initial string
std::string a;
a = "123";
std::string b ("abc");
```

## 常用methods
String provides lots of methods as it is an object.

```c++
// Check Length
int len = a.length();

if(a.empty()){
    // Do something in here
}

// Access elements in string
char c = a[0];
char d = a.at(0);

// Operate string
a += b;      // a = "123abc"
a.append(b); // a = "123abcabc"
a.insert(0, "abc"); // a = "abc123abcabc"
a.erase(0, 3);      // a = "123abcabc"

// Search string
std::size_t found = a.find("abc");
if (found != std::string::npos){
    // Do somthing in here
}
```
