当加载 [[图像 - Image]] 以外资源的时候，我们需要进行更多的工作。*（图像属于 asset catalogs，其他资源属于 loose files）*

Bundle 允许系统将单个应用程序的所有文件存储在一个地方，在 Bundle 中查找您放置在那里的文件是很常见的事情。这需要使用一种名为 `URL` 的新数据类型，用以访问文件的位置。

如果我们想读取**主应用程序**捆绑包中文件的 **URL**，我们可以使用 `Bundle.main.url()` 。如果文件存在，它将被发送回来，否则我们将得到 `nil` ，所以这是一个[[可选项 - Optional]]的 `URL` 。这意味着我们需要像这样拆开它：

```swift
if let fileURL = Bundle.main.url(forResource: "some-file", withExtension: "txt") {
    // we found the file in our bundle!
}
```

有了 URL 后，我们就可使用特殊的初始化器将其加载到字符串中： `String(contentsOf:)` 。我们给它一个文件 URL，如果可以加载，它就会发回一个包含该文件内容的字符串。如果无法加载，它就会抛出一个[[处理 Function 中的错误|错误]]，因此你需要使用 `try` 或 `try?` 像这样调用它：

```swift
if let fileContents = try? String(contentsOf: fileURL) {
    // we loaded the file into a string!
}
```

#swiftui #struct #type #string #hard 