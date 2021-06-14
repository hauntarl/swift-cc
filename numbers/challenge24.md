# Challenge 24

## Add numbers inside a string

> **Difficulty**: Tricky

Given a string that contains both letters and numbers, write a function that pulls out all the numbers then returns their sum.

### Sample input and output

- The string *“a1b2c3”* should return `6` (1 + 2 + 3).
- The string *“a10b20c30”* should return `60` (10 + 20 + 30).
- The string *“h8ers”* should return `8`.

### Stub

``` swift
import Foundation

func challenge24(input: String) -> Int { 
    // your code goes here
    return 0
}

// test cases
assert(challenge24(input: "a1b2c3") == 6, "Challenge 24: Test #1 - failed")
assert(challenge24(input: "a10b20c30") == 60, "Challenge 24: Test #2 - failed")
assert(challenge24(input: "h8ers") == 8, "Challenge 24: Test #3 - failed")
assert(challenge24(input: "abc") == 0, "Challenge 24: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Creating an *integer* from a *string* returns `Int`? – `nil` if it was a number, or an `Int` otherwise.
2. Use the nil coalescing operator, `??,` to strip out any unwanted optionality.
3. Don’t forget to catch trailing numbers, i.e. where the string ends with a number.
4. You could solve this using regular expressions, in which case I’d grade it as taxing rather than tricky.

### Solution 1

``` swift
import Foundation

let regex = try! NSRegularExpression(pattern: #"\d+"#)

func challenge24(input: String) -> Int {
    return regex.matches(
        in: input, range: NSRange(location: 0, length: input.utf16.count)
    ).reduce(0) { $0 + Int(input[Range($1.range, in: input)!])! }
}

// test cases
assert(challenge24(input: "a1b2c3") == 6, "Challenge 24: Test #1 - failed")
assert(challenge24(input: "a10b20c30") == 60, "Challenge 24: Test #2 - failed")
assert(challenge24(input: "h8ers") == 8, "Challenge 24: Test #3 - failed")
assert(challenge24(input: "abc") == 0, "Challenge 24: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

let regex = try! NSRegularExpression(pattern: #"\d+"#)

func challenge24(input: String) -> Int {
    var (cur, sum) = ("", 0)
    for ch in input {
        let ch = String(ch)

        if Int(ch) != nil {
            cur += ch
        } else {
            sum += Int(cur) ?? 0
            cur = ""
        }
    }
    return sum + (Int(cur) ?? 0)
}

// test cases
assert(challenge24(input: "a1b2c3") == 6, "Challenge 24: Test #1 - failed")
assert(challenge24(input: "a10b20c30") == 60, "Challenge 24: Test #2 - failed")
assert(challenge24(input: "h8ers") == 8, "Challenge 24: Test #3 - failed")
assert(challenge24(input: "abc") == 0, "Challenge 24: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`
