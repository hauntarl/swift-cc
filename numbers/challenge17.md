# Challenge 17

## Generate a random number in a range

> **Difficulty**: Easy

Write a function that accepts positive minimum and maximum integers, and returns a random number between those two bounds, inclusive.

### Sample input and output

- Given minimum `1` and maximum `5`, the return values *1, 2, 3, 4, 5* are valid.
- Given minimum `8` and maximum `10`, the return values *8, 9, 10* are valid.
- Given minimum `12` and maximum `12`, the return value *12* is valid.
- Given minimum `12` and maximum `18`, the return value *7* is invalid.

### Stub

``` swift
import Foundation

func challenge17(a: Int, b: Int) -> Int { 
    // your code goes here
    return 0
}

// test cases
assert(1...5 ~= challenge17(a: 1, b: 5), "Challenge 17: Test #1 - failed")
assert(8...10 ~= challenge17(a: 8, b: 10), "Challenge 17: Test #2 - failed")
assert(challenge17(a: 12, b: 12) == 12, "Challenge 17: Test #3 - failed")
assert(12...18 ~= challenge17(a: 12, b: 18), "Challenge 17: Test #4 - failed")
assert(1...5 ~= challenge17(a: 5, b: 1), "Challenge 17: Test #5 - failed")
```

### Solution 1

``` swift
import Foundation

func challenge17(a: Int, b: Int) -> Int { 
    return Int.random(in: min(a, b)...max(a, b))
}

// test cases
assert(1...5 ~= challenge17(a: 1, b: 5), "Challenge 17: Test #1 - failed")
assert(8...10 ~= challenge17(a: 8, b: 10), "Challenge 17: Test #2 - failed")
assert(challenge17(a: 12, b: 12) == 12, "Challenge 17: Test #3 - failed")
assert(12...18 ~= challenge17(a: 12, b: 18), "Challenge 17: Test #4 - failed")
assert(1...5 ~= challenge17(a: 5, b: 1), "Challenge 17: Test #5 - failed")
```

> **Time Complexity** (worst case): `O(n)`
