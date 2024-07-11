简单的案例：一张卡片，我们可以在屏幕上拖动它，但松手后它又会回到原来的位置。

1. 我们需要一些状态来存储它们的拖曳量

```swift
@State private var dragAmount = CGSize.zero

//CGSize 是 Core Graphics 库中的一个结构体，用于描述一个矩阵的宽和高
```

2. 我们希望使用该尺寸来影响卡片在屏幕上的位置（SwiftUI 提供名为 `offset()` 的[[修改器 - Modifier]]，可以调整视图的 X 和 Y 坐标，而无需移动周围的其他视图。如果需要，可以输入离散的 X 和 Y 坐标，但并非巧合的是， `offset()` 也可以直接接受 `CGSize`）

```swift
.offset(dragAmount)
```

3. 我们可以创建一个 `DragGesture` 并将其附加到卡片上（该[[结构 - Struct]]有一些[[修改器 - Modifier]]， `onChanged()` 可让我们在用户移动手指时运行闭包，而 `onEnded()` 可让我们在用户抬起手指离开屏幕时运行闭包，从而结束拖动）

```swift
.gesture(
    DragGesture()
        .onChanged { dragAmount = $0.translation }
        .onEnded { _ in dragAmount = .zero }
)
```

#animation #hard 