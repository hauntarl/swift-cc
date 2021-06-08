# Challenge 4

## Does one string contain another?

> Difficulty: **Medium**

Write your own version of the `contains()` method on `String` that `ignores letter case`, and
`without` using the existing `contains()` method.

### Sample input and output

- The code `"Hello, world".fuzzyContains("Hello")` should `return true`.
- The code `"Hello, world".fuzzyContains("WORLD")` should `return true`.
- The code `"Hello, world".fuzzyContains("Goodbye")` should `return false`.

### Stub

``` swift
import Foundation

extension String {
    func fuzzyContains(_ other: String) -> Bool {
        // your code goes here
        return false
    }
}

// test cases
assert("".fuzzyContains("Hello") == false, "Challenge 4: Test #1 - failed")
assert("Hello".fuzzyContains("Hello, world") == false, "Challenge 4: Test #1 - failed")
assert("Hello, world".fuzzyContains("Hello") == true, "Challenge 4: Test #1 - failed")
assert("Hello, world".fuzzyContains("WORLD") == true, "Challenge 4: Test #2 - failed")
assert("Hello, wor".fuzzyContains("WORLD") == false, "Challenge 4: Test #2 - failed")
assert("Hello, world".fuzzyContains("Goodbye") == false, "Challenge 4: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can’t use `contains()`, but there are other methods that do similar things.
2. Try the `range(of:)` method.
3. To ignore case, you can either `uppercase` both strings, or try the second parameter to `range(of:)`.

### Solution 1

``` swift
import Foundation

extension String {
    func fuzzyContains(_ other: String) -> Bool {
        // if any of the strings is empty, return false
        if self.isEmpty || other.isEmpty { return false }
        
        // convert given strings to lower case to ignore cases
        // convert them again into contiguous arrays for better performance
        let this = ContiguousArray(self.lowercased())
        let other = ContiguousArray(other.lowercased())
        let (len1, len2) = (this.count, other.count)
        // if length of subset greater, then return false
        if len1 < len2 { return false }
        
        // store all the indices of this array where:
        // . first character of other array matches character at i in this array
        // . distance from i to len1 >= length len2
        let fir = other[0]
        var match = [Int](), i = 0
        while i + len2 <= len1 {
            if this[i] == fir { match.append(i) }
            i += 1
        }
        
        // iterate over every valid start index, compare ArraySlice with other
        for i in match {
            if this[(i + 1)..<(i + len2)] == other[1..<len2] { return true }
        }
        // if subset is not found
        return false
    }
}

// test cases
assert("".fuzzyContains("Hello") == false, "Challenge 4: Test #1 - failed")
assert("Hello".fuzzyContains("Hello, world") == false, "Challenge 4: Test #2 - failed")
assert("Hello, world".fuzzyContains("Hello") == true, "Challenge 4: Test #3 - failed")
assert("Hello, world".fuzzyContains("WORLD") == true, "Challenge 4: Test #4 - failed")
assert("Hello, wor".fuzzyContains("WORLD") == false, "Challenge 4: Test #5 - failed")
assert("Hello, world".fuzzyContains("Goodbye") == false, "Challenge 4: Test #6 - failed")
```

> **Time Complexity** (worst case) `O(n + k*m)` - n: conversion, k: matches and m: comparison; where k and m are inversely proportional.

### Solution 2 - Paul Hudson

``` swift
import Foundation

// one
extension String {
    func fuzzyContains(_ string: String) -> Bool {
        return self.uppercased().range(of: string.uppercased()) != nil
    }
}

// two
extension String {
    func fuzzyContains(_ string: String) -> Bool {
        return range(of: string, options: .caseInsensitive) != nil
    }
}

// test cases
assert("".fuzzyContains("Hello") == false, "Challenge 4: Test #1 - failed")
assert("Hello".fuzzyContains("Hello, world") == false, "Challenge 4: Test #2 - failed")
assert("Hello, world".fuzzyContains("Hello") == true, "Challenge 4: Test #3 - failed")
assert("Hello, world".fuzzyContains("WORLD") == true, "Challenge 4: Test #4 - failed")
assert("Hello, wor".fuzzyContains("WORLD") == false, "Challenge 4: Test #5 - failed")
assert("Hello, world".fuzzyContains("Goodbye") == false, "Challenge 4: Test #6 - failed")
```
