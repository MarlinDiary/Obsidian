过渡效果可以控制插入和移除[[视图 - View]]的方式，我们可以使用内置的过渡效果，以不同的方式将它们组合起来，甚至创建[[自定义过渡|完全自定义的过渡效果]]。

通过[[显式动画 - explicit animation|动画]] `withAnimation()` 对状态变化进行包装，我们可以获得 SwiftUI 的内置过渡：

```swift
withAnimation {
    isShowingRed.toggle()
}
```

但我们还可以使用 `transition()` 修改器做得更好：

```swift
Rectangle()
    .fill(.red)
    .frame(width: 200, height: 200)
    .transition(.scale)

// 让矩形按比例缩放
```

还可以尝试其他一些过渡效果。 如用 `.asymmetric` 来组合过渡效果：

```swift
.transition(.asymmetric(insertion: .scale, removal: .opacity))
```

#animation #hard 