SwiftUI 提供了一种名为 `visualEffect()` 的方法，它具有非常明确的目的和限制：它允许我们应用可用于改变外观的效果，但这实际上意味着它不能做任何影响实际布局位置或视图框架的事情。

这个修改器的工作方式非常有趣：我们向它传递一个要运行的闭包，它会为我们提供要修改的内容（即视图本身）以及一个 `GeometryProxy` 。

我们不能像通常那样随意应用修改器，但我们仍然可以使用大量的修改器。

一个例子如下：

```swift
ScrollView(.horizontal, showsIndicators: false) {
    HStack(spacing: 0) {
        ForEach(1..<20) { num in
            Text("Number \(num)")
                .font(.largeTitle)
                .padding()
                .background(.red)
                .frame(width: 200, height: 200)
                .visualEffect { content, proxy in
                    content
                        .rotation3DEffect(.degrees(-proxy.frame(in: .global).minX) / 8, axis: (x: 0, y: 1, z: 0))
                }

        }
    }
}
```

这是一个比[[几何图形阅读器 - GeometryReader]]更简洁的解决方案，因为我们不再需要添加第二个 `frame()` 修改器来阻止内容占据整个屏幕。

如果添加两个额外的修改器，我们就能让这个效果更好地发挥作用：

- scrollTargetLayout()：用到 `HStack`，表示希望将 `HStack` 中的每个视图都设为**滚动目标**
- scrollTargetBehavior(.viewAligned)：用到 `ScrollView`，表示希望在所有**滚动目标**间平滑移动

#animation #hard 