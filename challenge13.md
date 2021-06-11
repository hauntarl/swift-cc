# Challenge 13

## Run-length encoding

> **Difficulty**: Taxing

Write a function that accepts a `String` as input, then returns *how often each letter is repeated* in a single run, *taking case into account*.

> **Tip**: This approach is used in a simple lossless compression technique called run-length encoding.

### Sample input and output

- The string *“aabbcc”* should return *“a2b2c2”*.
- The strings *“aaabaaabaaa”* should return *“a3b1a3b1a3”*
- The string *“aaAAaa”* should return *“a2A2a2”*

### Stub

``` swift
import Foundation

func challenge13(input: String) -> String { 
    // your code goes here
    return ""
}

// test cases
assert(challenge13(input: "aabbcc") == "a2b2c2", "Challenge 13: Test #1 - failed")
assert(challenge13(input: "aaabaaabaaa") == "a3b1a3b1a3", "Challenge 13: Test #2 - failed")
assert(challenge13(input: "aaAAaa") == "a2A2a2", "Challenge 13: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. This would be quite straightforward in other languages using *character lookahead*, but that’s expensive in `Swift` thanks to *grapheme clusters* – `String` isn’t an `Array`.
2. To use the *“Swifty”* approach of looping over your string as-is, make sure you *keep track of* the *current character*, and its *count*, as you loop over the string.
3. Alternatively, consider *converting* your `String` to a proper `Array` that you can index into freely, so you can look ahead to compare letters.

### Solution 1

``` swift
import Foundation

func challenge13(input: String) -> String {
    // convert input to an array for random access
    let input = Array(input)

    // setup index and result
    var (index, result) = (0, "")
    while index < input.count {
        // first character with which following will be compared
        let first = input[index]
        // how many times first character appears consecutively
        var count = 0
        // move forward until different character is found
        // or end of input
        repeat { 
            index += 1
            count += 1
        } while index < input.count && first == input[index]
        // encode current character with its count into result
        result += "\(first)\(count)"
    }
    return result
}

// test cases
assert(challenge13(input: "aabbcc") == "a2b2c2", "Challenge 13: Test #1 - failed")
assert(challenge13(input: "aaabaaabaaa") == "a3b1a3b1a3", "Challenge 13: Test #2 - failed")
assert(challenge13(input: "aaAAaa") == "a2A2a2", "Challenge 13: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge13(input: String) -> String {
    var result = ""
    var first: Character?
    var count = 0
    for ch in input {
        if first == ch {
            count += 1
            continue
        }
        
        if let value = first { result += "\(value)\(count)" }
        (first, count) = (ch, 1)
    }
    
    if let value = first { result += "\(value)\(count)" }
    return result
}

// test cases
assert(challenge13(input: "aabbcc") == "a2b2c2", "Challenge 13: Test #1 - failed")
assert(challenge13(input: "aaabaaabaaa") == "a3b1a3b1a3", "Challenge 13: Test #2 - failed")
assert(challenge13(input: "aaAAaa") == "a2A2a2", "Challenge 13: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`
