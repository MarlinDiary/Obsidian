在处理一般的数据时，Swift 为我们提供了一个名为 Codable 的奇妙[[协议 - Protocol]]：这是一个专门用于归档和取消归档数据的协议，也就是 "**将对象转换为纯文本，然后再返回**"的花哨说法。

现在，我们要对**自定义类型**进行存档，以便将其放入 [[用户偏好数据 - UserDefaults]] 中，然后当它从 `UserDefaults` 中返回时取消存档。

在处理只有简单属性（字符串、整数、布尔值、字符串数组等）的类型时，我们只需要让 [[结构 - Struct]] 服从于 Codable 协议：

```swift
struct User: Codable {
    let firstName: String
    let lastName: String
}
```

Swift 将自动为我们生成一些代码，根据需要为我们归档和取消归档 `User` 实例，但我们仍需要告诉 Swift 何时归档以及如何处理数据。

这部分流程由名为 `JSONEncoder` 的新类型提供支持。它的任务是接收符合 `Codable` 的内容，并以 JavaScript Object Notation (JSON) 的形式将该对象发送回来。

要将 `user` 数据转换为 JSON 数据，我们需要在 `JSONEncoder` 上调用 `encode()` 方法。该方法可能会出[[处理 Function 中的错误|错]]，因此在调用该方法时应同时调用 `try` 或 `try?` 以整齐地处理错误。

例如，如果我们有一个存储 `User` 实例的属性：

```swift
@State private var user = User(firstName: "Taylor", lastName: "Swift")
```

然后，我们就可以创建一个按钮来存档用户，并将其保存到 `UserDefaults` 中：

```swift
Button("Save User") {
    let encoder = JSONEncoder()

    if let data = try? encoder.encode(user) {
        UserDefaults.standard.set(data, forKey: "UserData")
    }
}
```

这里的 `data` 常量是一种新的数据类型，它被称为 `Data` 。它可以存储你能想到的任何数据类型，如字符串、图像、压缩文件等。它是我们可以直接写入 `UserDefaults` 的数据类型之一。

当我们从另一个方向返回时--当我们有 JSON 数据并希望将其转换为 Swift `Codable` 类型时--我们应该使用 `JSONDecoder` 而不是 `JSONEncoder()` ，但过程大致相同：

```swift
init() {
    if let savedItems = UserDefaults.standard.data(forKey: "Items") {
        if let decodedItems = try? JSONDecoder().decode([ExpenseItem].self, from: savedItems) {
            items = decodedItems
            return
        }
    }

    items = []
}
```

这里，`[ExpenseItem].self`引用的是`ExpenseItem`类型的数组，而不是数组的某个特定实例。

#protocol #data #struct #hard