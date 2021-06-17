# Challenge 52

## Sum an array of numbers

> **Difficulty**: Taxing

Write one function that sums an array of numbers. The array might contain all integers, all doubles, or all floats.

> **Tip**: If you think this challenge is easy, you’re either a hardened Swift pro or you’ve underestimated the problem.

### Sample input and output

- The code `challenge52(numbers: [1, 2, 3])` should return `6`.
- The code `challenge52(numbers: [1.0, 2.0, 3.0])` should return `6.0`.
- The code `challenge52(numbers: Array<Float>([1.0, 2.0, 3.0]))` should return `6.0`.

### Stub

``` swift
import Foundation

func challenge52() {
    // your code goes here
    return
}

// test cases
assert(challenge52(numbers: [1, 2, 3]) == 6, "Challenge 52: Test #1 - failed")
assert(challenge52(numbers: [1.0, 2.0, 3.0]) == 6.0, "Challenge 52: Test #2 - failed")
assert(challenge52(numbers: Array<Float>([1.0, 2.0, 3.0])) == 6.0, "Challenge 52: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. If this were just about counting integers this would definitely be an easy grade.
2. This function needs to work with multiple data types, so you’ll need to use generics with a constraint.
3. There’s no built-in protocol that covers *integers, floats, and doubles*, so you’ll need to create your own then extend `Int`, `Float`, and `Double` using it.
4. Your protocol needs to be able to initialize itself with an empty value, and add two instances of itself.
5. Once you have everything in place, you can solve this challenge functionally.

### Solution 1

``` swift
import Foundation

protocol Numeric {
    init()
    static func +(lhs: Self, rhs: Self) -> Self
}

extension Int: Numeric {}
extension Double: Numeric {}
extension Float: Numeric {}

func challenge52<T: Numeric>(numbers: [T]) -> T { numbers.reduce(T(), +) }

// test cases
assert(challenge52(numbers: [1, 2, 3]) == 6, "Challenge 52: Test #1 - failed")
assert(challenge52(numbers: [1.0, 2.0, 3.0]) == 6.0, "Challenge 52: Test #2 - failed")
assert(challenge52(numbers: Array<Float>([1.0, 2.0, 3.0])) == 6.0, "Challenge 52: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n)`
