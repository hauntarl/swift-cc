# Challenge 16

## Fizz Buzz

> **Difficulty**: Easy

Write a function that counts from 1 through 100, and prints “Fizz” if the counter is evenly divisible by 3, “Buzz” if it’s evenly divisible by 5, “Fizz Buzz” if it’s even divisible by three and five, or the counter number for all other cases.

### Sample input and output

- `1` should print *“1”*
- `2` should print *“2”*
- `3` should print *“Fizz”*
- `4` should print *“4”*
- `5` should print *“Buzz”*
- `15` should print *“Fizz Buzz”*

### Stub

``` swift
import Foundation

func challenge16(number: Int) -> String { 
    // your code goes here
    return ""
}

// test cases
assert(challenge16(number: 1) == "1", "Challenge 16: Test #1 - failed")
assert(challenge16(number: 2) == "2", "Challenge 16: Test #2 - failed")
assert(challenge16(number: 3) == "Fizz", "Challenge 16: Test #3 - failed")
assert(challenge16(number: 4) == "4", "Challenge 16: Test #4 - failed")
assert(challenge16(number: 5) == "Buzz", "Challenge 16: Test #5 - failed")
assert(challenge16(number: 15) == "Fizz Buzz", "Challenge 16: Test #6 - failed")

// count from 1 through 100
for cur in 1...100 { print(challenge16(number: cur)) }
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to use modulus: `%`.
2. Check for the *“Fizz Buzz”* case first, because that’s most specific.
3. Remember to use the *closed range operator* to include the number `100` at the end.

### Solution 1

``` swift
import Foundation

func challenge16(number: Int) -> String { 
    switch (number % 3, number % 5) {
    case (0, 0): return "Fizz Buzz"
    case (0, _): return "Fizz"
    case (_, 0): return "Buzz"
    default: return String(number)
    }
}

// test cases
assert(challenge16(number: 1) == "1", "Challenge 16: Test #1 - failed")
assert(challenge16(number: 2) == "2", "Challenge 16: Test #2 - failed")
assert(challenge16(number: 3) == "Fizz", "Challenge 16: Test #3 - failed")
assert(challenge16(number: 4) == "4", "Challenge 16: Test #4 - failed")
assert(challenge16(number: 5) == "Buzz", "Challenge 16: Test #5 - failed")
assert(challenge16(number: 15) == "Fizz Buzz", "Challenge 16: Test #6 - failed")

// count from 1 through 100
for cur in 1...100 { print(challenge16(number: cur)) }
```

> **Time Complexity** (worst case): `O(n)`
