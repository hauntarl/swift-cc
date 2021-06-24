# Challenge 63

## Flood fill

> **Difficulty**: Taxing

Write a function that accepts a two-dimensional array of integers that are 0 or 1, a new number to place, and a position to start. You should read the existing number at the start position, change it to the new number, then change any surrounding numbers that matched the start number, then change any surrounding those, and so on - like a flood fill algorithm in Photoshop.

> **Tip 1**: A flood fill works by filling grid positions directly above, below, to the left, and to the right, stopping only when a different number is encountered.
>
> **Tip 2**: If the arrays contained all zeros, filling 5 would cause the arrays to contain all 5s because all numbers would be filled.

### Sample input and output

Given the following set up:

``` swift
let random = GKMersenneTwisterRandomSource(seed: 1)
let grid = (1...10).map { _ in (1...10).map { _ in
    Int(random.nextInt(upperBound: 2)) } 
}
```

You will have the following grid:

``` text
[0, 0, 0, 0, 0, 1, 0, 0, 1, 1]
[0, 1, 1, 0, 0, 0, 0, 1, 0, 0]
[0, 1, 0, 0, 0, 0, 0, 0, 1, 1]
[1, 0, 1, 0, 0, 1, 1, 0, 0, 0]
[1, 0, 1, 0, 1, 1, 1, 1, 1, 0]
[1, 0, 1, 1, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 1, 1, 1, 0, 1, 1]
[1, 1, 1, 0, 0, 1, 1, 1, 1, 1]
[1, 1, 0, 1, 1, 1, 1, 0, 0, 0]
[0, 1, 1, 0, 0, 1, 0, 1, 1, 1]
```

After running this code:

``` swift
challenge63(fill: 5, in: grid, at: (x: 2, y: 0))
```

You will have the following grid:

``` text
[5, 5, X, 5, 5, 1, 5, 5, 1, 1]
[5, 1, 1, 5, 5, 5, 5, 1, 0, 0]
[5, 1, 5, 5, 5, 5, 5, 5, 1, 1]
[1, 0, 1, 5, 5, 1, 1, 5, 5, 5]
[1, 0, 1, 5, 1, 1, 1, 1, 1, 5]
[1, 0, 1, 1, 5, 5, 5, 5, 5, 5]
[0, 0, 0, 0, 1, 1, 1, 5, 1, 1]
[1, 1, 1, 0, 0, 1, 1, 1, 1, 1]
[1, 1, 0, 1, 1, 1, 1, 0, 0, 0]
[0, 1, 1, 0, 0, 1, 0, 1, 1, 1]
```

> **Note**: In the above grid I marked with X where the fill started, but that will be a five too.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
let limit = 0..<10
var grid = [[String]](
    repeating: [String](repeating: "", count: limit.count),
    count: limit.count
)
for y in limit { for x in limit { grid[y][x] = String(Int.random(in: 0...1)) } }
challenge63(fill: "_", in: grid, from: /*insert start point*/)
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You can solve this using a recursive function, or using a loop.
2. You will almost certainly find it useful to add `print()` statements inside your loop or function that displays what square is being manipulated, and perhaps also the current grid.
3. Keep a stack of squares that need to be filled. Start by adding your initial square, then loop over that and remove one square to fill / spread from each time.

### Solution 1

``` swift
import Foundation

struct Point: Hashable, LosslessStringConvertible {
    var x: Int
    var y: Int
    var description: String { return "(\(x), \(y))" }

    init(_ point: (Int, Int)) { (x, y) = point }
    init?(_ description: String) { return nil }

    static func +=(lhs: inout Point, rhs: Point) {
        lhs.x += rhs.x
        lhs.y += rhs.y
    }
}

let moves = [
    Point((-1, -1)), Point((0, -1)), Point((1, -1)),
    Point((-1, 0)), Point((1, 0)),
    Point((-1, 1)), Point((0, 1)), Point((1, 1))
]

func nextMoves(
    in grid: [[String]], 
    from point: Point, 
    with start: String,
    not seen: Set<Point>) -> [Point] {
    var valid = [Point](repeating: point, count: moves.count)
    for (cur, nxt) in moves.enumerated() { valid[cur] += nxt }
    return valid.filter {
        limit ~= $0.x && limit ~= $0.y &&
        grid[$0.y][$0.x] == start && !seen.contains($0)
    }
}

func challenge63( fill: String, in grid: [[String]], from point: Point) {
    print(grid: grid)
    let start = grid[point.y][point.x]
    print("start value: \(start)")

    var (filled, queue) = (grid, [point])
    var seen = Set(queue)
    while !queue.isEmpty {
        let point = queue.removeFirst()
        filled[point.y][point.x] = fill

        let moves = nextMoves(
            in: filled, from: point, 
            with: start, not: seen
        )
        print("start point: \(point), valid moves: \(moves)")
        for next in moves { seen.insert(next) }
        queue.append(contentsOf: moves)
    }
    filled[point.y][point.x] = "X"
    print("total points filled: \(seen.count)")
    print(grid: filled)
}

func print(grid: [[String]]) {
    print("--------------------------------")
    for row in grid { print("| \(row.joined(separator: ", ")) |") }
    print("--------------------------------")
}

// test cases
let limit = 0..<10
var grid = [[String]](
    repeating: [String](repeating: "", count: limit.count),
    count: limit.count
)
for y in limit { for x in limit { grid[y][x] = String(Int.random(in: 0...1)) } }
let start = Point((Int.random(in: 0...9), Int.random(in: 0...9)))
challenge63(fill: "_", in: grid, from: start)
```

