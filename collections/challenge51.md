# Challenge 51

## Reversing linked lists

> **Difficulty**: Easy

Expand your code from challenge 43 so that it has a reversed() method that returns a copy of itself in reverse.

> **Tip**: Don’t cheat! It is not a solution to this problem just to reverse the alphabet letters before you create your linked list. Create the linked list alphabetically, then write code to reverse it.

### Sample input and output

- When you call `reversed()` on your alphabet list, running `traverse()` on the return value should print the English alphabet printed to the screen in reverse, i.e. *“z y x … d b c a”*.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
let alphabets = Array("abcdefghijklmnopqrstuvwxyz")
let list = LinkedList(from: alphabets)
let reverse = list.reversed()
list.traverse()
reverse.traverse()
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Most of the work is just producing a copy of the linked list.
2. Having to work on a copy makes this a little more interesting.
3. You could create two methods: one for copying, and one for reversing a copy in place. If you do this, please think carefully about *Swift’s naming conventions*!
4. You need to create a `newNext` variable that starts as `nil`. Then traverse the full list, pull out its next value, then change the *current node’s* next property to be `newNext`. You can then continue on to whatever node was in next, and repeat until the end of the list is reached.

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
    
    func traverse() {
        var curr: Node<Element>! = head
        while curr != nil {
            print(curr.data, terminator: " ")
            curr = curr.next
        }
        print()
    }
    
    func copy() -> LinkedList<Element> {
        let copy = LinkedList<Element>()
        var curr: Node<Element>! = head
        while curr != nil {
            copy.append(curr.data)
            curr = curr.next
        }
        return copy
    }
    
    func reverse() {
        guard head != nil else { return }
        
        tail = head
        var prev: Node<Element>!
        var curr: Node<Element>!
        var next: Node<Element>! = head
        repeat {
            prev = curr
            curr = next
            next = next.next
            curr.next = prev
        } while next != nil
        head = curr
    }
    
    func reversed() -> LinkedList<Element> {
        let copy = self.copy()
        copy.reverse()
        return copy
    }
}

let alphabets = Array("abcdefghijklmnopqrstuvwxyz")
let list = LinkedList(from: alphabets)
let reverse = list.reversed()
list.traverse()
reverse.traverse()
```

> **Time Complexity** (worst case): `O(n)`
