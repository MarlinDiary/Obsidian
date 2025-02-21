1. 最简单的对齐方式是使用 `frame()` 修改器的 `alignment` 参数。

```swift
.frame(width: 300, height: 300, alignment: .topLeading)
```

2. 还可以使用 `offset(x:y:)` 在 frame 内移动文字。

3. 使用 Stack 的 `alignment` 参数也是一种选择。

```swift
HStack(alignment: .lastTextBaseline) {
```

4. 可以为每个视图自定义 "对齐" 的含义。

SwiftUI 为此提供了 `alignmentGuide()` 修改器。该修改器需要两个参数：**要更改的 Guide** 和 **返回新对齐方式的 Closure**。闭包将获得一个 `ViewDimensions` 对象，该对象包含视图的宽度和高度，以及读取不同边缘的能力。

默认情况下的 `.leading` 对齐方式相当于这样：

```swift
VStack(alignment: .leading) {
    Text("Hello, world!")
        .alignmentGuide(.leading) { d in d[.leading] }
    Text("This is a longer line of text")
}
```

我们可以重写 alignment guide：

```swift
VStack(alignment: .leading) {
    Text("Hello, world!")
        .alignmentGuide(.leading) { d in d[.trailing] }
    Text("This is a longer line of text")
}
```

虽然 alignment guide 闭包会传递 ViewDimensions，但如果不想使用，也不必使用它们--你可以发回一个硬编码的数字，或者创建一些其他的计算方法：

```swift
VStack(alignment: .leading) {
        ForEach(0..<10) { position in
            Text("Number \(position)")
                .alignmentGuide(.leading) { _ in Double(position) * -10 }
        }
    }
```

#swiftui #easy 