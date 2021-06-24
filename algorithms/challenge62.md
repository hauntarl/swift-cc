# Challenge 62

## Points to angles

> **Difficulty**: Tricky

Write a function that accepts an array of CGPoint pairs, and returns an array of the angles between each point pair. Return the angles in degrees, where 0 or 360 is straight up.

> **Tip**: If it helps your thought process, imagine each point pair as being two touches on the screen: you have the first touch and the second, what is the angle between them?

### Sample input and output

- If your code has worked correctly, that should print `[0.0, 45.0, 90.0, 135.0, 180.0, 225.0, 270.0, 315.0]`. Returning `360.0` for the first number is also acceptable.

### Stub

``` swift
import Foundation

// your code goes here

// test cases
var points = [(first: CGPoint, second: CGPoint)]()
points.append((first: CGPoint.zero, second: CGPoint(x: 0, y: -100)))
points.append((first: CGPoint.zero, second: CGPoint(x: 100, y: -100)))
points.append((first: CGPoint.zero, second: CGPoint(x: 100, y: 0)))
points.append((first: CGPoint.zero, second: CGPoint(x: 100, y: 100)))
points.append((first: CGPoint.zero, second: CGPoint(x: 0, y: 100)))
points.append((first: CGPoint.zero, second: CGPoint(x: -100, y: 100)))
points.append((first: CGPoint.zero, second: CGPoint(x: -100, y: 0)))
points.append((first: CGPoint.zero, second: CGPoint(x: -100, y: -100)))
assert(
    challenge62(points: points) == [0.0, 45.0, 90.0, 135.0, 180.0, 225.0, 270.0, 315.0], 
    "Challenge 62: Test #1 - failed"
)
```

### Hints

> **NOTE**: Remember, read as few hints as you can to help you solve the challenge, and only read them if you’ve tried and failed.

1. You’re mapping an array of one type to an array of another type. Yes, that means `map()` is a good idea.
2. You’ll need to use `atan2()` to calculate the angle between any two points, providing the Y delta and the X delta as its two parameters.
3. `atan2()` works in radians, so you’ll need to convert the value to degrees using the formula `degrees = radians * 180 / Double.pi`.
4. Where “0” lies is of course arbitrary, but the convention is that 0 degrees runs along the positive X axis. You need to correct for this.

### Solution 1

``` swift
import Foundation

func toDegrees(from rad: CGFloat) -> CGFloat {
    var deg = rad * 180 / CGFloat.pi - 90
    if deg < 0 { deg += 360 }
    return deg == 360 ? 0 : deg
}

func challenge62(points: [(first: CGPoint, second: CGPoint)]) -> [CGFloat] {
    return points.map { toDegrees(from: atan2(
            $0.first.y - $0.second.y,
            $0.first.x - $0.second.x
    )) }
}

// test cases
var points = [(first: CGPoint, second: CGPoint)]()
points.append((first: CGPoint.zero, second: CGPoint(x: 0, y: -100)))
points.append((first: CGPoint.zero, second: CGPoint(x: 100, y: -100)))
points.append((first: CGPoint.zero, second: CGPoint(x: 100, y: 0)))
points.append((first: CGPoint.zero, second: CGPoint(x: 100, y: 100)))
points.append((first: CGPoint.zero, second: CGPoint(x: 0, y: 100)))
points.append((first: CGPoint.zero, second: CGPoint(x: -100, y: 100)))
points.append((first: CGPoint.zero, second: CGPoint(x: -100, y: 0)))
points.append((first: CGPoint.zero, second: CGPoint(x: -100, y: -100)))
assert(
    challenge62(points: points) == [0.0, 45.0, 90.0, 135.0, 180.0, 225.0, 270.0, 315.0], 
    "Challenge 62: Test #1 - failed"
)
```
