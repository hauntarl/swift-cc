# Challenge 33

## Find duplicate filenames

> **Difficulty**: Tricky

Write a function that accepts the name of a directory to scan, and returns an array of filenames that appear more than once in that directory or any of its subdirectories. Your function should scan all subdirectories, including subdirectories of subdirectories.

### Sample input and output

- If *directory/subdir/a.txt* exists and *directory/sub/sub/sub/sub/subdir/a.txt* exists, *“a.txt”* should be in the array you return.
- Ignore directories that have the same name; you care only about files.
- If there are no files with duplicate names, return an empty array.

### Stub

``` swift
import Foundation

func challenge33(in directory: String) -> [String] {
    // your code goes here
    return []
}

// test cases
print(challenge33(in: "directory"))
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. There are several ways of solving this, but most people instinctively reach for recursion to allow them to scan any depth of directory structure.
2. `FileManager` has better solutions, though – take some time to explore!
3. `FileManager` has an uncomfortable relationship between using `String` and `URL` for its data types. You should prefer the latter wherever possible, however your return value needs to be `[String]` because you care about duplicate names not paths.
4. If you can’t read the directory that was requested, returning an empty array seems
like a sensible thing to do.

### Solution 1

``` swift
import Foundation

func challenge33(in directory: String) -> [String] {
    let fm = FileManager.default
    // create a stack of directory urls
    var stack = [URL(fileURLWithPath: directory)]
    // variables to track duplicate files
    var (seen, dup) = (Set<String>(), Set<String>())
    while !stack.isEmpty {
        let cur = stack.removeLast()
        // get contents of cur directory url,
        // if it is not a directory, continue
        guard let files = try? fm.contentsOfDirectory(
            at: cur,
            includingPropertiesForKeys: nil
        ) else { continue }

        files.forEach {
            // for files in current directory, check:
            // if directory, push it onto the stack
            // else, check for duplicate file name
            if $0.hasDirectoryPath {
                stack.append($0)
                return
            }
            let name = $0.lastPathComponent
            if seen.contains(name) { dup.insert(name) }
            else { seen.insert(name) } 
        }
    }
    return Array(dup)
}

// test cases
print(challenge33(in: "directory"))
```

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge33(in directory: String) -> [String] {
    let fm = FileManager.default
    let url = URL(fileURLWithPath: directory)
    guard let files = fm.enumerator(
        at: url, 
        includingPropertiesForKeys: nil
    ) else { return [] }

    var (seen, dup) = (Set<String>(), Set<String>())
    for case let file as URL in files {
        if file.hasDirectoryPath { continue }
        let name = file.lastPathComponent
        if seen.contains(name) { dup.insert(name) }
        else { seen.insert(name) }
    }
    return Array(dup)
}

// test cases
print(challenge33(in: "directory"))
```
