显式动画，它既不与绑定相连（[[绑定动画 - binding animation]]），也不与视图相连（[[隐式动画 - implicit animation]]），只是明确要求因一个状态变化而出现一个特定的动画。

如果我们使用 `withAnimation()` 函数，那么 SwiftUI 将确保新状态产生的任何变化都将自动以动画的形式呈现：

```swift
withAnimation {
    animationAmount += 360
}
```

与其他动画相同，`withAnimation()` 也可以给定[[隐式动画 - implicit animation#控制动画的类型|动画参数]]：

```swift
withAnimation(.spring(duration: 1, bounce: 0.5)) {
    animationAmount += 360
}
```

#animation #easy 