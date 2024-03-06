如果要将文字后面的整个区域填充为红色，应将颜色放入 `ZStack` 中，将其视为一个单独的整体视图：

```swift
ZStack {
    Color.red
    Text("Your content")
}
```

这里的 Color.red 我认为是一种 [[结构 - Struct#静态属性]]。

## 框架

颜色会自动占用所有可用空间，但您可以使用框架修饰符来要求特定尺寸。例如，我们可以这样要求一个 200 × 200 的红色正方形：

```swift
Color.red
    .frame(width: 200, height: 200)
```

您还可以根据所需的布局指定最小和最大宽度和高度：

```swift
Color.red
    .frame(minWidth: 200, maxWidth: .infinity, maxHeight: 200)
```

## 选色

内置颜色：`Color.blue` 、 `Color.green` 、 `Color.indigo`......

语义颜色：Color.primary、 Color.secondary

RGB 颜色：(red: 1, green: 0.8, blue: 0)

材质： `background()` 修改器还可以接受材质，这些材质会在其下方应用磨砂玻璃效果

## Safe Area

如果您希望您的内容位于安全区域之下，您可以使用 `.ignoresSafeArea()` 修饰符：

```swift
ZStack {
    Color.red
    Text("Your content")
}
.ignoresSafeArea()    
```

有些视图（如 `List` 视图）允许内容滚动到安全区域之外，但会添加额外的嵌入，以便用户可以将内容滚动到视图中。

#swiftui #struct 