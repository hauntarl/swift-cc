# Challenge 10

## Vowels and consonants

> **Difficulty**: Easy

Given a `String` in English, return a `Tuple` containing the number of *vowels* and *consonants*.

> **Tip**: Vowels are the letters, A, E, I, O, and U; consonants are the letters B, C, D, F, G, H, J, K, L, M, N, P, Q, R, S, T, V, W, X, Y, Z.

### Sample input and output

- The input *“Swift Coding Challenges”* should return `6` vowels and `15` consonants.
- The input *“Mississippi”* should return `4` vowels and `7` consonants.

### Stub

``` swift
import Foundation

func challenge10(input: String) -> (v: Int, c: Int) { 
    // your code goes here
    return (0, 0)
}

// test cases
assert(challenge10(input: "Swift Coding Challenges") == (6, 15), "Challenge 10: Test #1 - failed")
assert(challenge10(input: "Mississippi") == (4, 7), "Challenge 10: Test #2 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Just because a *letter* is not a *vowel*, it doesn’t mean it’s a *consonant* – think *punctuation*, for example.
2. You’ll need to *differentiate* carefully between the `String` and `Character` types.
3. You could use `CharacterSet` here, but is it really needed?
4. Your return type should be `(vowels: Int, consonants: Int)`.
5. Watch out for uppercase and lowercase letters – an *“A”* is a vowel regardless of its case.

### Solution 1

``` swift
import Foundation

let alphabets = Set("abcdefghijklmnopqrstuvwxyz")
let vowels = Set("aeiou")
let consonants = alphabets.subtracting(vowels)

func challenge10(input: String) -> (v: Int, c: Int) { 
    var (v, c) = (0, 0)
    for ch in input.lowercased() {
        if consonants.contains(ch) { c += 1 }
        else if vowels.contains(ch) { v += 1 }
    }
    return (v, c)
}

// test cases
assert(challenge10(input: "Swift Coding Challenges") == (6, 15), "Challenge 10: Test #1 - failed")
assert(challenge10(input: "Mississippi") == (4, 7), "Challenge 10: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge10(input: String) -> (v: Int, c: Int) { 
    let vowels = "aeiou"
    let consonants = "bcdfghjklmnpqrstvwxyz"
    var vowelCount = 0
    var consonantCount = 0
    for letter in input.lowercased() {
        if vowels.contains(letter) {
            vowelCount += 1
        } else if consonants.contains(letter) {
            consonantCount += 1
        }
    }
    return (vowelCount, consonantCount)
}

// test cases
assert(challenge10(input: "Swift Coding Challenges") == (6, 15), "Challenge 10: Test #1 - failed")
assert(challenge10(input: "Mississippi") == (4, 7), "Challenge 10: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(n)`
