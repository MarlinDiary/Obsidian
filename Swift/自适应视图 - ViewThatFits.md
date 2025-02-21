您可以为该视图提供多种不同的布局，它会自动按顺序尝试每一种布局，直到找到一个可以容纳在可用空间内的布局。

一个例子如下，默认情况下，它会尝试显示一个 500×200 的矩形，但如果无法适应可用空间，就会显示一个 200×200 的圆形：

```swift
ViewThatFits {
    Rectangle()
        .frame(width: 500, height: 200)

    Circle()
        .frame(width: 200, height: 200)
}
```

#swiftui #easy 