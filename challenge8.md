# Challenge 8

## String is rotated

> **Difficulty**: Tricky

Write a function that accepts two *strings*, and returns `true` if one string is rotation of the other, taking *letter case into account*.

> **Tip**: A string rotation is when you take a string, remove some letters from its end, then append them to the front. For example, *“swift”* rotated by two characters would be *“ftswi”*.

### Sample input and output

• The string *“abcde”* and *“eabcd”* should return `true`.
• The string *“abcde”* and *“cdeab”* should return `true`.
• The string *“abcde”* and *“abced”* should return `false`; this is not a string rotation.
• The string *“abc”* and *“a”* should return `false`; this is not a string rotation.

### Stub

``` swift
import Foundation

func challenge8(one: String, two: String) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge8(one: "abcde", two: "eabcd") == true, "Challenge 8: Test #1 - failed")
assert(challenge8(one: "abcde", two: "cdeab") == true, "Challenge 8: Test #2 - failed")
assert(challenge8(one: "abcde", two: "abced") == false, "Challenge 8: Test #3 - failed")
assert(challenge8(one: "abc", two: "a") == false, "Challenge 8: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. A string is only considered a *rotation* if is identical to the original once you factor in the letter movement. That is, *“tswi”* is not a rotation of *“swift”* because it is missing the F.
2. If you write a string twice, it must encapsulate all possible rotations, e.g. *“catcat”* contains *“cat”*, *“tca”*, and *“atc”*.

### Solution 1

``` swift
import Foundation

func challenge8(one: String, two: String) -> Bool {
    Set(one) == Set(two) ? (one + one).contains(two) : false
}

// test cases
assert(challenge8(one: "abcde", two: "eabcd") == true, "Challenge 8: Test #1 - failed")
assert(challenge8(one: "abcde", two: "cdeab") == true, "Challenge 8: Test #2 - failed")
assert(challenge8(one: "abcde", two: "abced") == false, "Challenge 8: Test #3 - failed")
assert(challenge8(one: "abc", two: "a") == false, "Challenge 8: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge8(one: String, two: String) -> Bool {
    guard one.count == two.count else { return false }
    let combined = one + one
    return one.contains(two)
}

// test cases
assert(challenge8(one: "abcde", two: "eabcd") == true, "Challenge 8: Test #1 - failed")
assert(challenge8(one: "abcde", two: "cdeab") == true, "Challenge 8: Test #2 - failed")
assert(challenge8(one: "abcde", two: "abced") == false, "Challenge 8: Test #3 - failed")
assert(challenge8(one: "abc", two: "a") == false, "Challenge 8: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`
