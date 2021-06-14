# Challenge 22

## Binary reverse

> **Difficulty**: Tricky

Create a function that accepts an unsigned 8-bit integer and returns its binary reverse, padded so that it holds precisely eight binary digits.

> **Tip**: When you get the binary representation of a number, Swift will always use as few bits as possible – make sure you pad to eight binary digits before reversing.

### Sample input and output

- The number `32` is `100000` in binary, and padded to eight binary digits that’s `00100000`. Reversing that binary sequence gives `00000100`, which is `4`. So, when given the input `32` your function should return `4`.
- The number `41` is `101001` in binary, and padded to eight binary digits that `00101001`. Reversing that binary sequence gives `10010100`, which is `148`. So, when given the input `41` your function should return `148`.
- It should go without saying that your function should be symmetrical: when fed `4` it should return `32`, and when fed `148` it should return `41`.

### Stub

``` swift
import Foundation

func challenge22(num: UInt8) -> UInt8 {
    // your code goes here
    return 0
}

// test cases
assert(challenge22(num: 32) == 4, "Challenge 22: Test #1 - failed")
assert(challenge22(num: 41) == 148, "Challenge 22: Test #2 - failed")
assert(challenge22(num: 4) == 32, "Challenge 22: Test #3 - failed")
assert(challenge22(num: 148) == 41, "Challenge 22: Test #4 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can get the binary representation of an integer using `String(someNumber, radix: 2)`.
2. You can get the decimal integer equivalent of a string containing binary using `Int(someString, radix: 2)` – but be warned that will given you an optional integer.
3. To pad the input number’s binary representation so that it holds eight digits, use the `String(repeating:count:)` initializer.
4. You can reverse a character array then create a new string from it.

### Solution 1

``` swift
import Foundation

func challenge22(num: UInt8) -> UInt8 {
    // example num = 32, binary = "00000000"
    var binary = [Character](repeating: "0", count: 8)
    // binary repr of num = "100000"
    // reversed = "000001"
    // binary = "00000100"
    for (i, ch) in String(num, radix: 2).reversed().enumerated() {
        binary[i] = ch
    }
    // result = 4
    return UInt8(String(binary), radix: 2)!
}

// test cases
assert(challenge22(num: 32) == 4, "Challenge 22: Test #1 - failed")
assert(challenge22(num: 41) == 148, "Challenge 22: Test #2 - failed")
assert(challenge22(num: 4) == 32, "Challenge 22: Test #3 - failed")
assert(challenge22(num: 148) == 41, "Challenge 22: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`

### Solution 2 - Paul Hudson

``` swift
import Foundation

func challenge22(num: UInt8) -> UInt8 {
    let bin = String(num, radix: 2)
    let pad = 8 - bin.count
    let paddedBin = String(repeating: "0", count: pad) + bin
    let reversedBin = String(paddedBin.reversed())
    return UInt8(reversedBin, radix: 2)!
}

// test cases
assert(challenge22(num: 32) == 4, "Challenge 22: Test #1 - failed")
assert(challenge22(num: 41) == 148, "Challenge 22: Test #2 - failed")
assert(challenge22(num: 4) == 32, "Challenge 22: Test #3 - failed")
assert(challenge22(num: 148) == 41, "Challenge 22: Test #4 - failed")
```

> **Time Complexity** (worst case): `O(n)`
