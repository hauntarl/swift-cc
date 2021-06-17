# Challenge 46

## Recreate map()

> **Difficulty**: Tricky

Write an extension for all collections that reimplements the `map()` method.

### Sample input and output

- The code `[1, 2, 3].challenge46 { String($0) }` should return `["1", "2", "3"]`
- The code `["1", "2", "3"].challenge46 { Int($0)! }` should return `[1, 2, 3]`

### Stub

``` swift
import Foundation

extension Collection {
    func challenge46() {
        // your code goes here
        return
    }
}

// test cases
assert([1, 2, 3].challenge46 { String($0) } == ["1", "2", "3"], "Challenge 46: Test #1 - failed")
assert(["1", "2", "3"].challenge46 { Int($0)! } == [1, 2, 3], "Challenge 46: Test #2 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to extend the `Collection` type.
2. Your transformation function should accept a parameter of type `Iterator.Element`, but must return a *generic parameter*.
3. You should accept transformation functions that `throws`, but you don’t want to handle any exceptions in your mapping method.
4. Non-throwing functions are sub-types of throwing functions.
5. You really ought to use `rethrows` to avoid irritating users who use non-throwing functions.

### Solution 1

``` swift
import Foundation

extension Collection {
    func challenge46<Result>(transform: (Element) throws -> Result) rethrows -> [Result] {
        var result = [Result]()
        result.reserveCapacity(count)
        for item in self { try result.append(transform(item)) }
        return result
    }
}

// test cases
assert([1, 2, 3].challenge46 { String($0) } == ["1", "2", "3"], "Challenge 46: Test #1 - failed")
assert(["1", "2", "3"].challenge46 { Int($0)! } == [1, 2, 3], "Challenge 46: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(n)`
