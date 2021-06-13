# Challenge 21

## Counting binary ones

> **Difficulty**: Tricky

Create a function that accepts any positive integer and returns the next highest and next lowest number that has the same number of ones in its binary representation. If either number is not possible, return nil for it.

### Sample input and output

- The number `12` is `1100` in binary, so it has two 1s. The next highest number with that many 1s is `17`, which is `10001`. The next lowest is `10`, which is `1010`.
- The number `28` is `11100` in binary, so it has three 1s. The next highest number with that many 1s is `35`, which is `100011`. The next lowest is `26`, which is `11010`.

### Stub

``` swift
import Foundation

func challenge21(num: Int) -> (high: Int, low: Int) { 
    // your code goes here
    return (0, 0)
}

// test cases
assert(challenge21(num: 12) == (17, 10), "Challenge 21: Test #1 - failed")
assert(challenge21(num: 28) == (35, 26), "Challenge 21: Test #2 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can find the binary representation of an integer by converting it to a string – look for a *“radix”* initializer.
2. You should be using *radix 2*, which is binary.
3. Your return value ought to be `(nextHighest: Int?, nextLowest: Int?)`.
4. You can count the 1s in a stringified number by using `filter()` on its letters property.
5. Don’t be afraid to duplicate code while you’re working – you need to search up and down for the same thing, so start with duplication then refactor.
6. You can’t create ranges where the end is higher than the start. Instead, create a forwards range then reverse it.

### Solution 1

``` swift
import Foundation

extension Int {
    // count 1s in the binary representation of given number
    func ones() -> Int { String(self, radix: 2).filter { $0 == "1"}.count }
}

func challenge21(num: Int) -> (high: Int?, low: Int?) {
    let count = num.ones()
    return (
        (num + 1...Int.max).lazy.first { count == $0.ones() },
        (0..<num).reversed().lazy.first { count == $0.ones() }
    )
}

// test cases
assert(challenge21(num: 12) == (17, 10), "Challenge 21: Test #1 - failed")
assert(challenge21(num: 28) == (35, 26), "Challenge 21: Test #2 - failed")
```
