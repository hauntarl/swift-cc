# Challenge 48

## Implement a deque data structure

> **Difficulty**: Tricky

Create a new data type that models a double-ended queue using generics, or deque. You should be able to push items to the front or back, pop them from the front or back, and get the number of items.

> **Tip**: It’s pronounced like “deck”

### Sample input and output

Once your data structure has been created, following code should compile and run cleanly:

### Stub

``` swift
import Foundation

// your code goes here

var numbers = deque<Int>()
numbers.pushBack(5)
numbers.pushBack(8)
numbers.pushBack(3)
assert(numbers.count == 3)
assert(numbers.popFront()! == 5)
assert(numbers.popBack()! == 3)
assert(numbers.popFront()! == 8)
assert(numbers.popBack() == nil)
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Use an internal array for your data.
2. If you used a class for this, expect to be questioned carefully as to why you didn’t choose a struct.
3. You’ll need to declare your whole data type as being generic, e.g. `struct deque<T> {`.
4. The `popBack()` and `popFront()` method should return optionals, because the deque might be empty.
5. You’ll need to mark your methods as `mutating`.
6. Make sure count is a property rather than a method. Something like `var count: Int { return array.count }` ought to do it.

### Solution 1

``` swift
import Foundation

struct deque<T> {
    private var array = [T]()
    
    var count: Int { array.count }
    
    init() {}
    
    mutating func pushBack(_ data: T) { array.append(data) }

    mutating func popFront() -> T? { 
        if array.isEmpty { return nil }
        return array.removeFirst()
    }
    
    mutating func popBack() -> T? { array.popLast() }
}

var numbers = deque<Int>()
numbers.pushBack(5)
numbers.pushBack(8)
numbers.pushBack(3)
assert(numbers.count == 3)
assert(numbers.popFront()! == 5)
assert(numbers.popBack()! == 3)
assert(numbers.popFront()! == 8)
assert(numbers.popBack() == nil)
```

> **Time Complexity** (worst case): `O(n)`
