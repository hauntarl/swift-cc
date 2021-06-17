# Challenge 44

## Linked list mid-point

> **Difficulty**: Easy

Extend your linked list class with a new method that returns the node at the mid point of the
linked list using no more than one loop.

> **Tip**: If the linked list contains an even number of items, returning the one before or the one after the center is acceptable.

### Sample input and output

- If the linked list contains `1, 2, 3, 4, 5`, your method should return `3`.
- If the linked list contains `1, 2, 3, 4`, your method may return `2 or 3`.
- If the linked list contains the *English alphabets*, your method may return `M or N`.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert(LinkedList(from: [1, 2, 3, 4, 5]).mid == 3, "Test #1 - failed")
assert(LinkedList(from: [1, 2, 3, 4]).mid == 3, "Test #2 - failed")
assert(LinkedList(from: Array("abcdefghijklmnopqrstuvwxyz")).mid == "n", "Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. It’s easy to solve this in two passes, but only fractionally harder to solve it in one.
2. If you use *fast enumeration* – for i in items – you move over one item at a time. Can you think of a way of moving over more than one item?
3. Once you pull out two items at the same time, you can make them move at different speeds through the list.
4. If you move pointer A through the list one item at a time, and pointer B through the list two items at a time, by the time pointer B reaches the end where will pointer A be?

### Solution 1

``` swift
import Foundation

private final class Node<Element> {
    var data: Element
    var next: Node<Element>!
    
    init(_ data: Element) {
        self.data = data
        self.next = nil
    }
}

final class LinkedList<Element> {
    private var head: Node<Element>!
    private var tail: Node<Element>!
    
    var mid: Element? {
        if head == nil { return nil }
        
        var fast: Node<Element>! = head
        var slow: Node<Element>! = head
        while fast != nil && fast.next != nil {
            slow = slow.next
            fast = fast.next.next
        }
        return slow.data
    }

    init() {}
    
    init(from list: [Element]) {
        if list.isEmpty { return }
        for data in list { append(data) } 
    }
    
    func append(_ data: Element) {
        let node = Node(data)
        if tail != nil {
            tail.next = node
            tail = tail.next
        } else {
            head = node
            tail = head
        }
    }
}

// test cases
assert(LinkedList(from: [1, 2, 3, 4, 5]).mid == 3, "Test #1 - failed")
assert(LinkedList(from: [1, 2, 3, 4]).mid == 3, "Test #2 - failed")
assert(LinkedList(from: Array("abcdefghijklmnopqrstuvwxyz")).mid == "n", "Test #3 - failed")
```

> **Time Complexity** (worst case): `O(n/2)`
