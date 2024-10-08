SwiftUI 提供了两种视图定位方式：使用 `position()` 的绝对位置和使用 `offset()` 的相对位置。

如果要对视图进行绝对定位，应像这样使用 `position()` 修饰符：

```swift
Text("Hello, world!")
    .position(x: 100, y: 100)
```

这将把文本视图定位在父视图中 x:100 y:100 的位置。

值得注意的是，为了正确定位，position 视图将占用所有可用的空间。

与之相比，`offset()` 修改器的原理便截然不同。使用 `offset()` 修改器时，我们是在改变视图的渲染位置，而不会实际改变其底层几何图形。

#swiftui #easy 