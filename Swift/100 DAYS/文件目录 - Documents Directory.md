在 [[用户偏好数据 - UserDefaults]] 和 [[SwiftData 框架]] 间，还有种中间方案：**直接将数据写入文件**。

所有应用程序都有一个目录，用于存储我们想要的任何类型的文件。但所有 iOS 应用程序都是沙箱式的，这意味着它们在自己的容器中运行，其目录名难以猜测。

因此，我们无法也不应该猜测应用程序的安装目录，而需要依赖指向程序文档目录的特殊 URL：

```swift
print(URL.documentsDirectory)
```

既然我们有了一个可以使用的目录，就可以在其中自由读写文件了。

**读取**数据时，我们可以使用 `String(contentsOf:)` 和 `Data(contentsOf:)`。**写入**数据时，我们需要使用 `write(to:)` 方法。

`write(to:)` 方法需要两个参数：

1. 可供 write 的 URL。（通过将文档目录 URL 与文件名相结合来创建）
2. 保存时要用的额外选项。（用数组赋两个值： `.atomic` 和 `.completeFileProtection`）

- .atomic：意味着整个文件应一次性写入
- .completeFileProtection：iOS 会自动加密文件

以下是一个读写数据的完整循环：

```swift
Button("Read and Write") {
    let data = Data("Test Message".utf8)
    let url = URL.documentsDirectory.appending(path: "message.txt")

    do {
        try data.write(to: url, options: [.atomic, .completeFileProtection])
        let input = try String(contentsOf: url)
        print(input)
    } catch {
        print(error.localizedDescription)
    }
}
```

如果想要数据**自动读取**，可以这么写：

```swift
init() {
    do {
        let data = try Data(contentsOf: savePath)
        locations = try JSONDecoder().decode([Location].self, from: data)
    } catch {
        locations = []
    }
}
```

#data 