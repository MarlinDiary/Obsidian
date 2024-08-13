确认对话框是 [[警报 - Alert]] 的替代方案，可让我们添加许多[[按钮 - Button]]。

二者的创建方式也很类似：

- 都是通过在视图层次结构中附加修改器创建的
- 当条件为真时，SwiftUI 会自动显示两者
- 两者都可以添加按钮来执行各种操作
- 两者都可以附加第二个[[闭包 - Closure]]，以提供额外的信息

1. 创建条件：

```swift
@State private var showingConfirmation = false
```

2. 添加修改器（接受三个参数：标题、当前是否显示对话框的绑定、提供应显示按钮的闭包）：

```swift
.confirmationDialog("Change background", isPresented: $showingConfirmation) {
    Button("Red") { backgroundColor = .red }
    Button("Green") { backgroundColor = .green }
    Button("Blue") { backgroundColor = .blue }
    Button("Cancel", role: .cancel) { }
} message: {
    Text("Select a new color")
}
```

#swiftui #easy 