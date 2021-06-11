# Challenge 7

## Condense whitespace

> **Difficulty**: Easy

Write a function that returns a `String` with any consecutive spaces replaced with a single space.

### Sample input and output

- The string *“a[space][space][space]b[space][space][space]c”* should return *“a[space]b[space]c”*.
- The string *“[space][space][space][space]a”* should return *“[space]a”*.
- The string *“abc”* should return *“abc”*.

### Stub

``` swift
import Foundation

func challenge7(input: String) -> String { 
    // your code goes here
    return ""
}

// test cases
assert(challenge7(input: "a   b   c") == "a b c", "Challenge 7: Test #1 - failed")
assert(challenge7(input: "    a") == " a", "Challenge 7: Test #2 - failed")
assert(challenge7(input: "abc") == "abc", "Challenge 7: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You might think it a good idea to use `components(separatedBy:)` then `joined()`, but that will struggle with leading and trailing spaces.
2. You could loop over each *character*, keeping track of a *seenSpace* boolean that gets set to true when the previous character was a space.
3. You could use regular expressions.
4. Try using `replacingOccurrences(of:)`

### Solution 1

``` swift
import Foundation

let regex = try! NSRegularExpression(pattern: #"\s+"#)

func challenge7(input: String) -> String {
    return regex.stringByReplacingMatches(
        in: input, 
        range: NSRange(location: 0, length: input.utf16.count), 
        withTemplate: " "
    )
}

// test cases
assert(challenge7(input: "a   b   c") == "a b c", "Challenge 7: Test #1 - failed")
assert(challenge7(input: "    a") == " a", "Challenge 7: Test #2 - failed")
assert(challenge7(input: "abc") == "abc", "Challenge 7: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge7(input: String) -> String {
    return input.replacingOccurrences(
        of: " +", with: " ", 
        options: .regularExpression
    )
}

// test cases
assert(challenge7(input: "a   b   c") == "a b c", "Challenge 7: Test #1 - failed")
assert(challenge7(input: "    a") == " a", "Challenge 7: Test #2 - failed")
assert(challenge7(input: "abc") == "abc", "Challenge 7: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`
