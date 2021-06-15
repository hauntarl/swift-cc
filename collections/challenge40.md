# Challenge 40

## Missing numbers in array

> **Difficulty**: Easy

Create a function that accepts an array of unsorted numbers from 1 to 100 where zero or more numbers might be missing, and returns an array of the missing numbers.

### Sample input and output

If your test array were created like this:

``` swift
var testArray = Array(1...100)
testArray.remove(at: 25)
testArray.remove(at: 20)
testArray.remove(at: 6)
```

Then your method should `[7, 21, 26]`, because those are the numbers missing from the array.

### Stub

``` swift
import Foundation

func challenge40(input: [Int]) -> [Int] {
    // your code goes here
    return []
}

// test cases
var testArray = Array(1...100)
testArray.remove(at: 25)
testArray.remove(at: 20)
testArray.remove(at: 6)
assert(challenge40(input: testArray) == [7, 21, 26], "Challenge 40: Test #1 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. There’s a naïve solution involving arrays, but it’s very slow.
2. You should try using a `Set`, which has a significantly faster `contains()` method.
3. You can compute the different between two sets using `symmetricDifference()`.

### Solution 1

``` swift
import Foundation

let complete = Set(1...100)

func challenge40(input: [Int]) -> [Int] {
    let input = Set(input)
    return Array(complete.subtracting(input)).sorted()
}

// test cases
var testArray = Array(1...100)
testArray.remove(at: 25)
testArray.remove(at: 20)
testArray.remove(at: 6)
assert(challenge40(input: testArray) == [7, 21, 26], "Challenge 40: Test #1 - failed")
```

> **Time Complexity** (worst case): `O(n)`
