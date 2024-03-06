## 自定义按钮的外观

### 方式 ①：role

```swift
Button("Delete selection", role: .destructive, action: executeDelete)
```

### 方式 ②：按钮的内置样式

```swift
VStack {
    Button("Button 1") { }
        .buttonStyle(.bordered)
    Button("Button 2", role: .destructive) { }
        .buttonStyle(.bordered)
    Button("Button 3") { }
        .buttonStyle(.borderedProminent)
    Button("Button 4", role: .destructive) { }
        .buttonStyle(.borderedProminent)
}
```

如果想更改外框的填充色：

```swift
Button("Button 3") { }
    .buttonStyle(.borderedProminent)
    .tint(.mint)
```

### 方式 ③：完全自定义

可以使用第二个尾部[[闭包 - Closure]]传递自定义标签：

```swift
Button {
    print("Button was tapped")
} label: {
    Text("Tap me!")
        .padding()
        .foregroundStyle(.white)
        .background(.red)
}
```

可以用 [[图像 - Image]] 作为按钮：

```swift
Button {
    print("Edit button was tapped")
} label: { 
    Image(systemName: "pencil")
}
```

如果同时需要文本和图像，您有两种选择。

第一种是直接在 `Button` 中同时提供文本和图像，就像这样：

```swift
Button("Edit", systemImage: "pencil") {
    print("Edit button was tapped")
}
```

但是，如果您需要更多自定义类型，SwiftUI 提供了一种名为 `Label` 的专用 Type：

```swift
Button {
    print("Edit button was tapped")
} label: {
    Label("Edit", systemImage: "pencil")
        .padding()
        .foregroundStyle(.white)
        .background(.red)
}
```

## 修饰符

| 修饰符               | 作用                  |
| ----------------- | ------------------- |
| .scaleEffect      | 1 代表 100%，即正常大小     |
| .blur             | 模糊效果，可调 radius      |
| .overlay          | 以与覆盖视图相同的大小和位置创建新视图 |
| .rotation3DEffect | 它可以给定一个旋转量和一个轴      |
| .buttonStyle      | 可以调整显示的颜色           |

#struct #swiftui #closure 