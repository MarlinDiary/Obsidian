`ShareLink` 视图可让用户从我们的应用中导出内容到其他地方共享，例如将图片保存到照片库、使用 "信息" 向朋友发送链接等。

我们提供想要共享的内容，iOS 就会显示可以处理我们发送的数据的所有应用程序。

例如，我们可以共享这样一个 **URL**：

```swift
ShareLink(item: URL(string: "https://www.hackingwithswift.com")!)
```

您可以像这样为共享数据附加**主题**和**信息**：

```swift
ShareLink(item: URL(string: "https://www.hackingwithswift.com")!, subject: Text("Learn Swift here"), message: Text("Check out the 100 Days of SwiftUI!"))
```

您可以自定义按钮本身，提供任何您想要的**标签**：

```swift
ShareLink(item: URL(string: "https://www.hackingwithswift.com")!) {
    Label("Spread the word about Swift", systemImage: "swift")
}
```

您可以提供**预览**：

```swift
let example = Image(.example)

ShareLink(item: example, preview: SharePreview("Singapore Airport", image: example)) {
    Label("Click to share", systemImage: "airplane")
}
```

#swiftui 