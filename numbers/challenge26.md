# Challenge 26

## Subtract without subtract

> **Difficulty**: Tricky

Create a function that subtracts one positive integer from another, without using -.

### Sample input and output

- The code `challenge26(subtract: 5, from: 9)` should return `4`.
- The code `challenge26(subtract: 10, from: 30)` should return `20`.

### Stub

``` swift
import Foundation

func challenge26(subtract: Int, from: Int) -> Int { 
    // your code goes here
    return 0
}

// test cases
assert(challenge26(subtract: 5, from: 9) == 4, "Challenge 26: Test #1 - failed")
assert(challenge26(subtract: 10, from: 30) == 20, "Challenge 26: Test #2 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. In your code you can use any other operator, or any other number, positive or negative, just not the - operator.
2. Swift has a full set of bitwise operators – operators that manipulate the binary digits of a number.
3. You could try using bitwise NOT, which is ~.

### Solution 1

``` swift
import Foundation

func challenge26(subtract: Int, from: Int) -> Int { 
    return from + (~subtract + 1)
}

// test cases
assert(challenge26(subtract: 5, from: 9) == 4, "Challenge 26: Test #1 - failed")
assert(challenge26(subtract: 10, from: 30) == 20, "Challenge 26: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(1)`
