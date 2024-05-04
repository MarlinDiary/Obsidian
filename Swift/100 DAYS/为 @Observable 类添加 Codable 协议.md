如果直接这样写，由于 [[属性包装器]] 的存在，会在[[归档数据 - Codable|解码和编码]]时导致一系列的问题：

```swift
@Observable
class User: Codable {
    var name = "Taylor"
}
```

为了解决这个问题，我们需要告诉 Swift 它应该如何对我们的数据进行编码和解码。

为此，我们在[[类 - Class]]中嵌套了一个名为 `CodingKeys` 的[[枚举 - Enum]]，并使其具有 `String` 原始值和 `CodingKey` 协议。

枚举中，你需要为你要保存的每个属性写入一种情况，同时写入一个包含你要为其命名的原始值：

```swift
@Observable
class User: Codable {
    enum CodingKeys: String, CodingKey {
        case _name = "name"
    }

    var name = "Taylor"
}
```

这事实上达成了一种双向映射。

#class #data 