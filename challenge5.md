# Challenge 5

## Count the characters

> **Difficulty**: Easy

Write a function that accepts a `string`, and returns how many *times a specific character appears*, taking *case into account*.

> **Tip**: If you can solve this without using a `for-in` loop, you can consider it a Tricky challenge.

### Sample input and output

- The letter *“a”* appears twice in *“The rain in Spain”*.
- The letter *“i”* appears four times in *“Mississippi”*.
- The letter *“i”* appears three times in *“Hacking with Swift”*.

### Stub

``` swift
import Foundation

func challenge5(input: String, ch: Character) -> Int { 
    // your code goes here
    return 0
}

// test cases
assert(challenge5(input: "", ch: Character("a")) == 0, "Challenge 5: Test #1 - failed")
assert(challenge5(input: "The rain in Spain", ch: Character("a")) == 2, "Challenge 5: Test #2 - failed")
assert(challenge5(input: "Mississippi", ch: Character("i")) == 4, "Challenge 5: Test #3 - failed")
assert(challenge5(input: "Hacking with Swift", ch: Character("i")) == 3, "Challenge 5: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Remember that `String` and `Character` are different data types.
2. Don’t be afraid to go down the brute force route: looping over characters using a `for-in` loop.
3. You could solve this functionally using `reduce()`, but tread carefully.
4. You could solve this using `NSCountedSet`, but I’d be suspicious unless you could justify the extra overhead.

### Solution 1

``` swift
import Foundation

func challenge5(input: String, ch: Character) -> Int { 
    var count = 0
    var i = input.startIndex
    while i < input.endIndex {
        if input[i] == ch { count += 1 }
        i = input.index(after: i)
    }
    return count
}

// test cases
assert(challenge5(input: "", ch: Character("a")) == 0, "Challenge 5: Test #1 - failed")
assert(challenge5(input: "The rain in Spain", ch: Character("a")) == 2, "Challenge 5: Test #2 - failed")
assert(challenge5(input: "Mississippi", ch: Character("i")) == 4, "Challenge 5: Test #3 - failed")
assert(challenge5(input: "Hacking with Swift", ch: Character("i")) == 3, "Challenge 5: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

// has a bit of a overhead, compared to simple for-in loop
func challenge5(input: String, ch: Character) -> Int { 
    return input.reduce(0) { $1 == ch ? $0 + 1 : $0 }
}

// test cases
assert(challenge5(input: "", ch: Character("a")) == 0, "Challenge 5: Test #1 - failed")
assert(challenge5(input: "The rain in Spain", ch: Character("a")) == 2, "Challenge 5: Test #2 - failed")
assert(challenge5(input: "Mississippi", ch: Character("i")) == 4, "Challenge 5: Test #3 - failed")
assert(challenge5(input: "Hacking with Swift", ch: Character("i")) == 3, "Challenge 5: Test #4 - failed")
```

``` swift
import Foundation

func challenge5(input: String, ch: String) -> Int { 
    let modified = input.replacingOccurrences(of: ch, with: "")
    return input.count - modified.count
}


// test cases
assert(challenge5(input: "", ch: "a") == 0, "Challenge 5: Test #1 - failed")
assert(challenge5(input: "The rain in Spain", ch: "a") == 2, "Challenge 5: Test #2 - failed")
assert(challenge5(input: "Mississippi", ch: "i") == 4, "Challenge 5: Test #3 - failed")
assert(challenge5(input: "Hacking with Swift", ch: "i") == 3, "Challenge 5: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`
