SwiftUI 的 `ContentUnavailableView` 显示了一个标准的用户界面，供应用程序在没有任何内容可显示时使用。

`ContentUnavailableView` 非常适合您的应用程序依赖于尚未提供的用户信息时使用，例如，用户尚未创建任何数据，或者用户正在搜索某些内容但没有结果。

您可以像这样使用 `ContentUnavailableView` ：

```swift
ContentUnavailableView("No snippets", systemImage: "swift")
```

您还可以在下面添加一行额外的描述文本：

```swift
ContentUnavailableView("No snippets", systemImage: "swift", description: Text("You don't have any saved snippets yet."))
```

如果你想**完全**控制，可以为 Title 和 Description 提供单独的视图，并显示按钮，帮用户开始使用：

```swift
ContentUnavailableView {
    Label("No snippets", systemImage: "swift")
} description: {
    Text("You don't have any saved snippets yet.")
} actions: {
    Button("Create Snippet") {
        // create a snippet
    }
    .buttonStyle(.borderedProminent)
}
```

#swiftui 