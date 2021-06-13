# Challenge 18

## Recreate the pow() function

> **Difficulty**: Easy

Create a function that accepts positive two integers, and raises the first to the power of the second.

> **Tip**: If you name your function myPow() or challenge18(), you’ll be able to use the built-in pow() for your tests. The built-in pow() uses doubles, so you’ll need to typecast.

### Sample input and output

- The inputs `4` and `3` should return `64`, i.e. 4 multiplied by itself 3 times.
- The inputs `2` and `8` should return `256`, i.e. 2 multiplied by itself 8 times.

### Stub

``` swift
import Foundation

func challenge18(base: Int, power: Int) -> Int { 
    // your code goes here
    return 0
}

// test cases
assert(challenge18(base: 4, power: 3) == 64, "Challenge 18: Test #1 - failed")
assert(challenge18(base: 2, power: 8) == 256, "Challenge 18: Test #2 - failed")
assert(challenge18(base: 1, power: 9) == 1, "Challenge 18: Test #3 - failed")
assert(challenge18(base: 9, power: 0) == 1, "Challenge 18: Test #4 - failed")
assert(challenge18(base: 9, power: -1) == 0, "Challenge 18: Test #5 - failed")
assert(challenge18(base: -2, power: 3) == -8, "Challenge 18: Test #6 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

### Solution 1

``` swift
import Foundation

func challenge18(base: Int, power: Int) -> Int {
    if power < 0 { return 0 }
    if base == 1 { return 1 } // optimization #1
    if base == 2 { return base << (power - 1) } // optimization #2

    var res = 1
    for _ in 0..<power { res *= base }
    return res
}

// test cases
assert(challenge18(base: 4, power: 3) == 64, "Challenge 18: Test #1 - failed")
assert(challenge18(base: 2, power: 8) == 256, "Challenge 18: Test #2 - failed")
assert(challenge18(base: 1, power: 9) == 1, "Challenge 18: Test #3 - failed")
assert(challenge18(base: 9, power: 0) == 1, "Challenge 18: Test #4 - failed")
assert(challenge18(base: 9, power: -1) == 0, "Challenge 18: Test #5 - failed")
assert(challenge18(base: -2, power: 3) == -8, "Challenge 18: Test #6 - failed")
```

> **Time Complexity** (worst case): `O(n)`
