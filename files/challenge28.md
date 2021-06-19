# Challenge 28

## Log a message

> **Difficulty**: Easy

Write a logging function that accepts accepts a path to a log file on disk as well as a new log message. Your function should open the log file (or create it if it does not already exist), then append the new message to the log along with the current time and date.

> **Tip**: It’s important that you add line breaks along with each message, otherwise the log will just become jumbled.

### Sample input and output

- If the file does not exist, running your function should create it and save the new message.
- If it does exist, running your function should load the existing content and append the message to the end, along with suitable line breaking.

After running the test cases, the following should be the contents of your log file:

``` text
[DATE TIME]: Challenge 28: Test #1 - passed
[DATE TIME]: Challenge 28: Test #2 - passed
[DATE TIME]: Challenge 28: Test #3 - passed
```

### Stub

``` swift
import Foundation

func challenge28(log message: String, to file: String) {
    // your code goes here
}

// test cases
challenge28(log: "Challenge 28: Test #2 - passed", to: "log.txt")
challenge28(log: "Challenge 28: Test #3 - passed", to: "log.txt")
challenge28(log: "Challenge 28: Test #1 - passed", to: "log.txt")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. I think it would be reasonable to use `contentsOfFile` to load the existing log file into a string.
2. You can use `try?` and *nil coalescing* to provide a default value if the existing log file doesn’t exist.
3. How you format the date and time for each message will be interesting, but don’t forget *KISS: Keep It Simple, Stupid*.
4. What should happen if you can’t write the log file? This wasn’t specified in the challenge description, so you get to use some initiative.

### Solution 1

``` swift
import Foundation

func challenge28(log message: String, to file: String) {
    var data = (try? String(contentsOfFile: file)) ?? ""
    data += ("\(Date()): \(message)\n")
    do {
        try data.write(toFile: file, atomically: true, encoding: String.Encoding.utf8)
    } catch {
        print("failed to log the message: \(error.localizedDescription)")
    }
}

// test cases
challenge28(log: "Challenge 28: Test #2 - passed", to: "log.txt")
challenge28(log: "Challenge 28: Test #3 - passed", to: "log.txt")
challenge28(log: "Challenge 28: Test #1 - passed", to: "log.txt")
```
