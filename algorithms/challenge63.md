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

// create a struct to represent a co-ordinate in given grid
// make Point conform to Hashable to avoid re-visiting seen points
// make Point representable as String to reduce visual density
struct Point: Hashable, CustomStringConvertible {
    var x: Int
    var y: Int
    var description: String { return "(\(x), \(y))" }

    init(_ x: Int, _ y: Int) { (self.x, self.y) = (x, y) }

    static func +=(lhs: inout Point, rhs: Point) {
        lhs.x += rhs.x
        lhs.y += rhs.y
    }
}

// moves contains all the surrounding points for origin i.e. (0, 0)
// utilize this to calc. surrounding points for a point in grid
let moves = [
    Point(-1, -1), Point(0, -1), Point(1, -1),
    Point(-1, 0), Point(1, 0),
    Point(-1, 1), Point(0, 1), Point(1, 1)
]

// nextMoves calc. and returns valid surrounding points based on:
// - grid Boundaries
// - given start point value
// - whether point has already been visited
func nextMoves(
    in grid: [[String]], 
    from point: Point, 
    with start: String,
    not seen: Set<Point>
) -> [Point] {
    // generate an array of surrounding points from given point in grid
    var valid = [Point](repeating: point, count: moves.count)
    for (cur, nxt) in moves.enumerated() { valid[cur] += nxt }
    // filter out the surrounding points which do not satisfy conditions
    return valid.filter {
        limit ~= $0.x && limit ~= $0.y &&
        grid[$0.y][$0.x] == start && !seen.contains($0)
    }
}

// performs flood fill in a given grid from a starting point
func challenge63(in grid: [[String]], from point: Point) {
    print(grid: grid)
    // find the value at starting position for reference
    let start = grid[point.y][point.x]
    print("start value: \(start)")

    // create a copy of grid to perform flood fill operation
    // create a queue with given starting point
    var (filled, queue) = (grid, [point])
    // create a Set to avoid visiting same points
    var seen = Set(queue)
    while !queue.isEmpty {
        let point = queue.removeFirst()
        // fill the visited points
        filled[point.y][point.x] = "_"

        // find out the next possible moves from current position
        let moves = nextMoves(
            in: filled, from: point, 
            with: start, not: seen
        )
        print("start point: \(point), valid moves: \(moves)")
        // mark the next moves as seen, marking them as visited before
        // actually visiting has a great performance boost it will stop
        // future iterations from adding same points in the queue
        for next in moves { seen.insert(next) }
        // and add them to the queue to visit later
        queue.append(contentsOf: moves)
    }
    // mark the start fill point with a different character for visual aid
    filled[point.y][point.x] = "X"
    print("total points filled: \(seen.count)")
    print(grid: filled)
}

// prints given grid in user readable format
func print(grid: [[String]]) {
    print("-----------------------")
    for row in grid { print("| \(row.joined(separator: " ")) |") }
    print("-----------------------")
}

// test cases
let limit = 0..<10
var grid = [[String]](
    repeating: [String](repeating: "", count: limit.count),
    count: limit.count
)
for y in limit { for x in limit { grid[y][x] = String(Int.random(in: 0...1)) } }
let start = Point(Int.random(in: limit), Int.random(in: limit))
challenge63(in: grid, from: start)
```

``` terminal
-----------------------
| 0 0 0 0 1 0 1 0 1 1 |
| 0 0 1 0 1 1 1 1 1 0 |
| 1 0 0 0 0 1 0 1 1 0 |
| 1 0 0 1 1 0 1 0 1 0 |
| 0 0 1 1 1 1 0 0 1 0 |
| 1 1 1 0 1 1 1 1 0 1 |
| 0 0 0 0 1 1 0 0 1 0 |
| 0 1 0 0 1 1 0 1 0 0 |
| 1 0 1 1 1 1 0 1 0 1 |
| 0 1 1 1 1 0 1 1 0 0 |
-----------------------
start value: 0
start point: (1, 6), valid moves: [(0, 6), (2, 6), (0, 7), (2, 7)]
start point: (0, 6), valid moves: []
start point: (2, 6), valid moves: [(3, 5), (3, 6), (3, 7)]
start point: (0, 7), valid moves: [(1, 8)]
start point: (2, 7), valid moves: []
start point: (3, 5), valid moves: []
start point: (3, 6), valid moves: []
start point: (3, 7), valid moves: []
start point: (1, 8), valid moves: [(0, 9)]
start point: (0, 9), valid moves: []
total points filled: 10
-----------------------
| 0 0 0 0 1 0 1 0 1 1 |
| 0 0 1 0 1 1 1 1 1 0 |
| 1 0 0 0 0 1 0 1 1 0 |
| 1 0 0 1 1 0 1 0 1 0 |
| 0 0 1 1 1 1 0 0 1 0 |
| 1 1 1 _ 1 1 1 1 0 1 |
| _ X _ _ 1 1 0 0 1 0 |
| _ 1 _ _ 1 1 0 1 0 0 |
| 1 _ 1 1 1 1 0 1 0 1 |
| _ 1 1 1 1 0 1 1 0 0 |
-----------------------
```
