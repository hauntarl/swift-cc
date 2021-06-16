# Challenge 14

## String permutations

> **Difficulty**: Taxing

Write a function that prints all possible *permutations* of a given input `String`.

> **Tip**: A *string permutation* is any given rearrangement of its letters, for example *“boamtw”* is a permutation of *“wombat”*.

### Sample input and output

- The string *“a”* should print *“a”*.
- The string *“ab”* should *“ab”*, *“ba”*.
- The string *“abc”* should print *“abc”*, *“acb”*, *“bac”*, *“bca”*, *“cab”*, *“cba”*.
- The string *“wombat”* should print *720* permutations.

### Stub

``` swift
import Foundation

func challenge14(input: String) -> [String] { 
    // your code goes here
    return []
}

// test cases
assert(challenge14(input: "a") == ["a"], "Challenge 14: Test #1 - failed")
assert(challenge14(input: "ab") == ["ab", "ba"], "Challenge 14: Test #2 - failed")
assert(challenge14(input: "abc") == ["abc", "acb", "bac", "bca", "cba", "cab"], "Challenge 14: Test #3 - failed")
assert(challenge14(input: "wombat").count == 720, "Challenge 14: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Your function will need to call itself.
2. The number of lines printed should be the *factorial* of the length of your string, e.g. *“wombat”* has six characters, so will have *6*! permutations: *6 x 5 x 4 x 3 x 2 x 1, or 720*.
3. You’ll find it easiest to convert the `String` to a `[Character]` for easier indexing.
4. Each time your function is called, it should loop through all letters in the string so that all combinations are generated.
5. You can slice arrays using `strArray[0...3]`.
6. You can convert *string array slices* into *strings* just by using an initializer: `String(strArray[0...3])`.

### Solution 1

``` swift
import Foundation

// cache factorial results upto 9
func generateFactorials() -> (Int) -> Int {
    var fact = ContiguousArray(repeating: 1, count: 10)
    for i in 1..<fact.count { fact[i] *= (i * fact[i - 1]) }
    return { fact[$0] }
}

let factorial = generateFactorials()

// make the function generic
// accepts input as a reference to avoid memory contention due to copies of input
func permutations<Element>(
    for input: inout ContiguousArray<Element>,
    at index: Int = 0,
    with callback: (ContiguousArray<Element>) -> Void
) {
    // when a single permutation is created
    if index == input.count {
        callback(input)
        return
    }
    
    permutations(for: &input, at: index + 1, with: callback)
    for next in (index + 1)..<input.count {
        input.swapAt(index, next)
        permutations(for: &input, at: index + 1, with: callback)
        input.swapAt(index, next)
    }
}

func challenge14(input: String) -> [String] {
    // use contiguous arrays for better performance
    var input = ContiguousArray(input)
    var index = 0
    // give result array a specified size to avoid re-allocation using append
    var result = ContiguousArray(repeating: "", count: factorial(input.count))
    permutations(for: &input) {
        // store generated permutation at current index and increment index position
        result[index] = String($0)
        index += 1
    }
    // convert contiguous array back to normal one for increased usability
    return Array(result)
}

// test cases
assert(challenge14(input: "a") == ["a"], "Challenge 14: Test #1 - failed")
assert(challenge14(input: "ab") == ["ab", "ba"], "Challenge 14: Test #2 - failed")
assert(challenge14(input: "abc") == ["abc", "acb", "bac", "bca", "cba", "cab"], "Challenge 14: Test #3 - failed")
assert(challenge14(input: "wombat").count == 720, "Challenge 14: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n!)`
