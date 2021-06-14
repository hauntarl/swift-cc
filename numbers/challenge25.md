# Challenge 25

## Calculate a square root by hand

> **Difficulty**: Taxing

Write a function that returns the square root of a positive integer, rounded down to the nearest
integer, without using `sqrt()`.

### Sample input and output

- The number `9` should return `3`.
- The number `16777216` should return `4096`.
- The number `16` should return `4`.
- The number `15` should return `3`.

### Stub

``` swift
import Foundation

func challenge25(num: Int) -> Int { 
    // your code goes here
    return 0
}

// test cases
assert(challenge25(num: 9) == 3, "Challenge 25: Test #1 - failed")
assert(challenge25(num: 16777216) == 4096, "Challenge 25: Test #2 - failed")
assert(challenge25(num: 16) == 4, "Challenge 25: Test #3 - failed")
assert(challenge25(num: 15) == 3, "Challenge 25: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can *brute force* this using a loop count from 0 up to the input number.
2. A more efficient solution is using a binary search.
3. A rounded-down integer square root will never be more than half its square.
4. If you consider half your input number to be your upper bound, then calculate the mid-point between that and a lower bound that’s initially 0 (i.e., input number / 4), you can check whether that mid-point squared gives your input.
5. If the mid-point is too low, make it the new lower bound then repeat. If the mid-point is too high, make it the new higher bound then repeat.
6. Using this technique, you should be able to loop until you find the best answer.

### Solution 1

``` swift
import Foundation

func challenge25(num: Int) -> Int {
    precondition(num >= 0, "Square root of negative number is undefined")
    if num < 2 { return num }
    
    var (beg, end) = (1, num / 2)
    while beg < end {
        let mid = (beg + end) / 2
        switch mid * mid {
        case let sqr where sqr > num: end = mid - 1
        case let sqr where sqr < num: beg = mid + 1
        default: return mid
        }
    }
    return beg
}

// test cases
assert(challenge25(num: 9) == 3, "Challenge 25: Test #1 - failed")
assert(challenge25(num: 16777216) == 4096, "Challenge 25: Test #2 - failed")
assert(challenge25(num: 16) == 4, "Challenge 25: Test #3 - failed")
assert(challenge25(num: 15) == 3, "Challenge 25: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(log(n))` - where n is the input number

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge25(num: Int) -> Int {
    return Int(floor(pow(Double(num), 0.5)))    
}

// test cases
assert(challenge25(num: 9) == 3, "Challenge 25: Test #1 - failed")
assert(challenge25(num: 16777216) == 4096, "Challenge 25: Test #2 - failed")
assert(challenge25(num: 16) == 4, "Challenge 25: Test #3 - failed")
assert(challenge25(num: 15) == 3, "Challenge 25: Test #4 - failed")
```
