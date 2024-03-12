SwiftUI 允许将上下文菜单附加到对象上，以通过长按的方式提供额外功能，所有操作均使用 `contextMenu()` 修改器完成。

您可以向其传递一系列按钮，它们将按顺序显示：

```swift
struct ContentView: View {
    @State private var backgroundColor = Color.red

    var body: some View {
        VStack {
            Text("Hello, World!")
                .padding()
                .background(backgroundColor)

            Text("Change Color")
                .padding()
                .contextMenu {
                    Button("Red") {
                        backgroundColor = .red
                    }

                    Button("Green") {
                        backgroundColor = .green
                    }

                    Button("Blue") {
                        backgroundColor = .blue
                    }
                }
        }
    }
}
```

与 [[标签 - Tab]] 一样，使用 `Label` 视图，上下文菜单中的每个项目都可以附加文本和图片：

```swift
Button("Red", systemImage: "checkmark.circle.fill") {
    backgroundColor = .red
}
```

#swiftui 