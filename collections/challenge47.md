# Challenge 47

## Recreate min()

> **Difficulty**: Tricky

Write an extension for all collections that reimplements the `min()` method.

### Sample input and output

- The code `[1, 2, 3].challenge47()` should return `1`.
- The code `["q", "f", "k"].challenge47()` should return `"f"`.
- The code `[4096, 256, 16].challenge47()` should return `16`.
- The code `[String]().challenge47()` should return `nil`.

### Stub

``` swift
import Foundation

extension Collection {
    func challenge47() {
        // your code goes here
        return
    }
}

// test cases
assert([1, 2, 3].challenge47() == 1, "Challenge 47: Test #1 - failed")
assert(["q", "f", "k"].challenge47() == "f", "Challenge 47: Test #2 - failed")
assert([4096, 256, 16].challenge47() == 16, "Challenge 47: Test #3 - failed")
assert([String]().challenge47() == nil, "Challenge 47: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to extend the `Collection` type with a constraint.
2. Finding the smallest of any value requires using the `<` operator, which is guaranteed to exist when something conforms to `Comparable`.
3. The collection might be empty, so you’ll need to return an optional value.
4. You can’t compare an optional value against a non-optional one
5. You can solve this quite beautifully using `reduce()`.

### Solution 1

``` swift
import Foundation

extension Collection where Element: Comparable {
    func challenge47() -> Element? {
        guard let min = first else { return nil }
        return reduce(min) { $1 < $0 ? $1 : $0 }
    }
}

// test cases
assert([1, 2, 3].challenge47() == 1, "Challenge 47: Test #1 - failed")
assert(["q", "f", "k"].challenge47() == "f", "Challenge 47: Test #2 - failed")
assert([4096, 256, 16].challenge47() == 16, "Challenge 47: Test #3 - failed")
assert([String]().challenge47() == nil, "Challenge 47: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`
