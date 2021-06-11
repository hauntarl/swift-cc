# Challenge 15

## Reverse the words in a string

> **Difficulty**: Easy

Write a function that returns a `String` with each of its *words reversed* but in the *original order*, *without* using a *loop*.

### Sample input and output

- The string *“Swift Coding Challenges”* should return *“tfiwS gnidoC segnellahC”*.
- The string *“The quick brown fox”* should return *“ehT kciuq nworb xof”*.

### Stub

``` swift
import Foundation

func challenge15(input: String) -> String { 
    // your code goes here
    return ""
}

// test cases
assert(challenge15(input: "Swift Coding Challenges") == "tfiwS gnidoC segnellahC", "Challenge 15: Test #1 - failed")
assert(challenge15(input: "The quick brown fox") == "ehT kciuq nworb xof", "Challenge 15: Test #2 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You should start by converting the `String` into an `Array` by separating on spaces.
2. You can reverse the *characters* in a `String` by calling `reversed()` on it.
3. You can create a string from a character array.
4. You want to convert an `Array` of left to right strings into an array of right to left strings, all without using a loop - this is a perfect use for `map()`.
5. Once you have an array of *reversed strings*, you can create a single string using `joined()`.

### Solution 1

``` swift
import Foundation

func challenge15(input: String) -> String { 
    return input
        .split(separator: " ")
        .map { String($0.reversed()) }
        .joined(separator: " ")
}

// test cases
assert(challenge15(input: "Swift Coding Challenges") == "tfiwS gnidoC segnellahC", "Challenge 15: Test #1 - failed")
assert(challenge15(input: "The quick brown fox") == "ehT kciuq nworb xof", "Challenge 15: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
```

> **Time Complexity** (worst case): `O(n)`
