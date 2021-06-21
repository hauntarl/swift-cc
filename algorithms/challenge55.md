# Challenge 55

## Bubble sort

> **Difficulty**: Easy

Create an extension for arrays that sorts them using the bubble sort algorithm.

> **Tip**: A bubble sort repeatedly loops over the items in an array, comparing items that are next to each other and swapping them if they aren’t sorted. This looping continues until all items are in their correct order

### Sample input and output

- The array `[12, 5, 4, 9, 3, 2, 1]` should become `[1, 2, 3, 4, 5, 9, 12]`.
- The array `["f", "a", "b"]` should become `["a", "b", "f"]`.
- The array `[String]()` should become `[]`.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert([12, 5, 4, 9, 3, 2, 1].challenge55() == [1, 2, 3, 4, 5, 9, 12], "Challenge 55: Test #1 - failed")
assert(["f", "a", "b"].challenge55() == ["a", "b", "f"], "Challenge 55: Test #2 - failed")
assert([String]().challenge55() == [], "Challenge 55: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’ll need to extend the `Array` type, but only when its elements conform to `Comparable` so you can establish a sort order.
2. You want to repeat your loop while a condition is `true`, so repeat while makes sense.
3. Watch out for the case when the array is empty.
4. You can swap two values using the global `swap()` function like this: `array.swapAt(a, b)`.
5. If you try printing out the array after each sorting pass you might spot a pattern that you can use to optimize your code.

### Solution 1

``` swift
import Foundation

extension Array where Element: Comparable {
    func challenge55() -> [Element] {
        var array = self
        for end in stride(from: count - 1, to: 0, by: -1) {
            var isSorted = true
            for cur in 0..<end {
                if array[cur] > array[cur + 1] {
                    array.swapAt(cur, cur + 1)
                    isSorted = false
                }
            }
            if isSorted { break }
        }
        return array
    }
}

// test cases
assert([12, 5, 4, 9, 3, 2, 1].challenge55() == [1, 2, 3, 4, 5, 9, 12], "Challenge 55: Test #1 - failed")
assert(["f", "a", "b"].challenge55() == ["a", "b", "f"], "Challenge 55: Test #2 - failed")
assert([String]().challenge55() == [], "Challenge 55: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n^2)`
