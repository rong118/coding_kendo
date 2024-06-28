# Math Topics

## 1. Greatest Common Divisor

The Greatest Common Divisor (GCD) of two or more integers is the largest positive integer that divides each of the integers without leaving a remainder. For example, the GCD of 8 and 12 is 4.

One of the most efficient algorithms to compute the GCD is the Euclidean algorithm. The Euclidean algorithm is based on the principle that the GCD of two numbers a and b (where a>b) is the same as the GCD of 
b and (a mod b).

### Implementation
```c++
#include <iostream>
using namespace std;

// Function to return the GCD of two numbers using the Euclidean algorithm
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int num1, num2;
    cout << "Enter two integers: ";
    cin >> num1 >> num2;

    cout << "GCD of " << num1 << " and " << num2 << " is " << gcd(num1, num2) << endl;

    return 0;
}
```

### LeetCode

- [1979. Find Greatest Common Divisor of Array](../../leetcode_questions/1979_find_greatest_common_divisor.md)