# Challenge 1

## Are the letters unique?

> **Difficulty**: Easy

Write a function that accepts a `String` as its only parameter, and returns `true` if the string has only unique letters, taking letter *case into account*.

### Sample input and output

- The string *“No duplicates”* should return `true`.
- The string *“abcdefghijklmnopqrstuvwxyz”* should return `true`.
- The string *“AaBbCc”* should return `true` because the challenge is *case-sensitive*.
- The string *“Hello, world”* should return `false` because of the double Ls and double Os.

### Stub

``` swift
import Foundation

func challenge1(input: String) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge1(input: "No duplicates") == true, "Challenge 1: Test #1 - failed")
assert(challenge1(input: "abcdefghijklmnopqrstuvwxyz") == true, "Challenge 1: Test #2 - failed")
assert(challenge1(input: "AaBbCc") == true, "Challenge 1: Test #3 - failed")
assert(challenge1(input: "Hello, world") == false, "Challenge 1: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You should treat the input *string* like an *array* that contains `Character` elements.
2. You could use a temporary *array* to store *characters* that have been checked, but it’s not necessary.
3. *Sets* are like *arrays*, except they can’t contain duplicate elements.
4. You can create *sets* from *arrays* and *arrays* from *sets*. Both have a `count` property.

### Solution 1

``` swift
import Foundation

func challenge1(input: String) -> Bool { 
    var unq = Set<Character>()
    // for each char in input, check if set already contains it or not
    return input.allSatisfy { unq.update(with: $0) == nil }
}

// test cases
assert(challenge1(input: "No duplicates") == true, "Challenge 1: Test #1 - failed")
assert(challenge1(input: "abcdefghijklmnopqrstuvwxyz") == true, "Challenge 1: Test #2 - failed")
assert(challenge1(input: "AaBbCc") == true, "Challenge 1: Test #3 - failed")
assert(challenge1(input: "Hello, world") == false, "Challenge 1: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)` - when no duplicates are present.

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge1b(input: String) -> Bool {
    return Set(input).count == input.count
}

// test cases
assert(challenge1(input: "No duplicates") == true, "Challenge 1: Test #1 - failed")
assert(challenge1(input: "abcdefghijklmnopqrstuvwxyz") == true, "Challenge 1: Test #2 - failed")
assert(challenge1(input: "AaBbCc") == true, "Challenge 1: Test #3 - failed")
assert(challenge1(input: "Hello, world") == false, "Challenge 1: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)` - for all cases.
