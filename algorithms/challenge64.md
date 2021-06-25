# Challenge 64

## N Queens

> **Difficulty**: Taxing

There are M different ways you can place N queens on an NxN chessboard so that none of them are able to capture others. Write a function that calculates them all and prints them to the screen as a visual board layout, and returns the number of solutions it found.

> **Tip 1**: A queen moves in straight lines vertically, horizontally, or diagonally. You need to place all eight queens so that no two share the same row, column, or diagonal.
>
> **Tip 2**: In the more advanced version of this challenge you would be required to return only the fundamental solutions, which means unique positions excluding rotations and reflections. This is not a requirement here.

### Sample input and output

- In an *8x8* board you need to place `8` queens. There are `92` possible arrangements, so your function should print each of them then return `92`.
- In a *10x10* board you need to place `10` queens. There are `724` possible arrangements, so your function should print each of them then return `724`.

Here is a suggested example layout for solutions:

``` text
. . . . . . . Q
. . . Q . . . .
Q . . . . . . .
. . Q . . . . .
. . . . . Q . .
. Q . . . . . .
. . . . . . Q .
. . . . Q . . .
```

### Stub

``` swift
import Foundation

func challenge64(board: [Int], queen cur: Int) -> Int {
    // your code goes here
    return 0
}

// test cases
let board = [Int](repeating: 0, count: Int.random(in: 5...10))
print("total solutions:", challenge64(board: board, queen: 0))
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Your queen placement function ought to call itself. The first time it’s called it represents the first queen being placed, the second it’s the second queen, and so on. If you reach N then you’ve placed all the queens and you have a solution.
2. In order to be sure you’ve found all solutions, you need to exhaust all possible placements.
3. Sometimes you will have placed six queens and realized there’s nowhere valid for the seventh to go. Be prepared to backtrack.
4. Two queens occupy the same column if their X difference is equal to their Y difference, or their X difference is equal to their negative Y difference.
5. You can solve this problem using a one-dimensional array of integers.

### Solution 1

``` swift
import Foundation

// transform given board into a NxN matrix, with
// given queen alignments and print it to console
func print(board: [Int]) -> Int {
    for row in 0..<board.count {
        let pos = board[row] // column of queen on current row
        for col in 0..<board.count {
            switch col == pos {
            case true: print("Q", terminator: " ")
            case false: print(".", terminator: " ")
            }
        }
        print()
    }
    print()
    return 1
}

func challenge64(board: inout [Int], queen: Int) -> Int {
    // when queen row number reaches max row of board, solution is found
    if queen == board.count { return print(board: board) }

    var total = 0
    column: for col in 0..<board.count {
        // limit this upto last row where queen was placed,
        // to avoid the condition of two queens on same row
        for row in 0..<queen {
            // get column number for already placed queen
            let other = board[row]
            // if two queens are on the same column
            if col == other { continue column }

            // current queen row - already placed queen row
            let deltaR = queen - row
            // already placed queen col - current queen col
            let deltaC = other - col
            // if current position is diagonal to already placed queen
            if deltaR == deltaC || deltaR == -deltaC { continue column }
        }
        // we have found a valid position for current queen
        board[queen] = col
        // recursively search for positions of next queens
        total += challenge64(board: &board, queen: queen + 1)
    }
    return total
}

// test cases
var board = [Int](repeating: 0, count: Int.random(in: 5...10))
print("total solutions:", challenge64(board: &board, queen: 0))
```

``` terminal
. Q . . . . 
. . . Q . . 
. . . . . Q 
Q . . . . . 
. . Q . . . 
. . . . Q . 

. . Q . . . 
. . . . . Q 
. Q . . . . 
. . . . Q . 
Q . . . . . 
. . . Q . . 

. . . Q . . 
Q . . . . . 
. . . . Q . 
. Q . . . . 
. . . . . Q 
. . Q . . . 

. . . . Q . 
. . Q . . . 
Q . . . . . 
. . . . . Q 
. . . Q . . 
. Q . . . . 

total solutions: 4
```
