# Challenge 59

## Quicksort

> **Difficulty**: Tricky

Create an extension for arrays that sorts them using the quicksort algorithm.

> **Tip 1**: The quicksort algorithm picks an item from its array to use as the pivot point, then splits itself into either two parts (less than or greater than) or three (less, greater, or equal). These parts then repeat the pivot and split until the entire array has been split, then it gets  rejoined so that less, equal, and greater are in order.
>
> **Tip 2**: I can write quicksort from memory, but I cannot write fully optimized quicksort from memory. It’s a complex beast to wrangle, and it requires careful thinking – honestly, I have better things to keep stored in what little space I have up there! So, don’t feel bad if your attempt is far from ideal: there’s no point creating a perfect solution if you struggle to remember it during an interview.
>
> **Tip 3**: Quicksort is an algorithm so well known and widely used that you don’t even write a space in its name – it’s “quicksort” rather than “quick sort”.

### Sample input and output

- The array `[12, 5, 4, 9, 3, 2, 1]` should become `[1, 2, 3, 4, 5, 9, 12]`.
- The array `["f", "a", "b"]` should become `["a", "b", "f"]`.
- The array `[String]()` should become `[]`.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert([12, 5, 4, 9, 3, 2, 1].challenge59() == [1, 2, 3, 4, 5, 9, 12], "Challenge 59: Test #1 - failed")
assert(["f", "a", "b"].challenge59() == ["a", "b", "f"], "Challenge 59: Test #2 - failed")
assert([String]().challenge59() == [], "Challenge 59: Test #3 - failed")
assert([12, 5, 4, 9, 3, 2, 1, 4, 9, 5, 1].challenge59() == [1, 1, 2, 3, 4, 4, 5, 5, 9, 9, 12], "Challenge 59: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You will need to extend `Array` with a constraint on their elements so that they must be `Comparable` – that’s what lets us sort items.
2. There are lots of ways to pick a pivot point; choosing a random item is probably best.
3. You can do most of the work with `filter()` if you want.
4. For maximum performance, try to solve the challenge in-place using `inout`.

### Solution 1

``` swift
import Foundation

func quicksort<T: Comparable>(
    _ arr: inout ContiguousArray<T>,
    beg: Int, end: Int
) {
    // termination case for recursion
    if end - beg < 1 { return }

    // randomize pivot selection for better performance
    // in worst case scenario
    let pivot = arr[Int.random(in: beg...end)]
    // create a three-way partition:
    // [beg, lower) - elements less than pivot
    // [lower, upper] - elements equal to pivot
    // (upper, end] - elements greater than pivot
    var (cur, lwr, upr) = (beg, beg, end)
    while cur <= upr {
        let val = arr[cur]
        if val < pivot {
            arr.swapAt(lwr, cur)
            lwr += 1
            cur += 1
        } 
        else if val > pivot { 
            arr.swapAt(cur, upr)
            upr -= 1
        } else {
            cur += 1
        }
    }

    // recursively call quicksort for less than
    quicksort(&arr, beg: beg, end: lwr - 1)
    // and greater than elements partition
    quicksort(&arr, beg: upr + 1, end: end)
}

extension Array where Element: Comparable {
    func challenge59() -> [Element] {
        var copy = ContiguousArray(self)
        quicksort(&copy, beg: 0, end: count - 1)
        return Array(copy)
    }
}

// test cases
assert([12, 5, 4, 9, 3, 2, 1].challenge59() == [1, 2, 3, 4, 5, 9, 12], "Challenge 59: Test #1 - failed")
assert(["f", "a", "b"].challenge59() == ["a", "b", "f"], "Challenge 59: Test #2 - failed")
assert([String]().challenge59() == [], "Challenge 59: Test #3 - failed")
assert([12, 5, 4, 9, 3, 2, 1, 4, 9, 5, 1].challenge59() == [1, 1, 2, 3, 4, 4, 5, 5, 9, 9, 12], "Challenge 59: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n*log(n))`
