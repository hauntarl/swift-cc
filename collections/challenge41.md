# Challenge 41

## Find the median

> **Difficulty**: Easy

Write an extension to collections that accepts an array of Int and returns the median average, or nil if there are no values.

> **Tip**: The mean average is the sum of some numbers divided by how many there are. The median average is the middle of a sorted list. If there is no single middle value – e.g. if there are eight numbers - then the median is the mean of the two middle values.

### Sample input and output

- The code `[1, 2, 3].challenge41()` should return `2`.
- The code `[1, 2, 3].challenge41()` should return `2`.
- The code `[1, 3, 5, 7, 9].challenge41()` should return `5`.
- The code `[1, 2, 3, 4].challenge41()` should return `2.5`.
- The code `[Int]().challenge41()` should return `nil`.

### Stub

``` swift
import Foundation

extension Collection {
    func challenge41() -> Double? {
        // your code goes here
        return nil
    }
}

// test cases
assert([1, 2, 3].challenge41() == 2, "Challenge 41: Test #1 - failed")
assert([1, 2, 3].challenge41() == 2, "Challenge 41: Test #2 - failed")
assert([1, 3, 5, 7, 9].challenge41() == 5, "Challenge 41: Test #3 - failed")
assert([1, 2, 3, 4].challenge41() == 2.5, "Challenge 41: Test #4 - failed")
assert([Int]().challenge41() == nil, "Challenge 41: Test #5 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to extend `Collection` with a specific constraint.
2. The method should return `Double?` because it might be a whole number, it might be a mean average of two numbers, or it might be `nil` if the collection is *empty*.
3. If you divide an odd integer by two, Swift will round down.
4. If you divide an even-numbered collection’s count by two, you’ll get the highest of the two values you need for your mean.
5. Make life easy for yourself: sort the collection first.

### Solution 1

``` swift
import Foundation

extension Collection where Element == Int {
    func challenge41() -> Double? {
        guard count != 0 else { return nil }

        let sorted = self.sorted()
        let middle = count / 2
        var median = Double(sorted[middle])
        if count % 2 == 0 { 
            median += Double(sorted[middle - 1])
            median /= 2
        }
        return median
    }
}

// test cases
assert([1, 2, 3].challenge41() == 2, "Challenge 41: Test #1 - failed")
assert([1, 2, 3].challenge41() == 2, "Challenge 41: Test #2 - failed")
assert([1, 3, 5, 7, 9].challenge41() == 5, "Challenge 41: Test #3 - failed")
assert([1, 2, 3, 4].challenge41() == 2.5, "Challenge 41: Test #4 - failed")
assert([Int]().challenge41() == nil, "Challenge 41: Test #5 - failed")
```

> **Time Complexity** (worst case): `O(n*log(n))`
