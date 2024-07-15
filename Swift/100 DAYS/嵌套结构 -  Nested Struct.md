简单地说就是一个[[结构 - Struct]]放在另一个结构的内部。

```swift
struct Mission: Codable, Identifiable {
    struct CrewRole: Codable {
        let name: String
        let role: String
    }

    let id: Int
    let launchDate: String?
    let crew: [CrewRole]
    let description: String
}
```

它可以帮助保持代码的条理性：你可以写 `Mission.CrewRole` 而不是 `CrewRole` 。

#struct #easy 