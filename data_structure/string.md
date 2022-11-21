# String

String is a sequence of characters, and it is a non-primitive data type. It is usually a string object in modern language.
primitive type指的是boolean, int, char, double, long, byte, short, float

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
```

```go
// go Implementation
package main

import "fmt"

func main() {
	const World = "world"
	var hello = "hello"

	// Concatenate strings.
	var helloWorld = hello + " " + World
	helloWorld += "!"
	fmt.Println(helloWorld) // hello world!

	// Compare strings.
	fmt.Println(hello == "hello")   // true
	fmt.Println(hello > helloWorld) // false

	var hello_sub = helloWorld[:5] // substring
	// 104 is the ASCII code (and Unicode) of char 'h'.
	fmt.Println(hello_sub[0])         // 104
	fmt.Printf("%T \n", hello[0])     // uint8

	// hello[0] is unaddressable and immutable,
	// so the following two lines fail to compile.
	/*
	hello[0] = 'H'         // error
	fmt.Println(&hello[0]) // error
	*/

	// The next statement prints: 5 12 true
	fmt.Println(len(hello), len(helloWorld),
			strings.HasPrefix(helloWorld, hello))
}
```
