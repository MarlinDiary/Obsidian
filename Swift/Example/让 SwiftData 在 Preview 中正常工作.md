我们需要手工创建模型容器（Model Container），并使用名为 `ModelConfiguration` 的新类型来创建，该类型允许我们请求临时内存存储。

```swift
#Preview {
    do {
        let config = ModelConfiguration(isStoredInMemoryOnly: true)
        let container = try ModelContainer(for: Book.self, configurations: config)
        let example = Book(title: "Test Book", author: "Test Author", genre: "Fantasy", review: "This was a great book; I really enjoyed it.", rating: 4)

        return DetailView(book: example)
            .modelContainer(container)
    } catch {
        return Text("Failed to create preview: \(error.localizedDescription)")
    }
}
```

创建 `Book` 实例实际上并没有在任何地方提及模型容器或配置，但这确实很重要：在没有容器的情况下尝试创建 [[SwiftData 框架]] 模型对象很可能会导致代码崩溃。

#data 