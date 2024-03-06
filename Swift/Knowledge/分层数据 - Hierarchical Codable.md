[[归档数据 - Codable|Codable]] [[协议 - Protocol|协议]]使扁平数据的解码变得轻而易举：如果您解码的是一个类型的单个实例，或者是由这些实例组成的数组或字典，那么一切都能正常工作。

但是，有时还需要解码稍微复杂一些的 JSON：在另一个数组中将包含一个数组，并使用不同的数据类型。如果您想解码这种分层数据，关键是为每一层创建单独的类型（或者说[[结构 - Struct]]）。

以下按钮将创建一个 JSON 字符串：

```swift
Button("Decode JSON") {
    let input = """
    {
        "name": "Taylor Swift",
        "address": {
            "street": "555, Taylor Swift Avenue",
            "city": "Nashville"
        }
    }
    """

    // more code to come
}
```

为了解码该数据，你需要创建与之匹配的数据结构：

```swift
struct User: Codable {
    let name: String
    let address: Address
}

struct Address: Codable {
    let street: String
    let city: String
}
```

现在，我们便可以将 JSON 字符串转换为 `Data` 类型（这正是 `Codable` 的工作原理），然后将其解码为 `User` 实例：

```swift
let data = Data(input.utf8)
let decoder = JSONDecoder()
if let user = try? decoder.decode(User.self, from: data) {
    print(user.address.street)
}
```

#data #struct 