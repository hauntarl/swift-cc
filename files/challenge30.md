# Challenge 30

## New JPEGs

> **Difficulty**: Easy

Write a function that accepts a path to a directory and returns an array of all JPEGs that have been created in the last 48 hours.

> **Tip 1**: For the purpose of this task, just looking for “.jpg” and “.jpeg” file extensions is sufficient.
>
> **Tip 2**: For this challenge, assume time is regular and constant, i.e. the user has not changed their timezone or moved into or out from daylight savings.
>
> **Tip 3**: Use the terminal command touch -t YYYYMMDDHHMM somefile.jpg to adjust the creation time of a file, e.g. touch -t 201612250101.

### Sample input and output

- If your directory contains three *JPEGs* older than *48 hours* and three newer, your function should return the names of the three newer.

### Stub

``` swift
import Foundation

func challenge30(in directory: String) -> [String] {
    // your code goes here
}

// test cases
print(challenge30())
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Use the `contentsOfDirectory()` method of `FileManager` to pull out the list of files in your target directory.
2. You can compare two dates directly using `>`.
3. You can read the attributes of a file using the `attributesOfItem()` method on `FileManager`, and you’ll want to read the `FileAttributeKey.creationDate` from that dictionary.

### Solution 1

``` swift
import Foundation

let filterDate = Date(timeIntervalSinceNow: -60 * 60 * 48)

func challenge30(in directory: String) -> [String] {
    let fm = FileManager.default
    let url = URL(fileURLWithPath: directory)

    guard let files = try? fm.contentsOfDirectory(
        at: url,
        includingPropertiesForKeys: nil
    ) else { return [] }

    var jpegs = [String]()
    for file in files {
        let ext = file.pathExtension
        if ext == "jpg" || ext == "jpeg" {
            guard let attr = try? fm.attributesOfItem(atPath: file.path) else {
                continue
            }
            print(attr[.creationDate])
            guard let fdate = attr[.creationDate] as? Date  else {
                continue
            }
            if fdate > filterDate { jpegs.append(file.lastPathComponent) }
        }
    }
    return jpegs
}

// test cases
print(challenge30(in: ""))
```
