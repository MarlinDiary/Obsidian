[[列表 - List]] 视图是显示滚动数据行的绝佳方法，但有时您也需要数据列（信息网格），以便在更大的屏幕上显示更多数据。

这可以通过两个视图来实现： `LazyHGrid` 用于显示水平数据，而 `LazyVGrid` 用于显示垂直数据。

创建网格分为两步。

1. 我们需要定义所需的行或列（我们只需定义其中之一）：

```swift
let layout = [
    GridItem(.fixed(80)),
    GridItem(.fixed(80)),
    GridItem(.fixed(80))
]
```

2. 定义好布局后，您应将网格放在 [[滚动视图 - ScrollView]] 中：

```swift
ScrollView {
    LazyVGrid(columns: layout) {
        ForEach(0..<1000) {
            Text("Item \($0)")
        }
    }
}
```

网格的最大优点是可以在不同尺寸的屏幕上使用。这可以通过使用自适应尺寸的不同列布局来实现，就像下面这样（只要列的宽度至少为 80 点，我们就可以尽可能多地容纳它们）：

```swift
let layout = [
    GridItem(.adaptive(minimum: 80)),
]
```

您还可以指定一个最大范围，以获得更多控制：

```swift
let layout = [
    GridItem(.adaptive(minimum: 80, maximum: 120)),
]
```

另外，水平网格的制作过程几乎相同：

```swift
ScrollView(.horizontal) {
    LazyHGrid(rows: layout) {
        ForEach(0..<1000) {
            Text("Item \($0)")
        }
    }
}
```

#swiftui 