# Challenge 49

## Sum the even repeats

> **Difficulty**: Tricky

Write a function that accepts a variadic array of integers and return the sum of all numbers that appear an even number of times.

### Sample input and output

- The code `challenge49(1, 2, 2, 3, 3, 4)` should return `5`, because the numbers 2 and 3 appear twice each.
- The code `challenge49(5, 5, 5, 12, 12)` should return `12`, because that’s the only number that appears an even number of times.
- The code `challenge49(1, 1, 2, 2, 3, 3, 4, 4)` should return `10`.

### Stub

``` swift
import Foundation

func challenge49() {
    // your code goes here
    return
}

// test cases
assert(challenge49(1, 2, 2, 3, 3, 4) == 5, "Challenge 49: Test #1 - failed")
assert(challenge49(5, 5, 5, 12, 12) == 12, "Challenge 49: Test #2 - failed")
assert(challenge49(1, 1, 2, 2, 3, 3, 4, 4) == 10, "Challenge 49: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. This is a perfect use for `NSCountedSet`.
2. But: `NSCountedSet` doesn’t use generics, so you’ll need to typecast somehow. Expect to be judged on your method of typecasting!
3. You’ll need to use modulus to find numbers that are repeated an even number of times.
4. You’ll need to declare your parameter as `numbers: Int...`.

### Solution 1

``` swift
import Foundation

extension Collection where Element: Hashable {
    func frequency() -> [Element: Int] {
        var map = [Element: Int]()
        for val in self { map[val] = (map[val] ?? 0) + 1 }
        return map
    }
}

func challenge49(_ numbers: Int...) -> Int {
    let map = numbers.frequency()
    return map.reduce(0) { $0 + ($1.value % 2 == 0 ? $1.key : 0) }
}

// test cases
assert(challenge49(1, 2, 2, 3, 3, 4) == 5, "Challenge 49: Test #1 - failed")
assert(challenge49(5, 5, 5, 12, 12) == 12, "Challenge 49: Test #2 - failed")
assert(challenge49(1, 1, 2, 2, 3, 3, 4, 4) == 10, "Challenge 49: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`
