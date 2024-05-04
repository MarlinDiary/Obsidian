可用 `swipeActions()` 实现行轻扫操作，它允许我们在列表行的一侧或两侧注册一个或多个按钮。

默认情况下，按钮将放置在行的右侧边缘，并且没有颜色，从右向左轻扫时将显示一个灰色按钮：

```swift
List {
    Text("Taylor Swift")
        .swipeActions {
            Button("Send message", systemImage: "message") {
                print("Hi")
            }
        }
}
```

**可以**为 `swipeActions()` 提供一个 `edge` 参数，从而自定义按钮的边缘位置；**可以**为按钮添加一个 `tint()` 修改器，并自选颜色；**可以**为按钮附加一个按钮角色，从而自定义按钮的颜色：

```swift
List {
    Text("Taylor Swift")
        .swipeActions {
            Button("Delete", systemImage: "minus.circle", role: .destructive) {
                print("Deleting")
            }
        }
        .swipeActions(edge: .leading) {
            Button("Pin", systemImage: "pin") {
                print("Pinning")
            }
            .tint(.orange)
        }
}
```

#swiftui 