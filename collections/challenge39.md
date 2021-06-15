# Challenge 39

## Sort a string array by length

> **Difficulty**: Easy

Extend collections with a function that returns an array of strings sorted by their lengths, longest first.

### Sample input and output

- The code `["a", "abc", "ab"].challenge39()` should return `["abc", "ab", "a"]`.
- The code `["paul", "taylor", "adele"].challenge39()` should return `["taylor", "adele", "paul"]`.
- The code `[String]().challenge39()` should return `[]`.

### Stub

``` swift
import Foundation

extension Collection {
    func challenge39() -> [Element] {
        // your code goes here
        return []
    }
}

// test cases
assert(["a", "abc", "ab"].challenge39() == ["abc","ab", "a"], "Challenge 39: Test #1 - failed")
assert(["paul", "taylor", "adele"].challenge39() == ["taylor", "adele", "paul"], "Challenge 39: Test #2 - failed")
assert([String]().challenge39() == [], "Challenge 39: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to extend the `Collection` type with a specific constraint rather than a protocol constraint.
2. You should use the built-in `sorted()` method.
3. You can provide a custom closure to `sorted()` to affect how it works.

### Solution 1

``` swift
import Foundation

extension Collection where Element == String {
    func challenge39() -> [Element] { 
        sorted { $0.count > $1.count } 
    }
}

// test cases
assert(["a", "abc", "ab"].challenge39() == ["abc","ab", "a"], "Challenge 39: Test #1 - failed")
assert(["paul", "taylor", "adele"].challenge39() == ["taylor", "adele", "paul"], "Challenge 39: Test #2 - failed")
assert([String]().challenge39() == [], "Challenge 39: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n*log(n))`
