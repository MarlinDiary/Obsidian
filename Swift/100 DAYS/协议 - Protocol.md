## 协议的功能

协议有点像 Swift 中的合约：它让我们定义我们期望数据类型支持哪些功能，而 Swift 则确保我们代码的其余部分遵循这些规则。

```swift
protocol Vehicle {
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}
```

## 使用协议

我们通过在 `Car` 名称后使用**冒号**来告诉 Swift `Car` 与 `Vehicle` 相符，就像我们标记子类一样。

协议可以被 [[类 - Class]]、[[结构 - Struct]] 和[[枚举 - Enum]]所遵循。

```swift
struct Car: Vehicle {
    func estimateTime(for distance: Int) -> Int {
        distance / 50
    }

    func travel(distance: Int) {
        print("I'm driving \(distance)km.")
    }

    func openSunroof() {
        print("It's a nice day!")
    }
}
```

## 协议的优势

可以用协议去替代符合协议的 Type。

```swift
func commute(distance: Int, using vehicle: Vehicle) {
```

#protocol