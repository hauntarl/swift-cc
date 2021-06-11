# Challenge 11

## Three different letters

> **Difficulty**: Easy

Write a function that accepts *two strings*, and returns `true` if they are identical in length but have *no more than three different letters*, taking *case* and *string order* into *account*.

### Sample input and output

- The strings *“Clamp”* and *“Cramp”* would return `true`, because there is one letter difference.
- The strings *“Clamp”* and *“Crams”* would return `true`, because there are two letter differences.
- The strings *“Clamp”* and *“Grams”* would return `true`, because there are three letter differences.
- The strings *“Clamp”* and *“Grans”* would return `false`, because there are four letter differences.
- The strings *“Clamp”* and *“Clam”* would return `false`, because they are different lengths.
- The strings *“clamp”* and *“maple”* should return `false`. Although they differ by only one letter, the letters that match are in different positions.

### Stub

``` swift
import Foundation

func challenge11(one: String, two: String) -> Bool { 
    // your code goes here
    return false
}

// test cases
assert(challenge11(one: "Clamp", two: "Cramp") == true, "Challenge 11: Test #1 - failed")
assert(challenge11(one: "Clamp", two: "Crams") == true, "Challenge 11: Test #2 - failed")
assert(challenge11(one: "Clamp", two: "Grams") == true, "Challenge 11: Test #3 - failed")
assert(challenge11(one: "Clamp", two: "Grans") == false, "Challenge 11: Test #4 - failed")
assert(challenge11(one: "Clamp", two: "Clam") == false, "Challenge 11: Test #5 - failed")
assert(challenge11(one: "clamp", two: "maple") == false, "Challenge 11: Test #6 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. If you value your *sanity*, get both *strings* into *arrays* as *quickly* as possible.
2. You probably want to use the `enumerated()` method on one array, to get the *index* and *character* at the same time.
3. Your function should return `false` as soon as it reaches *four differences*; there’s no point continuing to check characters.
4. Make sure you check the *strings* are the *same size* first, preferably using `guard`.

### Solution 1

``` swift
import Foundation

func challenge11(one: String, two: String) -> Bool {
    let (one, two) = (Array(one), Array(two))
    if one.count != two.count { return false }
    
    var diff = 0
    for (i, ch) in one.enumerated() where ch != two[i] {
        diff += 1
        if diff > 3 { return false }
    }
    return true
}

// test cases
assert(challenge11(one: "Clamp", two: "Cramp") == true, "Challenge 11: Test #1 - failed")
assert(challenge11(one: "Clamp", two: "Crams") == true, "Challenge 11: Test #2 - failed")
assert(challenge11(one: "Clamp", two: "Grams") == true, "Challenge 11: Test #3 - failed")
assert(challenge11(one: "Clamp", two: "Grans") == false, "Challenge 11: Test #4 - failed")
assert(challenge11(one: "Clamp", two: "Clam") == false, "Challenge 11: Test #5 - failed")
assert(challenge11(one: "clamp", two: "maple") == false, "Challenge 11: Test #6 - failed")
```

> **Time Complexity** (worst case): `O(n)` - when two strings have no more than three different letters.
