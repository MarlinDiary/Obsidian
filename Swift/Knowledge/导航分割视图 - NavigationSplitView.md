NavigationSplitView 可以指定并排显示两列或三列数据，iPadOS 会根据具体配置在适当的时候显示或隐藏这些数据。

比如以下代码：

```swift
NavigationSplitView {
    Text("Primary")
} detail: {
    Text("Content")
}
```

- 在 iPhone 上，你将看到 Primary；
- 在横屏 iPad 上，你会看到 Primary 位于设备的侧边栏中，而 Content 则占满屏幕的其余部分；
- 在纵向模式的 iPad 上，你会看到 Content 充满整个屏幕。

SwiftUI 会自动链接主视图和次要视图，这意味着如果您在主视图中有 [[导航链接 - NavigationLink]] 内容，它将自动在辅助视图中加载其内容：

```swift
NavigationSplitView {
    NavigationLink("Primary") {
        Text("New view")
    }
} detail: {
    Text("Content")
}
```

可以通过一些方法自定义分割视图的行为。

例如，当空间受到部分限制时（iPad 竖屏模式），你可以告诉 iOS 保留侧边栏：

```swift
NavigationSplitView(columnVisibility: .constant(.all)) {
    NavigationLink("Primary") {
        Text("New view")
    }
} detail: {
    Text("Content")
        .navigationTitle("Content View")
}
.navigationSplitViewStyle(.balanced)
```

其次，你可以告诉系统默认首选详细视图，这对选择主视图作为标准视图的 iPhone 很有帮助：

```swift
NavigationSplitView(preferredCompactColumn: .constant(.detail)) {
```

#swiftui 