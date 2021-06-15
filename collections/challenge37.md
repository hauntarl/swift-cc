# Challenge 37

## Count the numbers

> **Difficulty**: Easy

Write an extension for collections of integers that returns the number of times a specific digit appears in any of its numbers.

### Sample input and output

- The code `[5, 15, 55, 515].challenge37(count: "5")` should return `6`.
- The code `[5, 15, 55, 515].challenge37(count: "1")` should return `2`.
- The code `[55555].challenge37(count: "5")` should return `5`.
- The code `[55555].challenge37(count: "1")` should return `0`.

### Stub

``` swift
import Foundation

extension Collection {
    func challenge37(count: Character) -> Int {
        // your code goes here
        return 0
    }
}

// test cases
assert([5, 15, 55, 515].challenge37(count: "5") == 6, "Challenge 37: Test #1 - failed")
assert([5, 15, 55, 515].challenge37(count: "1") == 2, "Challenge 37: Test #2 - failed")
assert([55555].challenge37(count: "5") == 5, "Challenge 37: Test #3 - failed")
assert([55555].challenge37(count: "1") == 0, "Challenge 37: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to extend the `Collection` type with a specific constraint rather than a *protocol constraint*.
2. If you convert each number to a string, you can loop over its characters.
3. If you were functionally inclined, you could solve this challenge using `reduce()` and `filter()`.

### Solution 1

``` swift
import Foundation

extension Collection where Element == Int {
    func challenge37(count: Character) -> Int {
        // Steps:
        // 1. convert elements to strings
        // 2. iterate over each element
        // 3. count occurrences of input in each element
        // 4. sum up occurrences of input from each element
        return map { String($0) }.reduce(0) {
            $0 + $1.filter { $0 == count }.count
        }
    }
}

// test cases
assert([5, 15, 55, 515].challenge37(count: "5") == 6, "Challenge 37: Test #1 - failed")
assert([5, 15, 55, 515].challenge37(count: "1") == 2, "Challenge 37: Test #2 - failed")
assert([55555].challenge37(count: "5") == 5, "Challenge 37: Test #3 - failed")
assert([55555].challenge37(count: "1") == 0, "Challenge 37: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`
