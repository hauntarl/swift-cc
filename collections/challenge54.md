# Challenge 54

## Binary search trees

> **Difficulty**: Taxing

Create a binary search tree data structure that can be initialized from an unordered array of comparable values, then write a method that returns whether the tree is balanced.

> **Tip 1**: There is more than one description of a balanced binary tree. For the purpose of this challenge, a binary tree is considered balanced when the height of both subtrees for every node differs by no more than 1.
>
> **Tip 2**: Once you complete this challenge, keep your code around because you’ll need it in the 45th one.

### Sample input and output

The following values should create balanced trees:

- `[2, 1, 3]`
- `[5, 1, 7, 6, 2, 1, 9]`
- `[5, 1, 7, 6, 2, 1, 9, 1]`
- `[5, 1, 7, 6, 2, 1, 9, 1, 3]`
- `[50, 25, 100, 26, 101, 24, 99]`
- `["k", "t", "d", "a", "z", "m", "f"]`
- `[1]`
- `[Character]()`

The following values should not create balanced trees:

- `[1, 2, 3, 4, 5]`
- `[10, 5, 4, 3, 2, 1, 11, 12, 13, 14, 15]`
- `["f", "d", "c", "e", "a", "b"]`

### Stub

``` swift
import Foundation

// test cases
assert(BST([2, 1, 3]).isBalanced == true, "Challenge 54: Test #1 - failed")
assert(BST([5, 1, 7, 6, 2, 1, 9]).isBalanced == true, "Challenge 54: Test #2 - failed")
assert(BST([5, 1, 7, 6, 2, 1, 9, 1]).isBalanced == true, "Challenge 54: Test #3 - failed")
assert(BST([5, 1, 7, 6, 2, 1, 9, 1, 3]).isBalanced == true, "Challenge 54: Test #4 - failed")
assert(BST([50, 25, 100, 26, 101, 24, 99]).isBalanced == true, "Challenge 54: Test #5 - failed")
assert(BST(["k", "t", "d", "a", "z", "m", "f"]).isBalanced == true, "Challenge 54: Test #6 - failed")
assert(BST([1]).isBalanced == true, "Challenge 54: Test #7 - failed")
assert(BST([Character]()).isBalanced == true, "Challenge 54: Test #8 - failed")

assert(BST([1, 2, 3, 4, 5]).isBalanced == false, "Challenge 54: Test #9 - failed")
assert(BST([10, 5, 4, 3, 2, 1, 11, 12, 13, 14, 15]).isBalanced == false, "Challenge 54: Test #10 - failed")
assert(BST(["f", "d", "c", "e", "a", "b"]).isBalanced == false, "Challenge 54: Test #11 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You need to create a *binary search tree* rather than a plain *binary tree*. This means inserting nodes into the tree based on whether they are less than or equal *(left)* or greater than *(right)* their parent.
2. You should make your data types use a generic value that conforms to `Comparable`.
3. Each nodes should have a value, plus left and right optional nodes.
4. To find the correct place for each array item, start at the top of your tree then keep moving left or right until you find `nil` – that’s your place
5. You might find it useful to make your binary tree type conform to `CustomStringConvertible` so you can add a custom `var description: String` that prints the contents of your tree.
6. Checking a binary tree is balanced can be done by recursively comparing the *minimum depth* of both sides of a node against the *maximum depth* of both sides of a node. The tree can be considered balanced if the two values differ by no more than 1.

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
    static func height(from root: Node<Element>!) -> Int {
        if root == nil { return 0 }
        return 1 + max(height(from: root.lnode), height(from: root.rnode))
    }
    
    static func isBalanced(from root: Node<Element>!) -> (balanced: Bool, height: Int) {
        if root == nil { return (true, 0) }
        
        // check if left subtree is balanced, also calc. height for it
        let lst = isBalanced(from: root.lnode)
        if !lst.balanced { return (false, 0) }
        
        // check if right subtree is balanced, also calc. height for it
        let rst = isBalanced(from: root.rnode)
        if !rst.balanced { return (false, 0) }
        
        // check if current subtree is balanced, include calc. for height in the 
        // same function to avoid multiple recursive calls and optimize solution
        return (abs(lst.height - rst.height) < 2, 1 + max(lst.height, rst.height))
    }

    private var root: Node<Element>!
    
    var height: Int { BST.height(from: root) }
    var isBalanced: Bool { BST.isBalanced(from: root).0 }
    
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
}

// test cases
assert(BST([2, 1, 3]).isBalanced == true, "Challenge 54: Test #1 - failed")
assert(BST([5, 1, 7, 6, 2, 1, 9]).isBalanced == true, "Challenge 54: Test #2 - failed")
assert(BST([5, 1, 7, 6, 2, 1, 9, 1]).isBalanced == true, "Challenge 54: Test #3 - failed")
assert(BST([5, 1, 7, 6, 2, 1, 9, 1, 3]).isBalanced == true, "Challenge 54: Test #4 - failed")
assert(BST([50, 25, 100, 26, 101, 24, 99]).isBalanced == true, "Challenge 54: Test #5 - failed")
assert(BST(["k", "t", "d", "a", "z", "m", "f"]).isBalanced == true, "Challenge 54: Test #6 - failed")
assert(BST([1]).isBalanced == true, "Challenge 54: Test #7 - failed")
assert(BST([Character]()).isBalanced == true, "Challenge 54: Test #8 - failed")

assert(BST([1, 2, 3, 4, 5]).isBalanced == false, "Challenge 54: Test #9 - failed")
assert(BST([10, 5, 4, 3, 2, 1, 11, 12, 13, 14, 15]).isBalanced == false, "Challenge 54: Test #10 - failed")
assert(BST(["f", "d", "c", "e", "a", "b"]).isBalanced == false, "Challenge 54: Test #11 - failed")
```

> **Time Complexity** (worst case): `O(h + n)` - creating BST + checking if balanced, where h = height of BST
