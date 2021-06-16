# Challenge 42

## Recreate index(of:)

> **Difficulty**: Easy

Write an extension for all collections that reimplements the index(of:) method.

> **Tip**: This is one of the easiest standard library methods to reimplement, so please give it an especially good try before reading any hints.

### Sample input and output

- The code `[1, 2, 3].challenge42(indexOf: 1)` should return `0`.
- The code `[1, 2, 3].challenge42(indexOf: 3)` should return `2`.
- The code `[1, 2, 3].challenge42(indexOf: 5)` should return `nil`.

### Stub

``` swift
import Foundation

extension Collection {
    func challenge42(indexOf element: Element) -> Int? {
        // your code goes here
        return nil
    }
}

// test cases
assert([1, 2, 3].challenge42(indexOf: 1) == 0, "Challenge 42: Test #1 - failed")
assert([1, 2, 3].challenge42(indexOf: 3) == 2, "Challenge 42: Test #2 - failed")
assert([1, 2, 3].challenge42(indexOf: 5) == nil, "Challenge 42: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You will need to extend `Collection` using a constraint on the type of element it stores.
2. Your return type should be `Int?` because the item might not exist in the collection.
3. This would be a good time to use `enumerated()` to retrieve items and their index from a collection.

### Solution 1

``` swift
import Foundation

extension Collection where Element: Equatable {
    func challenge42(indexOf item: Element) -> Int? {
        for (i, val) in enumerated() where val == item { return i }
        return nil
    }
}

// test cases
assert([1, 2, 3].challenge42(indexOf: 1) == 0, "Challenge 42: Test #1 - failed")
assert([1, 2, 3].challenge42(indexOf: 3) == 2, "Challenge 42: Test #2 - failed")
assert([1, 2, 3].challenge42(indexOf: 5) == nil, "Challenge 42: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)` - when item is not found
