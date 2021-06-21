# Challenge 57

## Isomorphic values

> **Difficulty**: Tricky

Write a function that accepts two values and returns true if they are isomorphic. That is, each part of the value must map to precisely one other, but that might be itself.

> **Tip**: Strings A and B are considered isomorphic if you can replace all instances of each letter with another. For example, “tort” and “pump” are isomorphic, because you can replace both Ts with a P, the O with a U, and the R with an M. For integers you compare individual digits, so 1231 and 4564 are isomorphic numbers. For arrays you compare elements, so [1, 2, 1] and [4, 8, 4] are isomorphic.

### Sample input and output

These are all isomorphic values:

- “clap” and “slap”
- “rum” and “mud”
- “pip” and “did”
- “carry” and “baddy”
- “cream” and “lapse”
- 123123 and 456456
- 3.14159 and 2.03048
- [1, 2, 1, 2, 3] and [4, 5, 4, 5, 6]

These are not isomorphic values:

- “carry” and “daddy” – the Rs have become D, but C has also become D.
- “did” and “cad” – the first D has become C, but the second has remained D.
- “maim” and “same” – the first M has become S, but the second has become E.
- “curry” and “flurry” – the strings have different lengths.
- 112233 and 112211 – the number 1 is being mapped to 1, and the number 3 is also being mapped to 1.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert(challenge57(one: "clap", two: "slap") == true, "Challenge 57: Test #1 - failed")
assert(challenge57(one: "rum", two: "mud") == true, "Challenge 57: Test #2 - failed")
assert(challenge57(one: "pip", two: "did") == true, "Challenge 57: Test #3 - failed")
assert(challenge57(one: "carry", two: "baddy") == true, "Challenge 57: Test #4 - failed")
assert(challenge57(one: "cream", two: "lapse") == true, "Challenge 57: Test #5 - failed")
assert(challenge57(one: 123123, two: 456456) == true, "Challenge 57: Test #6 - failed")
assert(challenge57(one: 3.14159, two: 2.03048) == true, "Challenge 57: Test #7 - failed")
assert(challenge57(one: [1, 2, 1, 2, 3], two: [4, 5, 4, 5, 6]) == true, "Challenge 57: Test #8 - failed")

assert(challenge57(one: "carry", two: "daddy") == false, "Challenge 57: Test #9 - failed")
assert(challenge57(one: "did", two: "cad") == false, "Challenge 57: Test #10 - failed")
assert(challenge57(one: "maim", two: "same") == false, "Challenge 57: Test #11 - failed")
assert(challenge57(one: "curry", two: "flurry") == false, "Challenge 57: Test #12 - failed")
assert(challenge57(one: "112233", two: "112211") == false, "Challenge 57: Test #13 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

### Solution 1

``` swift
import Foundation

func challenge57(one: Any, two: Any) -> Bool {
    let (one, two) = (
        ContiguousArray(String(describing: one)),
        ContiguousArray(String(describing: two))
    )
    if one.count != two.count { return false }
    if Set(one).count != Set(two).count { return false }

    var map = [Character:Character]()
    for (cur, ch1) in one.enumerated() {
        if let ch2 = map[ch1] {
            if ch2 != two[cur] { return false }
        } else { map[ch1] = two[cur] }
    }
    return true
}

// test cases
assert(challenge57(one: "clap", two: "slap") == true, "Challenge 57: Test #1 - failed")
assert(challenge57(one: "rum", two: "mud") == true, "Challenge 57: Test #2 - failed")
assert(challenge57(one: "pip", two: "did") == true, "Challenge 57: Test #3 - failed")
assert(challenge57(one: "carry", two: "baddy") == true, "Challenge 57: Test #4 - failed")
assert(challenge57(one: "cream", two: "lapse") == true, "Challenge 57: Test #5 - failed")
assert(challenge57(one: 123123, two: 456456) == true, "Challenge 57: Test #6 - failed")
assert(challenge57(one: 3.14159, two: 2.03048) == true, "Challenge 57: Test #7 - failed")
assert(challenge57(one: [1, 2, 1, 2, 3], two: [4, 5, 4, 5, 6]) == true, "Challenge 57: Test #8 - failed")

assert(challenge57(one: "carry", two: "daddy") == false, "Challenge 57: Test #9 - failed")
assert(challenge57(one: "did", two: "cad") == false, "Challenge 57: Test #10 - failed")
assert(challenge57(one: "maim", two: "same") == false, "Challenge 57: Test #11 - failed")
assert(challenge57(one: "curry", two: "flurry") == false, "Challenge 57: Test #12 - failed")
assert(challenge57(one: "112233", two: "112211") == false, "Challenge 57: Test #13 - failed")
```

> **Time Complexity** (worst case): `O(n)`
