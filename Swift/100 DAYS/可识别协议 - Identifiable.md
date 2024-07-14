这是 Swift 内置的[[协议 - Protocol]]之一，意思是 "此类型可被唯一识别"。它只有一个要求，即必须有一个名为 `id` 的属性包含唯一标识符。

```swift
struct ExpenseItem: Identifiable {
    let id = UUID()
    let name: String
    let type: String
    let amount: Int
}
```

我们不再需要告诉[[循环视图 - ForEach]] 使用哪个属性作为标识符，它知道会有一个 `id` 属性，而且这个属性是唯一的，这正是 `Identifiable` 协议的意义所在。

```swift
ForEach(expenses.items) { item in
    Text(item.name)
}
```

#protocol #easy 