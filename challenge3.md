# Challenge 3

## Do two strings contain the same characters?

> Difficulty: **Easy**

Write a function that accepts two `String` parameters, and `returns true` if they contain the same characters in any order `taking into account letter case`.

### Sample input and output

- The strings `“abca”` and `“abca”` should `return true`.
- The strings `“abc”` and `“cba”` should `return true`.
- The strings `“a1 b2”` and `“b1 a2”` should `return true`.
- The strings `“abc”` and `“abca”` should `return false`.
- The strings `“abc”` and `“Abc”` should `return false`.
- The strings `“abc”` and `“cbAa”` should `return false`.

### Stub

``` swift
import Foundation

func challenge3(one: String, two: String) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge3(one: "abca", two: "abca") == true, "Challenge 3: Test #1 - failed")
assert(challenge3(one: "abc", two: "cba") == true, "Challenge 3: Test #2 - failed")
assert(challenge3(one: "a1 b2", two: "b1 a2") == true, "Challenge 3: Test #3 - failed")
assert(challenge3(one: "abc", two: "abca") == false, "Challenge 3: Test #4 - failed")
assert(challenge3(one: "abc", two: "Abc") == false, "Challenge 3: Test #5 - failed")
assert(challenge3(one: "abc", two: "cbAa") == false, "Challenge 3: Test #6 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. This task requires you to handle `duplicate characters`.
2. The naive way to check this is to `loop over` the `characters` in one and check it exists in the other, `removing matches` as you go.
3. A faster solution is to convert both `strings` to `character arrays`.
4. If you `sort` two character `arrays`, then you will have something that is the `same length`
and `identical character for character`.

### Solution 1

``` swift
import Foundation

func challenge3(one: String, two: String) -> Bool {
    var map = [Character: Int]()
    // create a Dictionary of Characters with their respective count
    for ch in one {
        // increment count by 1
        map[ch] = (map[ch] ?? 0) + 1
    }

    // subtract count by 1 for each Character that is also present in two 
    for ch in two {
        // if Character is absent, strings do not contain same set of Characters
        guard let count = map[ch] else { return false }
        // if count becomes negative, two has more number of ch than one
        if count - 1 < 0 { return false }
        map[ch] = count - 1
    }

    // count all the remaining Characters, if count is 0
    // the input strings contain same characters
    return map.values.reduce(0, +) == 0
}

// test cases
assert(challenge3(one: "abca", two: "abca") == true, "Challenge 3: Test #1 - failed")
assert(challenge3(one: "abc", two: "cba") == true, "Challenge 3: Test #2 - failed")
assert(challenge3(one: "a1 b2", two: "b1 a2") == true, "Challenge 3: Test #3 - failed")
assert(challenge3(one: "abc", two: "abca") == false, "Challenge 3: Test #4 - failed")
assert(challenge3(one: "abc", two: "Abc") == false, "Challenge 3: Test #5 - failed")
assert(challenge3(one: "abc", two: "cbAa") == false, "Challenge 3: Test #6 - failed")
```

> **Time Complexity** (worst case) `O(n)` - when count for both strings is equal

### Solution 2 - Paul Hudson

``` swift
import Foundation

let whiteSpace = Character(" ")

func challenge3(one: String, two: String) -> Bool {
    return Array(one).sorted() == Array(two).sorted()
}

// test cases
assert(challenge3(one: "abca", two: "abca") == true, "Challenge 3: Test #1 - failed")
assert(challenge3(one: "abc", two: "cba") == true, "Challenge 3: Test #2 - failed")
assert(challenge3(one: "a1 b2", two: "b1 a2") == true, "Challenge 3: Test #3 - failed")
assert(challenge3(one: "abc", two: "abca") == false, "Challenge 3: Test #4 - failed")
assert(challenge3(one: "abc", two: "Abc") == false, "Challenge 3: Test #5 - failed")
assert(challenge3(one: "abc", two: "cbAa") == false, "Challenge 3: Test #6 - failed")
```

> **Time Complexity** (worst case) `O(nlog(n) + n)` - sorting and comparing
