# Challenge 53

## Linked lists with a loop

> **Difficulty**: Taxing

Someone used the linked list you made previously, but they accidentally made one of the items link back to an earlier part of the list. As a result, the list can’t be traversed properly because it loops infinitely.

Your job is to write a function that accepts your linked list as its parameter, and returns the node at the start of the loop, i.e. the one that is linked back to.

### Stub

``` swift
import Foundation

// your code goes here

// build test 1 - has a loop
/*
    Visualization:
    - total 6 nodes in linked list
    - n2 = loop back node

    n1(head) -- n2 -- n3 -- n4
                |            |
                ------n6 -- n5
*/
var list1 = LinkedList<UInt32>()
var prev1: Node<UInt32>! = nil
var loop: Node<UInt32>! = nil
var point = Int.random(in: 1...1000)
for i in 1...1000 {
    let node = Node(UInt32.random(in: 0...UInt32.max))

    if i == point { loop = node }
    
    if prev1 != nil { prev1.next = node }
    else { list1.head = node }
    prev1 = node
}
prev1.next = loop
// ------------

// build test 2 - no loop
var list2 = LinkedList<Character>()
var prev2: Node<Character>! = nil
for ch in "abcdefghijklmnopqrstuvwxyz" {
    let node = Node(ch)
    
    if prev2 != nil { prev2.next = node }
    else { list2.head = node }
    prev2 = node
}
// ------------

// test cases
assert(list1.findLoopNode()! == loop, "Challenge 53: Test #1 - failed")
assert(list2.findLoopNode() == nil, "Challenge 53: Test #2 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. There are two ways to solve this: using a set or using mathematics. You could also use an array, but only if you had no regard at all for performance.
2. If you take the set approach you will need to conform to `Hashable`, which in turn implies `Equatable`.
3. You can also solve this problem with pure mathematics, which is both significantly faster and more memory efficient. If you ever learned to do *tortoise and hare loop detection*, now is your chance to feel smug!

### Solution 1

``` swift
import Foundation

let generateID: () -> UInt = {
    var id: UInt = 0
    return {
        if id == UInt.max { id = 0 }
        id += 1
        return id
    }
}()

final class Node<Element>: Equatable {
    var data: Element
    var next: Node<Element>!
    let id: UInt
    
    init(_ data: Element) {
        self.data = data
        self.next = nil
        self.id = generateID()
    }
    
    static func ==(lhs: Node<Element>, rhs: Node<Element>) -> Bool {
        lhs.id == rhs.id
    }
}

final class LinkedList<Element> {
    var head: Node<Element>!

    init() {}
    
    func traverse() {
        var curr: Node<Element>! = head
        while curr != nil {
            print(curr.data, terminator: " ")
            curr = curr.next
        }
        print()
    }

    func findLoopNode() -> Node<Element>? {
        var slow: Node<Element>! = head
        var fast: Node<Element>! = head
        while fast != nil && fast.next != nil {
            slow = slow.next
            fast = fast.next.next
            if slow == fast { break }
        }
        if fast == nil || fast.next == nil { return nil }
        
        slow = head
        while slow != fast {
            slow = slow.next
            fast = fast.next
        }
        return slow
    }
}

// build test 1 - has a loop
/*
    Visualization:
    - total 6 nodes in linked list
    - n2 = loop back node

    n1(head) -- n2 -- n3 -- n4
                |            |
                ------n6 -- n5
*/
var list1 = LinkedList<UInt32>()
var prev1: Node<UInt32>! = nil
var loop: Node<UInt32>! = nil
var point = Int.random(in: 1...1000)
for i in 1...1000 {
    let node = Node(UInt32.random(in: 0...UInt32.max))

    if i == point { loop = node }
    
    if prev1 != nil { prev1.next = node }
    else { list1.head = node }
    prev1 = node
}
prev1.next = loop
// ------------

// build test 2 - no loop
var list2 = LinkedList<Character>()
var prev2: Node<Character>! = nil
for ch in "abcdefghijklmnopqrstuvwxyz" {
    let node = Node(ch)
    
    if prev2 != nil { prev2.next = node }
    else { list2.head = node }
    prev2 = node
}
// ------------

// test cases
assert(list1.findLoopNode()! == loop, "Challenge 53: Test #1 - failed")
assert(list2.findLoopNode() == nil, "Challenge 53: Test #2 - failed")
```

> **Time Complexity** (worst case): `O(n)`
