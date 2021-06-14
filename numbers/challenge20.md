# Challenge 20

## Number is prime

> **Difficulty**: Tricky

Write a function that accepts an `Int` as its parameter and returns `true` if the number is *prime*.

> **Tip**: A number is considered prime if it is greater than one and has no positive divisors other than 1 and itself.

### Sample input and output

- The number `11` should return `true`.
- The number `13` should return `true`.
- The number `4` should return `false`.
- The number `9` should return `false`.
- The number `16777259` should return `true`.

### Stub

``` swift
import Foundation

func challenge20(num: Int) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge20(num: 11) == true, "Challenge 20: Test #1 - failed")
assert(challenge20(num: 13) == true, "Challenge 20: Test #2 - failed")
assert(challenge20(num: 4) == false, "Challenge 20: Test #3 - failed")
assert(challenge20(num: 9) == false, "Challenge 20: Test #4 - failed")
assert(challenge20(num: 16777259) == true, "Challenge 20: Test #5 - failed")
assert(challenge20(num: 1) == false, "Challenge 20: Test #6 - failed")
assert(challenge20(num: -1) == false, "Challenge 20: Test #7 - failed")
assert(challenge20(num: 3) == true, "Challenge 20: Test #8 - failed")
assert(challenge20(num: 2) == true, "Challenge 20: Test #9 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You should start with a *brute force approach*: loop through every number from 2 up to one less than the input number, and check whether the input number divides into it.
2. You can shrink the search space by searching up to a smaller number – what’s the highest it could be?
3. There’s no point searching higher than the square root of your input number, rounding up.

### Solution 1

``` swift
import Foundation

extension Int {
    func squareRoot() -> Int { Int(ceil(sqrt(Double(self)))) }
}

func challenge20(num: Int) -> Bool { 
    if num <= 1 { return false }
    if num == 2 { return true }

    for div in 2...num.squareRoot() where num % div == 0 { return false }
    return true
}

// test cases
assert(challenge20(num: 11) == true, "Challenge 20: Test #1 - failed")
assert(challenge20(num: 13) == true, "Challenge 20: Test #2 - failed")
assert(challenge20(num: 4) == false, "Challenge 20: Test #3 - failed")
assert(challenge20(num: 9) == false, "Challenge 20: Test #4 - failed")
assert(challenge20(num: 16777259) == true, "Challenge 20: Test #5 - failed")
assert(challenge20(num: 1) == false, "Challenge 20: Test #6 - failed")
assert(challenge20(num: -1) == false, "Challenge 20: Test #7 - failed")
assert(challenge20(num: 3) == true, "Challenge 20: Test #8 - failed")
assert(challenge20(num: 2) == true, "Challenge 20: Test #9 - failed")
```

> **Time Complexity** (worst case): `O(sqrt(n))` - when the number is prime
