# Challenge 43

## Linked lists

> **Difficulty**: Easy

Create a linked list of lowercase English alphabet letters, along with a method that traverses all nodes and prints their letters on a single line separated by spaces.

> **Tip 1**: This is several problems in one. First, create a linked list data structure, which itself is really two things. Second, use your linked list to create the alphabet. Third, write a method traverses all nodes and prints their letters.
>
> **Tip 2**: You should use a class for this. Yes, really.
>
> **Tip 3**: Once you complete your solution, keep a copy of the code – you’ll need it for future challenges!

### Sample input and output

- The output of your code should be the English alphabet printed to the screen, i.e. *“a b c d … x y z”*.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
let alphabets = Array("abcdefghijklmnopqrstuvwxyz")

// using 1st constructor
let list1 = LinkedList<Character>()
for ch in alphabets { list1.append(ch) }
list1.traverse() // a b c d e f g h i j k l m n o p q r s t u v w x y z 
print(list1.length) // 26

// using 2nd constructor
let list2 = LinkedList(from: alphabets)
list2.traverse() // a b c d e f g h i j k l m n o p q r s t u v w x y z 
print(list2.length) // 26

// using insert operation
let list3 = LinkedList<Character>()
for ch in alphabets { list3.insert(ch, at: list3.length) }
list3.traverse() // a b c d e f g h i j k l m n o p q r s t u v w x y z 
print(list3.length) // 26
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. If your first instinct was to create your new data types as a struct, it shows you’re a sound Swift developer. Sadly, I’m afraid that approach won’t work here because *structs can’t have stored properties that reference themselves*.
2. Your second instinct might be to use an enum. This makes creation tricksy because you would need to change the associated value after creating the enum.
3. Even though this challenge uses alphabet letters, aim to make your class *generic* – it shows smart forward thinking, and is only fractionally harder than using a specific data type.
4. There are lots of hacky ways to loop over the alphabet. The only sensible way is to use `"abcdefghijklmnopqrstuvwxyz"` – it’s not hard to write, is self-documenting, and quite safe.
5. You should create *two data types*: one for a *node*, which contains its character and link to the next node in the list, and one for the overall *linked list*, which contains a property for the first node in the list as well as the print method.
6. The `print()` function has a `terminator` parameter.

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
    private var size = 0
    
    var length: Int { size }
    
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
        size += 1
    }
    
    func insert(_ data: Element, at index: Int = 0) {
        precondition(index >= 0, "index can't be negative")
    
        if size == 0 || index >= size { 
            append(data) 
            return
        }
        
        let node = Node(data)
        if index == 0 {    
            node.next = head
            head = node
        } else {
            var curr: Node<Element>! = head
            var prev: Node<Element>! = nil
            for _ in 1...index {
                prev = curr
                curr = curr.next 
            }
            if prev != nil { prev.next = node }
            node.next = curr
        }
        size += 1
    }
    
    func traverse() {
        var curr: Node<Element>! = head
        while curr != nil {
            print(curr.data, terminator: " ")
            curr = curr.next
        }
        print()
    }
}

// test cases
let alphabets = Array("abcdefghijklmnopqrstuvwxyz")

// using 1st constructor
let list1 = LinkedList<Character>()
for ch in alphabets { list1.append(ch) }
list1.traverse() // a b c d e f g h i j k l m n o p q r s t u v w x y z 
print(list1.length) // 26

// using 2nd constructor
let list2 = LinkedList(from: alphabets)
list2.traverse() // a b c d e f g h i j k l m n o p q r s t u v w x y z 
print(list2.length) // 26

// using insert operation
let list3 = LinkedList<Character>()
for ch in alphabets { list3.insert(ch, at: list3.length) }
list3.traverse() // a b c d e f g h i j k l m n o p q r s t u v w x y z 
print(list3.length) // 26
```

> **Time Complexity** (worst case): `O(n)`
