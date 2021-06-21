# Challenge 56

## Insertion sort

> **Difficulty**: Easy

Create an extension for arrays that sorts them using the insertion sort algorithm.

> **Tip**: An insertion sort creates a new, sorted array by removing items individually from the input array and placing them into the correct position in the new array.

### Sample input and output

- The array `[12, 5, 4, 9, 3, 2, 1]` should become `[1, 2, 3, 4, 5, 9, 12]`.
- The array `["f", "a", "b"]` should become `["a", "b", "f"]`.
- The array `[String]()` should become `[]`.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert([12, 5, 4, 9, 3, 2, 1].challenge56() == [1, 2, 3, 4, 5, 9, 12], "Challenge 56: Test #1 - failed")
assert(["f", "a", "b"].challenge56() == ["a", "b", "f"], "Challenge 56: Test #2 - failed")
assert([String]().challenge56() == [], "Challenge 56: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can perform insertion sort in-place, but that takes a little more thinking. Aim for correctness first, and efficiency later.
2. You will need to extend `Array` with a constraint on their elements so that they must be `Comparable` – that’s what lets us sort items.
3. In the most simple solution, you should be able to pick out an item from your source array, then search through your sorted destination array to find where it should go.
4. If you want to try the in-place solution, pull out the current item you want to sort, then keep moving other elements to the right until you find the correct spot for your item.

### Solution 1

``` swift
import Foundation

extension Array where Element: Comparable {
    func challenge55() -> [Element] {
        if isEmpty { return self }

        var arr = self
        for end in 1..<arr.count {
            let val = arr[end]
            var cur = end - 1
            while cur >= 0 && arr[cur] > val {
                arr[cur + 1] = arr[cur]
                cur -= 1
            }
            arr[cur + 1] = val
        }
        return arr
    }
}

// test cases
assert([12, 5, 4, 9, 3, 2, 1].challenge55() == [1, 2, 3, 4, 5, 9, 12], "Challenge 55: Test #1 - failed")
assert(["f", "a", "b"].challenge55() == ["a", "b", "f"], "Challenge 55: Test #2 - failed")
assert([String]().challenge55() == [], "Challenge 55: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n^2)`
