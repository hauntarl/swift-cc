# Challenge 6

## Remove duplicate letters from a string

> **Difficulty**: Easy

Write a function that accepts a `String` as its input, and returns the same `String` just with
*duplicate letters removed*.

> **Tip**: If you can solve this challenge without a `for-in` loop, you can consider it *“tricky”* rather than *“easy”*.

### Sample input and output

- The string *“wombat”* should print *“wombat”*.
- The string *“hello”* should print *“helo”*.
- The string *“Mississippi”* should print *“Misp”*.

### Stub

``` swift
import Foundation

func challenge6(input: String) -> String { 
    // your code goes here
    return ""
}

// test cases
assert(challenge6(input: "wombat") == "wombat", "Challenge 6: Test #1 - failed")
assert(challenge6(input: "hello") == "helo", "Challenge 6: Test #2 - failed")
assert(challenge6(input: "Mississippi") == "Misp", "Challenge 6: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

- *Sets* are great at *removing duplicates*, but bad at retaining order.
- `Foundation` does have a way of forcing `sets` to retain their order, but you need to handle the typecasting.
- You can create *strings* out of *character arrays*.
- You can solve this functionally using *filter()*.

### Solution 1

``` swift
import Foundation

func challenge6(input: String) -> String { 
    var unq = Set<Character>()
    return input.filter { unq.update(with: $0) == nil }
}

// test cases
assert(challenge6(input: "wombat") == "wombat", "Challenge 6: Test #1 - failed")
assert(challenge6(input: "hello") == "helo", "Challenge 6: Test #2 - failed")
assert(challenge6(input: "Mississippi") == "Misp", "Challenge 6: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge6(input: String) -> String { 
    var used = [Character: Bool]()
    return input.filter { used.updateValue(true, forKey: $0) == nil }
}

// test cases
assert(challenge6(input: "wombat") == "wombat", "Challenge 6: Test #1 - failed")
assert(challenge6(input: "hello") == "helo", "Challenge 6: Test #2 - failed")
assert(challenge6(input: "Mississippi") == "Misp", "Challenge 6: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`
