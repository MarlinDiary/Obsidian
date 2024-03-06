如果您创建了一个自定义[[结构 - Struct]]，其属性全部符合 `Hashable` 的要求，那么只需稍作修改，您就可以使整个结构符合 `Hashable` 的要求。

```swift
struct Student: Hashable {
    var id = UUID()
    var name: String
    var age: Int
}
```

#data #protocol #struct 