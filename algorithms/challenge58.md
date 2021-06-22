# Challenge 58

## Balanced brackets

> **Difficulty**: Easy

Write a function that accepts a string containing the characters (, [, {, <, >, }, ], and ) in any arrangement and frequency. It should return true if the brackets are opened and closed in the correct order, and if all brackets are closed. Any other input should false.

### Sample input and output

- The string `"()"` should return `true`.
- The string `"([])"` should return `true`.
- The string `"([])(<{}>)"` should return `true`.
- The string `"([]{}<[{}]>)"` should return `true`.
- The string `“”` should return `true`.
- The string `"}{"` should return `false`.
- The string `"([)"` should return `false`.
- The string `"([)"` should return `false`.
- The string `"(["` should return `false`.
- The string `"[<<<{}>>]"` should return `false`.
- The string `"hello"` should return `false`.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert(challenge58(input: "()") == true, "Challenge 58: Test #1 - failed")
assert(challenge58(input: "([])") == true, "Challenge 58: Test #2 - failed")
assert(challenge58(input: "([])(<{}>)") == true, "Challenge 58: Test #3 - failed")
assert(challenge58(input: "([]{}<[{}]>)") == true, "Challenge 58: Test #4 - failed")
assert(challenge58(input: "") == true, "Challenge 58: Test #5 - failed")

assert(challenge58(input: "}{") == false, "Challenge 58: Test #6 - failed")
assert(challenge58(input: "([)") == false, "Challenge 58: Test #7 - failed")
assert(challenge58(input: "([)") == false, "Challenge 58: Test #8 - failed")
assert(challenge58(input: "([") == false, "Challenge 58: Test #9 - failed")
assert(challenge58(input: "[<<<{}>>]") == false, "Challenge 58: Test #10 - failed")
assert(challenge58(input: "hello") == false, "Challenge 58: Test #11 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You should start by making the most simple check: does the string have only the eight different characters that are allowed?
2. Each type of opening bracket has only one matching opening bracket, so you should store that data somehow – a dictionary would seem sensible.
3. Every bracket need to be closed at some point, but not necessarily immediately – it might be closed many characters later, for example. So, you need to push it onto a stack, then wait.
4. As you loop over each character in the string, it’s either an opening bracket or a closing bracket. If it’s an opening one it can go on your stack; if it’s a closing one, then it should be the matching pair of whatever is on the end of your bracket stack.
5. If the function ends with anything left in the bracket stack it means there was one bracket that was not closed – a failure.

### Solution 1

``` swift
import Foundation

let brackets = Set("[]{}()<>")
let matching: [Character: Character] = [
    "]": "[", "}": "{", ")": "(", ">": "<"
]

func challenge58(input: String) -> Bool {
    var stack = [Character]()
    for ch in input {
        if !brackets.contains(ch) { return false }

        if let open = matching[ch] {
            guard let top = stack.popLast() else { return false }
            if open != top { return false }
        }
        else { stack.append(ch) }
    }
    return stack.isEmpty
}

// test cases
assert(challenge58(input: "()") == true, "Challenge 58: Test #1 - failed")
assert(challenge58(input: "([])") == true, "Challenge 58: Test #2 - failed")
assert(challenge58(input: "([])(<{}>)") == true, "Challenge 58: Test #3 - failed")
assert(challenge58(input: "([]{}<[{}]>)") == true, "Challenge 58: Test #4 - failed")
assert(challenge58(input: "") == true, "Challenge 58: Test #5 - failed")

assert(challenge58(input: "}{") == false, "Challenge 58: Test #6 - failed")
assert(challenge58(input: "([)") == false, "Challenge 58: Test #7 - failed")
assert(challenge58(input: "([)") == false, "Challenge 58: Test #8 - failed")
assert(challenge58(input: "([") == false, "Challenge 58: Test #9 - failed")
assert(challenge58(input: "[<<<{}>>]") == false, "Challenge 58: Test #10 - failed")
assert(challenge58(input: "hello") == false, "Challenge 58: Test #11 - failed")
```

> **Time Complexity** (worst case): `O(n)`
