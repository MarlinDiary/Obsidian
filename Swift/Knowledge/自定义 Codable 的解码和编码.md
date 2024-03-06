当 JSON 数据与我们设计类型（Type）的方式相匹配时， [[归档数据 - Codable]] 可以完美地工作。不过，还有一些处理更复杂数据的方法。

## 要求 Swift 自动转换属性名称

当传入 JSON 属性用不同的命名约定时，要求 Swift 自动转换属性名就非常有用，如**蛇形到驼峰**。

我们需要在 decoder 上设置一个名为 `keyDecodingStrategy` 的属性。

下面是一个具有两个属性的 `User` 结构：

```swift
struct User: Codable {
    var firstName: String
    var lastName: String
}
```

下面是具有相同两个属性的 JSON 数据：

```swift
let str = """
{
    "first_name": "Andrew",
    "last_name": "Glouberman"
}
"""

let data = Data(str.utf8)
```

我们在调用 `decode()` 之前需要修改密钥解码策略：

```swift
do {
    let decoder = JSONDecoder()
    decoder.keyDecodingStrategy = .convertFromSnakeCase

    let user = try decoder.decode(User.self, from: data)
    print("Hi, I'm \(user.firstName) \(user.lastName)")
} catch {
    print("Whoops: \(error.localizedDescription)")
} 
```

## 创建自定义属性名称转换

如果我们的属性名称完全不同，就需要创建自定义属性名称转换。

比如下面这个属性名完全不同的 JSON：

```swift
let str = """
{
    "first": "Andrew",
    "last": "Glouberman"
}
"""
```

我们可以和 [[为 @Observable 类添加 Codable 协议]] 一样，利用[[枚举 - Enum]]进行映射：

```swift
struct User: Codable {
    enum CodingKeys: String, CodingKey {
        case firstName = "first"
        case lastName = "last"
    }

    var firstName: String
    var lastName: String
}
```

之所以习惯使用 `CodingKeys` 作为名称，是因为该名称具有超能力：如果存在 `CodingKeys` 枚举，Swift 将自动使用它来决定如何对对象进行编码和解码。另外，case name 会自动匹配 Swift property name，case value 会自动匹配 JSON property name。

## 创建完全自定义的编码和解码

这个选项适用于变化更大的情况，例如 JSON 数据以字符串形式提供了一个数字。或者，想让 SwiftData 模型符合 `Codable`。

比如下面这个怪异的 JSON：

```swift
let str = """
{
    "first": "Andrew",
    "last": "Glouberman",
    "age": "13"
}
"""
```

这意味着要在 `User` 结构中添加两样东西：

1. 一个新的初始化器，它接受一个 `Decoder` 实例，并知道如何从中**读取**属性。
2. 一个新的 `encode(to:)` 方法，它接受一个 `Encoder` 实例，并知道如何将属性**写入**其中。

这两项工作可以在 Xcode 的代码辅助下完成：

```swift
struct User: Codable {
    enum CodingKeys: String, CodingKey {
        case firstName = "first"
        case lastName = "last"
        case age
    }

    var firstName: String
    var lastName: String
    var age: Int

    init(from decoder: Decoder) throws {
        let container = try decoder.container(keyedBy: CodingKeys.self)
        self.firstName = try container.decode(String.self, forKey: .firstName)
        self.lastName = try container.decode(String.self, forKey: .lastName)
        self.age = try container.decode(Int.self, forKey: .age)
    }

    func encode(to encoder: Encoder) throws {
        var container = encoder.container(keyedBy: CodingKeys.self)
        try container.encode(self.firstName, forKey: .firstName)
        try container.encode(self.lastName, forKey: .lastName)
        try container.encode(self.age, forKey: .age)
    }
}
```

在使用 [[SwiftData 框架]] 时，添加 `Codable` 支持意味着**创建自定义实现**。要记住上述所有代码是很烦人的，而且 Xcode 几乎肯定不会提供帮助。因此，只需创建一个 Xcode 可以生成 `Codable` 实现的临时结构（包含一个 **property** 和一个 **one-case `CodingKeys` enum**），然后使用其结构来辅助创建 SwiftData 类的 `Codable` 。

以上自动生成的代码中还需要修改两处。

1. 要以字符串形式读取，再转化为整数：

```swift
let stringAge = try container.decode(String.self, forKey: .age)
self.age = Int(stringAge) ?? 0
```

2. 要转化为字符串，再编码：

```swift
try container.encode(String(self.age), forKey: .age)
```

#data 