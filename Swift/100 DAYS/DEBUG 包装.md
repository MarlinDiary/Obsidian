尽可能在自定义数据类型中添加**静态** `example` 属性，这将大大简化预览工作：

```swift
static let example = Location(id: UUID(), name: "Buckingham Palace", description: "Lit by over 40,000 lightbulbs.", latitude: 51.501, longitude: -0.141)
```

可以用 `#if DEBUG` 和 `#endif` 对 `static let example` 行进行包装，以避免将其内置到您的应用商店版本中。

#struct #class 