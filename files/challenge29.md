# Challenge 29

## Documents directory

> **Difficulty**: Easy

Write a function that returns a `URL` to the user’s documents directory.

### Sample input and output

- Your function should need no input, and return a `URL` pointing to `/Users/yourUserName/Documents` on macOS, and `/path/to/container/Documents` on iOS.

### Stub

``` swift
import Foundation

func challenge29() -> URL {
    // your code goes here
}

// test cases
print(challenge29())
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. This is one you either know or you don’t. I’d be tempted to answer *“that’s something I could find on Google”* if the answer fled from my brain in an interview.
2. You should investigate the `urls(for:in)` method of `FileManager`.
3. The user has only one documents directory.

### Solution 1

``` swift
import Foundation

func challenge29() -> URL {
    let paths = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)
    return paths[0]
}

// test cases
print(challenge29())
```
