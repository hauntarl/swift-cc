# Challenge 19

## Swap two numbers

> **Difficulty**: Easy

Swap two positive variable integers, a and b, without using a temporary variable.

### Sample input and output

- Before running your code *a* should be `1` and *b* should be `2`; afterwards, *b* should be `1` and *a* should be `2`.

### Stub

``` swift
import Foundation

func challenge19(_ a: inout Int, _  b: inout Int) {
    // your code goes here
}

// test cases
var (a, b) = (1, 2)
challenge19(&a, &b)
assert((a, b) == (2, 1), "Challenge 19: Test #1 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. There are lots of ways to solve this, but probably the easiest to remember is using *tuples*.
2. Alternatively, try using the global Swift function `swap()`.
3. If you’re feeling fancy, you can solve this problem with *arithmetic*.
4. If you’re feeling fancy and want to demonstrate your bit manipulation skills, you can also solve this problem using *bitwise XOR*.

### Solution 1

``` swift
import Foundation

func challenge19(_ a: inout Int, _  b: inout Int) {
    // (a, b) = (b, a) // solution 1 - idiomatic
    // swap(&a, &b)    // solution 2 - micro-optimized to be as fast as possible
    a = a + b
    b = a - b
    a = a - b
}

// test cases
var (a, b) = (1, 2)
challenge19(&a, &b)
assert((a, b) == (2, 1), "Challenge 19: Test #1 - failed")
```

> **Time Complexity** (worst case): `O(1)`
