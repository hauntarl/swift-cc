# Challenge 23

## Integer disguised as string

> **Difficulty**: Tricky

Write a function that accepts a string and returns true if it contains only numbers, i.e. the digits 0 through 9.

### Sample input and output

- The input *“01010101”* should return `true`.
- The input *“123456789”* should return `true`.
- The letter *“9223372036854775808”* should return `true`.
- The letter *“1.01”* should return `false`; “.” is not a number.

### Stub

``` swift
import Foundation

func challenge23(input: String) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge23(input: "01010101") == true, "Challenge 23: Test #1 - failed")
assert(challenge23(input: "123456789") == true, "Challenge 23: Test #2 - failed")
assert(challenge23(input: "9223372036854775808") == true, "Challenge 23: Test #3 - failed")
assert(challenge23(input: "1.01") == false, "Challenge 23: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can create integers from strings, and Swift will return nil if the conversion failed.
2. The number *“9223372036854775808”* is a precise choice, not just a random string of numbers.
3. Chances are Swift’s integer type will be *64-bit* for you, and it’s signed, which means its maximum value is `2` to the power of `63`, minus `1`, i.e. `9223372036854775807` – that’s one less than the test case you’ve been given.
4. You should look into inverted character sets.
5. Some languages write numbers differently from English.

### Solution 1

``` swift
import Foundation

let numbers = Set("0123456789")

func challenge23(input: String) -> Bool {
    return Set(input).allSatisfy(numbers.contains)
}

// test cases
assert(challenge23(input: "01010101") == true, "Challenge 23: Test #1 - failed")
assert(challenge23(input: "123456789") == true, "Challenge 23: Test #2 - failed")
assert(challenge23(input: "9223372036854775808") == true, "Challenge 23: Test #3 - failed")
assert(challenge23(input: "1.01") == false, "Challenge 23: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

let numbers = CharacterSet(charactersIn: "0123456789").inverted

func challenge23(input: String) -> Bool {
    return input.rangeOfCharacter(from: numbers) == nil
}

// test cases
assert(challenge23(input: "01010101") == true, "Challenge 23: Test #1 - failed")
assert(challenge23(input: "123456789") == true, "Challenge 23: Test #2 - failed")
assert(challenge23(input: "9223372036854775808") == true, "Challenge 23: Test #3 - failed")
assert(challenge23(input: "1.01") == false, "Challenge 23: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`