``` terminal
--------------------------------
| 0, 1, 1, 1, 0, 1, 0, 0, 1, 0 |
| 0, 1, 1, 1, 0, 1, 0, 1, 0, 0 |
| 0, 0, 0, 0, 0, 1, 0, 1, 0, 0 |
| 0, 0, 1, 0, 1, 1, 1, 1, 0, 0 |
| 1, 1, 0, 0, 0, 0, 1, 1, 1, 1 |
| 0, 1, 0, 0, 0, 1, 0, 1, 1, 1 |
| 0, 0, 0, 0, 0, 1, 0, 0, 1, 1 |
| 0, 0, 0, 0, 1, 1, 0, 1, 0, 0 |
| 0, 0, 1, 0, 1, 1, 0, 0, 0, 1 |
| 1, 1, 1, 0, 0, 1, 1, 0, 1, 1 |
--------------------------------
start value: 1
start point: (8, 4), valid moves: [(7, 3), (7, 4), (9, 4), (7, 5), (8, 5), (9, 5)]
start point: (7, 3), valid moves: [(7, 2), (6, 3), (6, 4)]
start point: (7, 4), valid moves: []
start point: (9, 4), valid moves: []
start point: (7, 5), valid moves: [(8, 6)]
start point: (8, 5), valid moves: [(9, 6)]
start point: (9, 5), valid moves: []
start point: (7, 2), valid moves: [(7, 1)]
start point: (6, 3), valid moves: [(5, 2), (5, 3)]
start point: (6, 4), valid moves: [(5, 5)]
start point: (8, 6), valid moves: [(7, 7)]
start point: (9, 6), valid moves: []
start point: (7, 1), valid moves: [(8, 0)]
start point: (5, 2), valid moves: [(5, 1), (4, 3)]
start point: (5, 3), valid moves: []
start point: (5, 5), valid moves: [(5, 6)]
start point: (7, 7), valid moves: []
start point: (8, 0), valid moves: []
start point: (5, 1), valid moves: [(5, 0)]
start point: (4, 3), valid moves: []
start point: (5, 6), valid moves: [(4, 7), (5, 7)]
start point: (5, 0), valid moves: []
start point: (4, 7), valid moves: [(4, 8), (5, 8)]
start point: (5, 7), valid moves: []
start point: (4, 8), valid moves: [(5, 9)]
start point: (5, 8), valid moves: [(6, 9)]
start point: (5, 9), valid moves: []
start point: (6, 9), valid moves: []
total points filled: 28
--------------------------------
| 0, 1, 1, 1, 0, _, 0, 0, _, 0 |
| 0, 1, 1, 1, 0, _, 0, _, 0, 0 |
| 0, 0, 0, 0, 0, _, 0, _, 0, 0 |
| 0, 0, 1, 0, _, _, _, _, 0, 0 |
| 1, 1, 0, 0, 0, 0, _, _, X, _ |
| 0, 1, 0, 0, 0, _, 0, _, _, _ |
| 0, 0, 0, 0, 0, _, 0, 0, _, _ |
| 0, 0, 0, 0, _, _, 0, _, 0, 0 |
| 0, 0, 1, 0, _, _, 0, 0, 0, 1 |
| 1, 1, 1, 0, 0, _, _, 0, 1, 1 |
--------------------------------
```
