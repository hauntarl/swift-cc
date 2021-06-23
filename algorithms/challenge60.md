# Challenge 60

## Tic-Tac-Toe winner

> **Difficulty**: Tricky

Create a function that detects whether either player has won in a game of Tic-Tac-Toe.

> **Tip**: A tic-tac-toe board is 3x3, containing single letters that are either X, O, or empty. A win is three Xs or Os in a straight line.

### Sample input and output

- The array `[["X", "", "O"], ["", "X", "O"], ["", "", "X"]]` should return `true`.
- The array `[["X", "", "O"], ["X", "", "O"], ["X", "", ""]]` should return `true`.
- The array `[["", "X", ""], ["O", "X", ""], ["O", "X", ""]]` should return `true`.
- The array `[["", "X", ""], ["O", "X", ""], ["O", "", "X"]]` should return `false`.
- The array `[["", "", ""], ["", "", ""], ["", "", ""]]` should return `false`.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
assert(challenge60(board: [["X", "", "O"], ["", "X", "O"], ["", "", "X"]]) == true, "Challenge 60: Test #1 - failed")
assert(challenge60(board: [["X", "", "O"], ["X", "", "O"], ["X", "", ""]]) == true, "Challenge 60: Test #2 - failed")
assert(challenge60(board: [["", "X", ""], ["O", "X", ""], ["O", "X", ""]]) == true, "Challenge 60: Test #3 - failed")
assert(challenge60(board: [["", "X", ""], ["O", "X", ""], ["O", "", "X"]]) == false, "Challenge 60: Test #4 - failed")
assert(challenge60(board: [["", "", ""], ["", "", ""], ["", "", ""]] ) == false, "Challenge 60: Test #5 - failed")
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. Your board parameter should be `[[String]]` – an array of array of strings.
2. You can evaluate the rows and columns in a loop.
3. You can evaluate diagonals using two checks: one from top left to bottom right, and one from bottom left to top right.
4. You might want to use a nested function to make your code cleaner.

### Solution 1

``` swift
import Foundation

let valid = Set<String>(["X", "O", ""])

func verify(_ board: [[String]]) -> Bool {
    if board.count != 3 { return false }
    for row in board {
        if row.count != 3  { return false }
        if !row.allSatisfy(valid.contains) { return false }
    }
    return true
}

func character(
    at coord: (x: Int, y: Int), 
    of board: [[String]]
) -> String? {
    let ch = board[coord.x][coord.y]
    if ch.isEmpty { return nil }
    return ch
}

func checkDiagonals(of board: [[String]]) -> Bool {
    switch character(at: (1, 1), of: board) {
    case let ch where board[0][0] == ch && board[2][2] == ch:
        return true
    case let ch where board[2][0] == ch && board[0][2] == ch:
        return true
    default:
        return false
    }
}

func check(row: Int, of board: [[String]]) -> Bool {
    if let ch = character(at: (row, 1), of: board) {
        return board[row][0] == ch && board[row][2] == ch    
    }
    return false
}

func check(col: Int, of board: [[String]]) -> Bool {
    if let ch = character(at: (1, col), of: board) {
        return board[0][col] == ch && board[2][col] == ch
    } 
    return false
}

func challenge60(board: [[String]]) -> Bool {
    precondition(verify(board), "A tic-tac-toe board is 3x3.")
    if checkDiagonals(of: board) { return true }
    for i in 0...2 where check(row: i, of: board) { return true }
    for j in 0...2 where check(col: j, of: board) { return true }
    return false
}

// test cases
assert(challenge60(board: [["X", "", "O"], ["", "X", "O"], ["", "", "X"]]) == true, "Challenge 60: Test #1 - failed")
assert(challenge60(board: [["X", "", "O"], ["X", "", "O"], ["X", "", ""]]) == true, "Challenge 60: Test #2 - failed")
assert(challenge60(board: [["", "X", ""], ["O", "X", ""], ["O", "X", ""]]) == true, "Challenge 60: Test #3 - failed")
assert(challenge60(board: [["", "X", ""], ["O", "X", ""], ["O", "", "X"]]) == false, "Challenge 60: Test #4 - failed")
assert(challenge60(board: [["", "", ""], ["", "", ""], ["", "", ""]] ) == false, "Challenge 60: Test #5 - failed")
```

> **Time Complexity** (worst case): `O(n)`
