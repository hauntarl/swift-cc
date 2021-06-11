# Challenge 9

## Find pangrams

> **Difficulty**: Easy

Write a function that returns `true` if it is given a `String` that is an *English pangram*, *ignoring letter case*.

> **Tip**: A pangram is a string that contains every letter of the alphabet at least once.

### Sample input and output

- The string *“The quick brown fox jumps over the lazy dog”* should return `true`.
- The string *“The quick brown fox jumped over the lazy dog”* should return `false`, because it’s missing the S.

### Stub

``` swift
import Foundation

func challenge9(input: String) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge9(input: "The quick brown fox jumps over the lazy dog") == true, "Challenge 9: Test #1 - failed")
assert(challenge9(input: "The quick brown fox jumped over the lazy dog") == false, "Challenge 9: Test #2 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Make sure you start by collapsing case using something like `lowercased()`.
2. You can compare letters using `>`, `>=`, and so on.
3. If you remove duplicates and non-alphabetic characters, the remaining string should add up to 26 letters.

### Solution 1

``` swift
import Foundation

let atoz = Set("abcdefghijklmnopqrstuvwxyz")

func challenge9(input: String) -> Bool {
    return Set(input.lowercased()).intersection(atoz) == atoz
}

// test cases
assert(challenge9(input: "The quick brown fox jumps over the lazy dog") == true, "Challenge 9: Test #1 - failed")
assert(challenge9(input: "The quick brown fox jumped over the lazy dog") == false, "Challenge 9: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge9(input: String) -> Bool {
    let set = Set(input.lowercased())
    let letters = set.filter { $0 >= "a" && $0 <= "z" }
    return letters.count == 26
}

// test cases
assert(challenge9(input: "The quick brown fox jumps over the lazy dog") == true, "Challenge 9: Test #1 - failed")
assert(challenge9(input: "The quick brown fox jumped over the lazy dog") == false, "Challenge 9: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(n)`
