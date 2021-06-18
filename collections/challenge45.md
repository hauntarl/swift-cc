# Challenge 45

## Traversing the tree

> **Difficulty**: Easy
>
> **NOTE**: this challenge cannot be attempted until you have first completed challenge 54.

Write a new method for your binary search tree that traverses the tree in order, running a closure on each node.

> **Tip**: Traversing a node in order means visiting its left value, then visiting its own value, then visiting its right value.

### Stub

``` swift
import Foundation

// test cases
var result = [Int]()
BST([50, 25, 100, 26, 101, 24, 99]).traverse { result.append($0) }

var string = ""
BST([5, 1, 7, 6, 2, 1, 9, 1, 3]).traverse { string += "\($0) " }

var sum = 0
BST([10, 5, 4, 3, 2, 1, 11, 12, 13, 14, 15]).traverse { sum += $0 }

assert(result == [24, 25, 26, 50, 99, 100, 101], "Challenge 45: Test #1 - failed")
assert(string == "1 1 1 2 3 5 6 7 9 ", "Challenge 45: Test #2 - failed")
assert(sum == 90, "Challenge 45: Test #3 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Your entire function can be just three lines of code. Yes, it really is that easy – hurray for recursion!
2. You can write this method for the binary tree class or for its nodes; it really doesn’t matter. I chose to write it for the nodes so that I can print partial trees.
3. Make sure it accepts a closure parameter that itself accepts one parameter (your `Node<T>` equivalent) and returns void.
4. Remember the left and/or right node may not exist.

### Solution 1

``` swift
import Foundation

final class Node<Element: Comparable>: Comparable {
    var data: Element
    var lnode: Node<Element>!
    var rnode: Node<Element>!
    
    static func <(lhs: Node<Element>, rhs: Node<Element>) -> Bool {
        lhs.data < rhs.data
    }
    
    static func ==(lhs: Node<Element>, rhs: Node<Element>) -> Bool {
        lhs.data == rhs.data
    }
    
    init(_ data: Element) { self.data = data }
}

class BST<Element: Comparable> {
    private var root: Node<Element>!
    
    init(_ list: [Element]) {
        if list.isEmpty { return }
        
        for item in list {
            let node = Node(item)
            var curr: Node<Element>! = root
            var prev: Node<Element>! = nil
            
            while curr != nil {
                prev = curr
                curr = node > curr ? curr.rnode : curr.lnode
            }
            switch prev {
            case let .some(prev) where node > prev: prev.rnode = node
            case let .some(prev): prev.lnode = node
            default: root = node
            }
        }
    }
    
    func traverse(_ callback: (Element) -> Void) {
        if root == nil { return }
        
        var stack = [Node<Element>]()
        var curr: Node<Element>! = root
        while curr != nil {
            stack.append(curr)
            curr = curr.lnode
        }
        
        while !stack.isEmpty {
            curr = stack.removeLast()
            callback(curr.data)

            curr = curr.rnode
            while curr != nil {
                stack.append(curr)
                curr = curr.lnode
            }
        }
    }
}

// test cases
var result = [Int]()
BST([50, 25, 100, 26, 101, 24, 99]).traverse { result.append($0) }

var string = ""
BST([5, 1, 7, 6, 2, 1, 9, 1, 3]).traverse { string += "\($0) " }

var sum = 0
BST([10, 5, 4, 3, 2, 1, 11, 12, 13, 14, 15]).traverse { sum += $0 }

assert(result == [24, 25, 26, 50, 99, 100, 101], "Challenge 45: Test #1 - failed")
assert(string == "1 1 1 2 3 5 6 7 9 ", "Challenge 45: Test #2 - failed")
assert(sum == 90, "Challenge 45: Test #3 - failed")
```

> **Time Complexity** (worst case): `O(h + n)` - creating BST + traversing, where h = height of BST
