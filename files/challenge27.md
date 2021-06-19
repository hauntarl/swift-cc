# Challenge 27

## Print last lines

> **Difficulty**: Easy

Write a function that accepts a filename on disk, then prints its last N lines in reverse order, all on a single line separated by commas.

### Sample input and output

Here is your test input file:

``` text
Antony And Cleopatra
Coriolanus
Cymbeline
Hamlet
Julius Caesar
King Lear
Macbeth
Othello
Twelfth Night
```

- If asked to print the last `3` lines, your code should output *“Twelfth Night, Othello, Macbeth”*.
- If asked to print the last `100` lines, your code should output *“Twelfth Night, Othello, Macbeth, King Lear, Julius Caesar, Hamlet, Cymbeline, Coriolanus, Antony and Cleopatra”*.
- If asked to print the last `0` lines, your could should print *nothing*.

### Stub

``` swift
import Foundation

func challenge27(file name: String, lines: Int) -> String {
    // your code goes here
    return ""
}

// test cases
assert(challenge27(file: "input.txt", lines: 3) == "Twelfth Night, Othello, Macbeth", "Challenge 27: Test #1 - failed")
assert(challenge27(file: "input.txt", lines: 100) == "Twelfth Night, Othello, Macbeth, King Lear, Julius Caesar, Hamlet, Cymbeline, Coriolanus, Antony and Cleopatra", "Challenge 27: Test #2 - failed")
assert(challenge27(file: "input.txt", lines: 0) == "", "Challenge 27: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Use the `contentsOfFile` initializer to pull in the text, then `components(separatedBy:)` to create an array of lines.
2. Arrays have a built-in `reverse()` method that flip them around in-place.
3. You need to print the last *N* lines, but of course you don’t want to read beyond the size of the array. Make sure you use the `min()` function to choose the lesser of the two.

### Solution 1

``` swift
import Foundation

func challenge27(file name: String, lines: Int) -> String {
    guard let data = try? String(contentsOfFile: name) else { return "" }
    let list = data.components(separatedBy: "\n").reversed()
    return list.prefix(min(lines, list.count)).joined(separator: ", ")
}

// test cases
assert(challenge27(file: "input.txt", lines: 3) == "Twelfth Night, Othello, Macbeth", "Challenge 27: Test #1 - failed")
assert(challenge27(file: "input.txt", lines: 100) == "Twelfth Night, Othello, Macbeth, King Lear, Julius Caesar, Hamlet, Cymbeline, Coriolanus, Antony and Cleopatra", "Challenge 27: Test #2 - failed")
assert(challenge27(file: "input.txt", lines: 0) == "", "Challenge 27: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`
