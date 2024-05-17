# Big O Notation

Big O notation, also known as the simply "O", is a way to describe the performance or complexity of an algorithm.

It's used to classify algorithms based on how their running time or space requirements scale with respect to the size of the input.

## Key Aspects
- **Asymptotic notation**: Big O notation is a way to describe an algorithm's performance as the input size increases without bound (i.e., n approaches infinity).
- **Worst-case scenario**: Big O notation measures the maximum amount of time or space required by the algorithm in the worst-case scenario.
- **Upper bound**: Big O notation provides an upper bound on the running time or space usage, which means that the actual performance may be better (but not worse) than what's described.
- **Constant factor ignored**: When describing an algorithm's performance using Big O notation, any constant factors are ignored. For example, O(2n) and O(n) would be considered equivalent because the constant factor 2 is ignored.
- **Only considering worst-case scenario**: Big O notation only considers the worst-case scenario and does not account for average-case or best-case scenarios.

## Common Examples
Below is the list of some of the most used Big O notations and their performance comparisons against different sizes of the input data.

| Big O Notation | Type        | Computations for 10 elements | Computations for 100 elements | Computations for 1000 elements  |
| -------------- | ----------- | ---------------------------- | ----------------------------- | ------------------------------- |
| **O(1)**       | Constant    | 1                            | 1                             | 1                               |
| **O(log N)**   | Logarithmic | 3                            | 6                             | 9                               |
| **O(N)**       | Linear      | 10                           | 100                           | 1000                            |
| **O(N log N)** | n log(n)    | 30                           | 600                           | 9000                            |
| **O(N^2)**     | Quadratic   | 100                          | 10000                         | 1000000                         |
| **O(2^N)**     | Exponential | 1024                         | 1.26e+29                      | 1.07e+301                       |
| **O(N!)**      | Factorial   | 3628800                      | 9.3e+157                      | 4.02e+2567                      |