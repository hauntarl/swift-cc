# Challenge 38

## Find N smallest

> **Difficulty**: Easy

Write an extension for all collections that returns the N smallest elements as an array, sorted smallest first, where N is an integer parameter.

### Sample input and output

- The code `[1, 2, 3, 4].challenge38(count: 3)` should return `[1, 2, 3]`.
- The code `["q", "f", "k"].challenge38(count: 10)` should return `[“f”, “k”, “q”]`.
- The code `[256, 16].challenge38(count: 3)` should return `[16, 256]`.
- The code `[String]().challenge38(count: 3)` should return an *empty* array.

### Stub

``` swift
import Foundation

extension Collection {
    func challenge38(count: Int) -> [Element] {
        // your code goes here
        return []
    }
}

// test cases
assert([1, 2, 3, 4].challenge38(count: 3) == [1, 2, 3], "Challenge 38: Test #1 - failed")
assert(["q", "f", "k"].challenge38(count: 10) == ["f", "k", "q"], "Challenge 38: Test #2 - failed")
assert([256, 16].challenge38(count: 3) == [16, 256], "Challenge 38: Test #3 - failed")
assert([String]().challenge38(count: 3) == [String](), "Challenge 38: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to extend the `Collection` type with a constraint.
2. Finding the smallest of any value requires using the < operator, which is guaranteed to exist when something conforms to `Comparable`
3. The collection might be contain fewer than N items.
4. The solution is made more interesting by the requirement to return a variable number of results.
5. If you want to avoid complexity, use `sorted()`.

### Solution 1

``` swift
extension Collection where Element: Comparable {
    func challenge38(count: Int) -> [Element] {
        return Array(sorted()[0..<Swift.min(self.count, count)])
    }
}

// test cases
assert([1, 2, 3, 4].challenge38(count: 3) == [1, 2, 3], "Challenge 38: Test #1 - failed")
assert(["q", "f", "k"].challenge38(count: 10) == ["f", "k", "q"], "Challenge 38: Test #2 - failed")
assert([256, 16].challenge38(count: 3) == [16, 256], "Challenge 38: Test #3 - failed")
assert([String]().challenge38(count: 3) == [String](), "Challenge 38: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n*log(n))`

### Solution 2 - Paul Hudson

``` swift
extension Collection where Element: Comparable {
    func challenge38(count: Int) -> [Element] {
        return Array(sorted().prefix(count))
    }
}

// test cases
assert([1, 2, 3, 4].challenge38(count: 3) == [1, 2, 3], "Challenge 38: Test #1 - failed")
assert(["q", "f", "k"].challenge38(count: 10) == ["f", "k", "q"], "Challenge 38: Test #2 - failed")
assert([256, 16].challenge38(count: 3) == [16, 256], "Challenge 38: Test #3 - failed")
assert([String]().challenge38(count: 3) == [String](), "Challenge 38: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n*log(n))`
