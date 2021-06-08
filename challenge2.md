# Challenge 2

## Is a string a palindrome?

> Difficulty: **Easy**

Write a function that accepts a `String` as its only parameter, and `returns true` if the string
reads the same when reversed, `ignoring case`.

### Sample input and output

- The string `“rotator”` should `return true`.
- The string `“Rats live on no evil star”` should `return true`.
- The string `“Never odd or even”` should `return false`; even though the letters are the same in reverse the spaces are in different places.
- The string `“Hello, world”` should `return false` because it reads `“dlrow ,olleH”` backwards.

### Stub

``` swift
import Foundation

func challenge2(input: String) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge2(input: "rotator") == true, "Challenge 2: Test #1 - failed")
assert(challenge2(input: "Rats live on no evil star") == true, "Challenge 2: Test #2 - failed")
assert(challenge2(input: "Never odd or even") == false, "Challenge 2: Test #3 - failed")
assert(challenge2(input: "Hello, world") == false, "Challenge 2: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can reverse arrays using their `.reversed()` method.
2. Two arrays compare as equal if they contain the same items in the same order. They are `value types` in Swift, so it doesn’t matter how they were created, as long as their values are the same.
3. `String` aren’t really arrays, but you can make them one using `Array()`.
4. You need to `ignore case`, so consider forcing the `string` to either `lowercase` or `uppercase` before comparing.

### Solution 1

``` swift
import Foundation

func challenge2(input: String) -> Bool {
    // convert input string into an array of lower case characters
    let input = Array(input.lowercased())
    // traverse the input in two directions:
    // . from the beginning: i
    // . from the end: j
    var i = 0, j = input.count - 1
    // end the loop, when i and j meet in the middle or cross each other
    while i < j {
        // compare the characters present at these two indices:
        // . if characters are not same, return false
        if input[i] != input[j] { return false }
        i += 1
        j -= 1
    }
    // if the input string is a palindrome
    return true
}

// test cases
assert(challenge2(input: "rotator") == true, "Challenge 2: Test #1 - failed")
assert(challenge2(input: "Rats live on no evil star") == true, "Challenge 2: Test #2 - failed")
assert(challenge2(input: "Never odd or even") == false, "Challenge 2: Test #3 - failed")
assert(challenge2(input: "Hello, world") == false, "Challenge 2: Test #4 - failed")
```

> **Time Complexity** (worst case) `O(n)` - when the string is a palindrome.

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge2(input: String) -> Bool {
    let lowercase = input.lowercased()
    return lowercase.reversed() == Array(lowercase)
}

// test cases
assert(challenge2(input: "rotator") == true, "Challenge 2: Test #1 - failed")
assert(challenge2(input: "Rats live on no evil star") == true, "Challenge 2: Test #2 - failed")
assert(challenge2(input: "Never odd or even") == false, "Challenge 2: Test #3 - failed")
assert(challenge2(input: "Hello, world") == false, "Challenge 2: Test #4 - failed")
```

> **Time Complexity** (worst case) `O(n)` - when the string is a palindrome.
