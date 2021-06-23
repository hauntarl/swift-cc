# Challenge 61

## Find prime numbers

> **Difficulty**: Tricky

Write a function that returns an array of prime numbers from 2 up to but excluding N, taking care to be as efficient as possible.

> **Tip**: Calculating primes is easy. Calculating primes efficiently is not. Take care!

### Sample input and output

- The code `challenge61(upTo: 10)` should return *2, 3, 5, 7*.
- The code `challenge61(upTo: 11)` should return *2, 3, 5, 7*; remember to exclude the upper bound.
- The code `challenge61(upTo: 12)` should return *2, 3, 5, 7, 11*.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert(challenge61(upto: 10) == [2, 3, 5, 7], "Challenge 61: Test #1 - failed")
assert(challenge61(upto: 11) == [2, 3, 5, 7], "Challenge 61: Test #2 - failed")
assert(challenge61(upto: 12) == [2, 3, 5, 7, 11], "Challenge 61: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Writing code to find whether one number is prime or not is very different to writing code to find all prime numbers – there’s a reason this is in the algorithms chapter.
2. When given a number, you decide whether it’s prime by checking whether it has any factors. When given a range of numbers, you want to take the opposite approach: assume all numbers are prime, then remove numbers that are composites by multiplying primes.
3. This is known as the *Sieve of Eratosthenes*: take the number 2, then mark all multiples of 2 as being not prime. Then take the number 3 and repeat. Then 5 (no need to check 4; that’s a multiple of 2), then 7 (no need to check 6; that’s a multiple of 3), and so on. What remains must be prime.
4. Once you have an array containing which numbers are prime and which are not, you just need to extract the numbers that are prime and return them.

### Solution 1 - Generic procedural algorithm

``` swift
import Foundation

func challenge61(upto limit: Int) -> [Int] {
    if limit < 3 { return [] }

    var numbers = [2]
    outer: for cur in 3..<limit {
        let root = Int(sqrt(Double(cur)))
        inner: for prime in numbers {
            if prime > root { break inner }
            if cur % prime == 0 { continue outer }
        }
        numbers.append(cur)
    }
    return numbers
}

// test cases
assert(challenge61(upto: 10) == [2, 3, 5, 7], "Challenge 61: Test #1 - failed")
assert(challenge61(upto: 11) == [2, 3, 5, 7], "Challenge 61: Test #2 - failed")
assert(challenge61(upto: 12) == [2, 3, 5, 7, 11], "Challenge 61: Test #3 - failed")
```

### Solution 2 - Paul Hudson (Faster and more optimized)

``` swift
import Foundation

func challenge61(upto limit: Int) -> [Int] {
    if limit < 3 { return [] }

    var sieve = [Bool](repeating: true, count: limit)
    (sieve[0], sieve[1]) = (false, false)
    for cur in 2..<limit {
        if !sieve[cur] { continue }

        for mul in stride(from: cur * cur, to: limit, by: cur) {
            sieve[mul] = false
        }
    }
    return sieve
        .enumerated()
        .compactMap { $0.element ? $0.offset : nil }
}

// test cases
assert(challenge61(upto: 10) == [2, 3, 5, 7], "Challenge 61: Test #1 - failed")
assert(challenge61(upto: 11) == [2, 3, 5, 7], "Challenge 61: Test #2 - failed")
assert(challenge61(upto: 12) == [2, 3, 5, 7, 11], "Challenge 61: Test #3 - failed")
```
