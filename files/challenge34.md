# Challenge 34

## Find executables

> **Difficulty**: Tricky

Write a function that accepts the name of a directory to scan, and returns an array containing the name of any executable files in there.

### Sample input and output

- If *directory/a* exists and is executable, `“a”` should be in the array you return.
- If *directory/subdirectory/a* exists and is executable, it should not be in the array you return; only return files in the directory itself, not its subdirectories.
- If there are no executable files, return an empty array.

### Stub

``` swift
import Foundation

func challenge34(in directory: String) -> [String] {
    // your code goes here
    return []
}

// test cases
print(challenge34(in: ""))
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Make sure you create the test directories as shown in the sample input/output. You can use `touch a` to create a file called `“a”`, then `chmod a+x a` to mark it executable.
2. You probably want to use the `isExecutableFile()` method of `FileManager`.
3. If you don’t create at least one subdirectory to test with, your tests will be incomplete.
4. Directories are considered executable for historical reasons. If they appear in your return array, you won’t have passed the challenge.

### Solution 1

``` swift
import Foundation

func challenge34(in directory: String) -> [String] {
    let fm = FileManager.default
    let url = URL(fileURLWithPath: directory)
    guard let contents = try? fm.contentsOfDirectory(
        at: url,
        includingPropertiesForKeys: nil
    ) else { return [] }

    var executables = [String]()
    for obj in contents {
        if obj.hasDirectoryPath { continue }
        if fm.isExecutableFile(atPath: obj.path) {
            executables.append(obj.lastPathComponent)
        }
    }
    return executables
}

// test cases
print(challenge34(in: ""))
```
