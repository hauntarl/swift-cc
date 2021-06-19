# Challenge 32

## Word frequency

> **Difficulty**: Tricky

Write a function that accepts a filename on disk, loads it into a string, then returns the frequency of a word in that string, taking letter case into account. How you define “word” is worth considering carefully.

> **Tip**: Create different files on your desktop for each of your pieces of sample input, then pass the paths to those files into your function.

### Sample input and output

- A file containing *“Hello, world!”* should return `1` for *“Hello”*
- A file containing *“Hello, world!”* should return `0` for *“Hello,”* – note the comma at the end.
- A file containing *“The rain in Spain falls mainly on the plain”* should return `1` for *"Spain"*, and `1` for *“in”*; the “in” inside rain, Spain, mainly, and plain does not count because it’s not a word by itself.
- A file containing *“I’m a great coder”* should return `1` for *“I’m”*.

### Stub

``` swift
import Foundation

func challenge32(in file: String) -> [String: Int] {
    // your code goes here
    return [:]
}

// test cases
assert(challenge32(in: "test1.txt")["Hello"] == 1, "Challenge 32: Test #1 - failed")
assert(challenge32(in: "test1.txt")["Hello,"] == 0, "Challenge 32: Test #2 - failed")
assert(challenge32(in: "test2.txt")["Spain"] == 1, "Challenge 32: Test #3 - failed")
assert(challenge32(in: "test2.txt")["in"] == 1, "Challenge 32: Test #4 - failed")
assert(challenge32(in: "test3.txt")["I'm"] == 1, "Challenge 32: Test #5 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Being able to ask questions about definitions – *“what is a word?”* is an important skill in white boarding tests.
2. I would suggest that splitting by any non-alphabetic character is a safe choice for defining words to begin with, but watch out for that last test case.
3. There’s a *built-in character set* for letters, which includes uppercase and lowercase letters.
4. All character sets have an *inverted* property that gives you the opposite. For letters that gives you all non-letters.
5. Once you have a set of all non-letters, you can remove ' and split your string on that.
6. The `NSCountedSet` class can count words in an array extremely efficiently.

### Solution 1

``` swift
import Foundation

// if case in-sensitive
// let regex = try! NSRegularExpression(pattern: #"([a-z]+'[a-z]+)|([a-z0-9]+)"#)
// if case sensitive
let regex = try! NSRegularExpression(pattern: #"([a-zA-Z]+'[a-zA-Z]+)|([a-zA-Z0-9]+)"#)

func challenge32(in file: String) -> [String: Int] {
    guard var contents = try? String(contentsOfFile: file) else { 
        return [:]
    }

    var frequency = [String: Int]()
    let matches = regex.matches(
        in: contents,
        range: NSRange(location: 0, length: contents.utf16.count)
    )
    for match in matches {
        let word = String(contents[Range(match.range, in: contents)!])
        frequency[word] = (frequency[word] ?? 0) + 1
    }
    return frequency
}

// test cases
assert(challenge32(in: "test1.txt")["Hello"] == 1, "Challenge 32: Test #1 - failed")
assert(challenge32(in: "test1.txt")["Hello,"] == nil, "Challenge 32: Test #2 - failed")
assert(challenge32(in: "test2.txt")["Spain"] == 1, "Challenge 32: Test #3 - failed")
assert(challenge32(in: "test2.txt")["in"] == 1, "Challenge 32: Test #4 - failed")
assert(challenge32(in: "test3.txt")["I'm"] == 1, "Challenge 32: Test #5 - failed")
```

### Solution 2 - Paul Hudson

``` swift
import Foundation

var nonLetters = CharacterSet.letters.inverted
nonLetters.remove("'")

func challenge32(in file: String) -> [String: Int] {
    guard let contents = try? String(contentsOfFile: file) else { 
        return [:]
    }

    var frequency = [String: Int]()
    contents.components(separatedBy: nonLetters).forEach { 
        frequency[$0] = (frequency[$0] ?? 0) + 1 
    }
    return frequency
}

// test cases
assert(challenge32(in: "test1.txt")["Hello"] == 1, "Challenge 32: Test #1 - failed")
assert(challenge32(in: "test1.txt")["Hello,"] == nil, "Challenge 32: Test #2 - failed")
assert(challenge32(in: "test2.txt")["Spain"] == 1, "Challenge 32: Test #3 - failed")
assert(challenge32(in: "test2.txt")["in"] == 1, "Challenge 32: Test #4 - failed")
assert(challenge32(in: "test3.txt")["I'm"] == 1, "Challenge 32: Test #5 - failed")
```
