可以将布尔值的变化制作成动画的原因：Swift 并没有以某种方式在假值和真值之间创造新的值，而只是将因变化而发生的视图变化制作成动画。

我们可以把 [[隐式动画 - implicit animation]] 修饰符作用到一些[[双向绑定]]的数据上：

```swift
$animationAmount.animation()
```

这些绑定动画使用的 `animation()` 修饰符与我们在视图上使用的类似，因此，如果您愿意，可以使用动画[[隐式动画 - implicit animation#修改器|修改器]]：

```swift
Stepper("Scale amount", value: $animationAmount.animation(
    .easeInOut(duration: 1)
        .repeatCount(3, autoreverses: true)
), in: 1...10)
```

这些绑定动画有效地扭转了隐式动画的局面：与其在视图上设置动画并通过状态变化隐式地使其产生动画效果，不如不在视图上设置任何动画并通过状态变化显式地使其产生动画效果。在前者中，状态变化不知道会触发动画，而在后者中，视图也不知道会被动画化。

#animation #hard 