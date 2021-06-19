# Challenge 31

## Copy recursively

> **Difficulty**: Easy

Write a function that accepts two paths: the first should point to a directory to copy, and the second should be where the directory should be copied to. Return true if the directory and all its contents were copied successfully; false if the copy failed, or the user specified something other than a directory.

### Sample input and output

- If your directory exists and is readable, the destination is writeable, and the copy succeeded, your function should return `true`.
- Under all other circumstances you should return `false`: if the directory does not exist or was not readable, if the destination was not writeable, if a file was specified rather than a directory, or if the copy failed for any other reason.

### Stub

``` swift
import Foundation

func challenge31(source: String, destination: String) -> Bool {
    return false
}

// test cases
assert(challenge31(source: "source", destination: "destination") == true, "Challenge 31: Test #1 - failed")
assert(challenge31(source: "does-not-exists", destination: "destination") == false, "Challenge 31: Test #2 - failed")
assert(challenge31(source: "not-a-dir.txt", destination: "destination") == false, "Challenge 31: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. FileManager has a dedicated `copyItem()` method that is perfectly capable of recursively copying directories.
2. To comply fully with the challenge, you must ensure the user does not specify a file to copy – this should accept only directories.
3. You should try the `fileExists()` method. It has a second parameter, specified as inout, that returns whether the requested item is a directory.
4. Never used `ObjCBool` before? Lucky you. Create your variable like this: `var isDirectory: ObjCBool = false`. Now call `fileExists()` then use its boolValue property to read the boolean value.

### Solution 1

``` swift
import Foundation

func challenge31(source: String, destination: String) -> Bool {
    let fm = FileManager.default
    var isDir: ObjCBool = false

    if !fm.fileExists(atPath: source, isDirectory: &isDir) || !isDir.boolValue {
        return false
    }

    let src = URL(fileURLWithPath: source)
    let dst = URL(fileURLWithPath: destination)
    do {
        try fm.copyItem(at: src, to: dst)
    } catch {
        print("Copy failed: \(error.localizedDescription)")
        return false
    }
    return true
}

// test cases
assert(challenge31(source: "source", destination: "destination") == true, "Challenge 31: Test #1 - failed")
assert(challenge31(source: "does-not-exists", destination: "destination") == false, "Challenge 31: Test #2 - failed")
assert(challenge31(source: "not-a-dir.txt", destination: "destination") == false, "Challenge 31: Test #3 - failed")
```
