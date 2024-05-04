SwiftUI 有先进的点击算法，它除了借助视图的框架（frame），还借助视图的内容（content）。例如，如果在圆形上附加点击[[手势 - Gesture|手势]]，SwiftUI 将忽略圆形的透明部分。

我们可以通过**两种**实用的方式来控制用户的交互性。

## allowsHitTesting()

如果将该修饰符附加到视图，并将其参数设置为 false，那么该视图就不会被认为是可点击的。

但这只意味着该视图不会捕捉到任何点击，视图后面的东西仍然会被点击。

```swift
Circle()
    .fill(.red)
    .frame(width: 300, height: 300)
    .onTapGesture {
        print("Circle tapped!")
    }
    .allowsHitTesting(false)
```

## contentShape()

它可以让我们指定某视图的可点击形状。

默认情况下，圆的可点击形状是一个相同大小的圆，但你也可以像这样指定一个不同的形状：

```swift
Circle()
    .fill(.red)
    .frame(width: 300, height: 300)
    .contentShape(.rect)
    .onTapGesture {
        print("Circle tapped!")
    }
```

这个修改器在带有 Spacer() 的[[堆栈 - Stack|堆栈]]中格外有用，因为 Spacer() 默认不可以触发动作：

```swift
VStack {
    Text("Hello")
    Spacer().frame(height: 100)
    Text("World")
}
.contentShape(.rect)
.onTapGesture {
    print("VStack tapped!")
}
```

#swiftui 