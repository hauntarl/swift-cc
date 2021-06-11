# Challenge 12

## Find longest prefix

> **Difficulty**: Tricky

Write a function that accepts a `String` of words with a *similar prefix*, *separated by spaces*, and returns the *longest substring* that prefixes all words.

### Sample input and output

- The string *“swift switch swill swim”* should return *“swi”*.
- The string *“flip flap flop”* should return *“fl”*.

### Stub

``` swift
import Foundation

func challenge12(input: String) -> String { 
    // your code goes here
    return ""
}

// test cases
assert(challenge12(input: "swift switch swill swim") == "swi", "Challenge 12: Test #1 - failed")
assert(challenge12(input: "flip flap flop") == "fl", "Challenge 12: Test #2 - failed")
assert(challenge12(input: "") == "", "Challenge 12: Test #3 - failed")
assert(challenge12(input: "flip flip flip") == "flip", "Challenge 12: Test #4 - failed")
assert(challenge12(input: "flipflipflip") == "flipflipflip", "Challenge 12: Test #5 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Start with `components(separatedBy:)` so you can check words with a loop.
2. You’ll need a property for the prefix you’re currently checking as well as for the best prefix you’ve found so far.
3. Make sure you use the `hasPrefix()` method.

### Solution 1

``` swift
import Foundation

func challenge12(input: String) -> String { 
    var input = input.split(separator: " ")
    // check if input is an empty string
    if input.count == 0 { return "" }
    // check if input contains a single word
    if input.count == 1 { return String(input[0]) }
    
    var (curr, best) = ("", "")
    for ch in input.removeFirst() {
        // current prefix
        curr.append(ch)
        // match with rest of the words
        if !input.allSatisfy { $0.hasPrefix(curr) } { return best }
        // if all have same prefix, curr is new longest substring
        best = curr
    }
    return best
}

// test cases
assert(challenge12(input: "swift switch swill swim") == "swi", "Challenge 12: Test #1 - failed")
assert(challenge12(input: "flip flap flop") == "fl", "Challenge 12: Test #2 - failed")
assert(challenge12(input: "") == "", "Challenge 12: Test #3 - failed")
assert(challenge12(input: "flip flip flip") == "flip", "Challenge 12: Test #4 - failed")
assert(challenge12(input: "flipflipflip") == "flipflipflip", "Challenge 12: Test #5 - failed")
```

> **Time Complexity** (worst case): `O(n*m)` - where n = no. of components, m = size of substring
