# Challenge 50

## Count the largest range

> **Difficulty**: Tricky

Write a function that accepts an array of positive and negative numbers and returns a closed range containing the position of the contiguous numbers that sum to the highest value, or nil if nothing were found.

> **NOTE**: This is a slightly modified version of Paul Hudson's problem statement, here we are trying to find the max subarray sum, i.e. range of subarray whose sum is maximum

### Sample input and output

- The array `[0, 1, 1, -1, 2, 3, 1]` should return `1...6` with sum as `7`.
- The array `[10, 20, 30, -10, -20, 10, 20]` should return `0...2` with sum as `60`.
- The array `[1, -1, 2, -1]` should return `2...2` with sum as `2`.
- The array `[2, 0, 2, 0, 2]` should return `0...4` with sum as `6`.
- The array `[Int]()` should return nil.

### Stub

``` swift
import Foundation

func challenge50() {
    // your code goes here
    return
}

// test cases
assert(challenge50([0, 1, 1, -1, 2, 3, 1])! == (1...6, 7), "Challenge 50: Test #1 - failed")
assert(challenge50([10, 20, 30, -10, -20, 10, 20])! == (0...2, 60), "Challenge 50: Test #2 - failed")
assert(challenge50([1, -1, 2, -1])! == (2...2, 2), "Challenge 50: Test #3 - failed")
assert(challenge50([2, 0, 2, 0, 2])! == (0...4, 6), "Challenge 50: Test #4 - failed")
assert(challenge50([Int]()) == nil, "Challenge 50: Test #5 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. This challenge is best solved using a little trial and error – start by writing tests to ensure your solution is good as you work.
2. Your return type should be `ClosedRange<Int>?` because there might not be any ranges of positive numbers.
3. This would be a good time to use `enumerated()` to retrieve items and their index from a collection.

### Solution 1

This solution is an extension on **Kadane's Algorithm** for maximum subarray sum

For more details: [https://github.com/hauntarl/real-python/blob/master/cp/max_subarray_sum.py]

``` swift
import Foundation

func challenge50(_ numbers: [Int]) -> (ClosedRange<Int>, Int)? {
    if numbers.isEmpty { return nil }
    
    var (l, h, best) = (0, 0, 0)
    var (i, j, curr) = (0, 0, 0)
    for (k, num) in numbers.enumerated() {
        if num < curr + num {
            // include current number in range
            curr += num
            j += 1
        }
        else { 
            // reset range to start from current number
            curr = num
            (i, j) = (k, k) 
        }
        
        // if current range sum is greater, save it as best range
        if best < curr {
            best = curr
            (l, h) = (i, j)
        }
    }
    return (l...h, best)
}

// test cases
assert(challenge50([0, 1, 1, -1, 2, 3, 1])! == (1...6, 7), "Challenge 50: Test #1 - failed")
assert(challenge50([10, 20, 30, -10, -20, 10, 20])! == (0...2, 60), "Challenge 50: Test #2 - failed")
assert(challenge50([1, -1, 2, -1])! == (2...2, 2), "Challenge 50: Test #3 - failed")
assert(challenge50([2, 0, 2, 0, 2])! == (0...4, 6), "Challenge 50: Test #4 - failed")
assert(challenge50([Int]()) == nil, "Challenge 50: Test #5 - failed")
```

> **Time Complexity** (worst case): `O(n)`
